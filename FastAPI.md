# TIL: FastAPI 🚀

**Date:** 2026-09-16

Today I learned the basics of **FastAPI**, a modern Python framework for building APIs.

## What I Learned

### 1. Creating a FastAPI Application

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def home():
    return {
        "message": "Hello FastAPI"
    }
```

FastAPI uses decorators such as `@app.get()` to define API routes.

---

### 2. HTTP Methods

FastAPI supports common HTTP methods:

```python
@app.get("/users")
def get_users():
    pass


@app.post("/users")
def create_user():
    pass


@app.put("/users/{user_id}")
def update_user(user_id: int):
    pass


@app.delete("/users/{user_id}")
def delete_user(user_id: int):
    pass
```

These can be used to build REST APIs and CRUD operations.

---

### 3. Path Parameters

Path parameters can be defined directly in the route:

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {
        "user_id": user_id
    }
```

FastAPI uses Python type hints to understand that `user_id` should be an integer.

---

### 4. Query Parameters

Query parameters can be defined using function parameters:

```python
@app.get("/users")
def get_users(limit: int = 10):
    return {
        "limit": limit
    }
```

Example:

```text
/users?limit=20
```

---

### 5. Request Body with Pydantic

FastAPI works with **Pydantic** for request validation.

```python
from pydantic import BaseModel


class User(BaseModel):
    name: str
    email: str
    age: int
```

The model can then be used in an endpoint:

```python
@app.post("/users")
def create_user(user: User):
    return {
        "message": "User created",
        "user": user
    }
```

FastAPI automatically validates incoming request data.

---

### 6. Automatic API Documentation

FastAPI automatically generates interactive API documentation.

Swagger UI:

```text
http://127.0.0.1:8000/docs
```

ReDoc:

```text
http://127.0.0.1:8000/redoc
```

This makes it easy to test and understand APIs during development.

---

## FastAPI vs Express

Since FastAPI and Express are both commonly used for REST APIs:

| Express.js                                | FastAPI             |
| ----------------------------------------- | ------------------- |
| JavaScript / Node.js                      | Python              |
| `app.get()`                               | `@app.get()`        |
| `req.body`                                | Pydantic model      |
| Middleware                                | Dependencies        |
| Manual validation commonly used           | Pydantic validation |
| API docs usually require additional setup | Automatic API docs  |

---

## Simple FastAPI Example

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class User(BaseModel):
    name: str
    email: str
    age: int


@app.get("/")
def home():
    return {
        "message": "User API"
    }


@app.get("/users")
def get_users():
    return {
        "users": []
    }


@app.post("/users")
def create_user(user: User):
    return {
        "message": "User created",
        "user": user
    }
```

## Key Takeaways

* FastAPI is a Python framework for building APIs.
* Routes are defined using decorators such as `@app.get()` and `@app.post()`.
* Python type hints are heavily used.
* Pydantic provides request data validation.
* FastAPI automatically generates Swagger and ReDoc documentation.
* FastAPI can be used to build REST APIs, backend services, and ML model APIs.

## Next Topics

* Pydantic validation
* Response models
* Error handling
* Dependency Injection
* PostgreSQL + SQLAlchemy
* Authentication with JWT
* API testing with Pytest
* Dockerizing FastAPI
* Deploying FastAPI
* Serving AI/ML models through FastAPI
