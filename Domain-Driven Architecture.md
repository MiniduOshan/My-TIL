# TIL: Domain-Driven Architecture

📅 Date: 2026-08-29

Today I learned about **Domain-Driven Architecture (DDA)** and how organizing an application around business domains can make large applications easier to maintain and scale.

### What is Domain-Driven Architecture?

**Domain-Driven Architecture** is an approach where the application is structured around its **business domains or features**, rather than organizing everything only by technical types such as controllers, models, and views.

For example, instead of having:

```text
app/
├── Models/
├── Controllers/
├── Services/
└── Requests/
```

a domain-oriented application can be organized like:

```text
app/
├── Domains/
│   ├── Course/
│   │   ├── Models/
│   │   ├── Actions/
│   │   ├── Services/
│   │   ├── Controllers/
│   │   └── Requests/
│   │
│   ├── Enrollment/
│   │   ├── Models/
│   │   ├── Actions/
│   │   ├── Services/
│   │   └── Controllers/
│   │
│   ├── Assessment/
│   │   ├── Models/
│   │   ├── Actions/
│   │   └── Services/
│   │
│   └── User/
│       ├── Models/
│       ├── Actions/
│       └── Services/
```

### Traditional MVC vs Domain-Driven Architecture

In a traditional Laravel MVC structure, files are grouped according to their technical responsibility. As the application grows, folders such as `Models` and `Controllers` can become very large.

For example:

```text
Models/
├── User.php
├── Course.php
├── Enrollment.php
├── Assessment.php
├── Payment.php
└── Certificate.php
```

With Domain-Driven Architecture, related functionality is grouped together:

```text
Domains/
├── Course/
├── Enrollment/
├── Assessment/
├── Payment/
└── Certificate/
```

This creates **high cohesion**, because everything related to a particular business capability is kept together.

### Benefits

**1. High Cohesion**

All functionality related to a domain stays together. If I need to modify course-related functionality, I can primarily work inside the `Course` domain.

**2. Better Scalability**

New business features can be added as new domains without continuously increasing the size of global folders.

**3. Easier Maintenance**

Business logic is easier to locate because it is organized according to business concepts rather than technical file types.

**4. Better Testability**

Business rules can be moved into dedicated `Actions` and `Services`, allowing them to be tested independently from HTTP requests and UI components.

**5. Clear Business Boundaries**

Domains such as `Course`, `Enrollment`, `Assessment`, and `Payment` represent real business capabilities. This makes the architecture easier to understand.

### Example: LMS

An LMS is a good candidate for domain-oriented architecture because it contains several independent business areas:

```text
LMS
│
├── Course
├── Enrollment
├── Assessment
├── User
├── Payment
├── Certification
└── Notifications
```

Each domain can contain its own models, actions, services, requests, and controllers.

For example:

```text
Domains/
└── Enrollment/
    ├── Models/
    │   └── Enrollment.php
    ├── Actions/
    │   └── EnrollStudent.php
    ├── Services/
    │   └── EnrollmentService.php
    ├── Controllers/
    │   └── EnrollmentController.php
    └── Requests/
        └── EnrollmentRequest.php
```

The `EnrollStudent` action could contain the business operation for enrolling a student, instead of putting the entire process inside a controller or Livewire component.

### Domain-Driven Architecture vs More Advanced Architectures

Domain-driven organization does not necessarily mean that the application must become microservices.

A Laravel application can remain a **modular monolith** while using domain boundaries:

```text
             Laravel Application
                    │
       ┌────────────┼────────────┐
       │            │            │
    Course      Enrollment    Assessment
       │            │            │
    Models        Models       Models
    Actions       Actions      Actions
    Services      Services     Services
```

If the application becomes significantly larger, other architectural patterns can be introduced.

**Hexagonal Architecture** can be used to separate the core business logic from frameworks and external systems.

**CQRS (Command Query Responsibility Segregation)** can separate read operations from write operations when the system has demanding performance requirements.

**Microservices** can eventually separate individual domains into independent applications, but this introduces additional complexity such as distributed communication, deployment, monitoring, and data consistency.
