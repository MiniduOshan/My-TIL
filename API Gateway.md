# TIL: API Gateway

📅 Date: 2026-08-11

Today I learned about **API Gateway**.

An **API Gateway** acts as a single entry point between clients and backend services. Instead of the frontend directly communicating with multiple APIs, requests are first sent to the API Gateway, which then routes them to the appropriate service.

```text
Client
   │
   ▼
API Gateway
   │
   ├──► User API
   ├──► Product API
   ├──► Order API
   └──► Payment API
```

## What Does an API Gateway Do?

- **Request Routing** – Sends requests to the correct backend service.
- **Authentication** – Verifies access tokens and user identity.
- **Authorization** – Controls what users are allowed to access.
- **Rate Limiting** – Limits excessive API requests.
- **Load Balancing** – Distributes requests across backend instances.
- **Caching** – Stores frequently requested responses.
- **Logging & Monitoring** – Tracks API requests and performance.
- **Security** – Provides an additional security layer between clients and backend services.

## API vs API Gateway

| API | API Gateway |
|---|---|
| Provides functionality | Manages access to APIs |
| Contains business logic | Mainly handles routing and policies |
| Performs operations | Forwards requests |
| Usually belongs to a service | Sits in front of multiple services |
| Example: Product API | Example: Gateway for Product, User & Order APIs |

## Example

### Without API Gateway

```text
Frontend ──► User API
Frontend ──► Product API
Frontend ──► Order API
```

### With API Gateway

```text
              ┌──► User API
Frontend ──► API Gateway ──► Product API
              └──► Order API
```

## Key Takeaway

> **API provides functionality, while an API Gateway manages and controls access to multiple APIs.**

In simple terms:

```text
API          = Does the work
API Gateway  = Controls and routes the requests
```
