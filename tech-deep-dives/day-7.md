# FastAPI Fundamentals

## What I Learned

Today I learned the fundamentals of:
- FastAPI
- REST API development
- request/response flow
- routing
- dependency injection
- async programming
- API validation

---

# 1. What is FastAPI?

FastAPI is a modern Python web framework used for building:
- backend APIs
- microservices
- high-performance web applications

It is built on top of:
- Starlette
- Pydantic

---

# Why FastAPI is Popular

FastAPI provides:
- very fast performance
- automatic API documentation
- easy request validation
- async support
- clean developer experience

---

# Main Advantages

- fast development
- simple syntax
- automatic Swagger docs
- async request handling
- built-in validation
- ideal for AI/ML APIs

---

# 2. Why FastAPI is Called “Fast”

FastAPI is fast because:
- it uses ASGI instead of WSGI
- supports asynchronous programming
- handles concurrent requests efficiently

Performance is comparable to:
- Node.js
- Go

and much faster than traditional synchronous Python frameworks in many cases.

---

# 3. When to Use FastAPI

FastAPI is commonly used for:
- REST APIs
- AI/LLM backends
- machine learning inference APIs
- microservices
- async applications
- real-time systems

---

# Real-World Examples

FastAPI is heavily used in:
- AI agents
- chatbot backends
- recommendation systems
- data pipelines
- internal backend services

---

# 4. FastAPI Basic API Example

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello FastAPI"}
```

---

# Key Understanding

## FastAPI()

Creates:
> FastAPI application instance

---

## @app.get("/")

Defines:
> GET API endpoint

Example:

```txt
GET /
```

---

## return

FastAPI automatically converts:
```txt
Python Dictionary → JSON Response
```

---

# 5. FastAPI Request Flow

```txt
Client Request
      ↓
FastAPI Route
      ↓
Business Logic
      ↓
Database/API Calls
      ↓
JSON Response
```

This is the core backend request lifecycle.

---

# 6. HTTP Methods in FastAPI

FastAPI supports standard REST methods.

| Method | Usage |
|---|---|
| GET | Fetch data |
| POST | Create data |
| PUT | Update full resource |
| PATCH | Partial update |
| DELETE | Delete resource |

---

# Example

```python
@app.post("/users")
def create_user():
    return {"message": "User Created"}
```

---

# 7. Path Parameters

Used for:
> dynamic values inside URL

---

# Example

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id}
```

---

# Example Request

```txt
GET /users/10
```

---

# Key Learning

FastAPI automatically validates:
```python
user_id: int
```

Type validation is built-in.

---

# 8. Query Parameters

Used for:
- filtering
- searching
- pagination

---

# Example

```python
@app.get("/search")
def search(q: str):
    return {"query": q}
```

---

# Example Request

```txt
/search?q=fastapi
```

---

# 9. Request Body

Used mainly with:
- POST
- PUT
- PATCH

FastAPI commonly uses:
> Pydantic Models

for request validation.

---

# Example

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
```

---

# API Using Model

```python
@app.post("/users")
def create_user(user: User):
    return user
```

---

# Key Learning

Pydantic automatically:
- validates request data
- checks data types
- returns validation errors

---

# 10. Automatic API Documentation

One of FastAPI’s best features.

FastAPI automatically generates:
- Swagger UI
- OpenAPI documentation

---

# URLs

```txt
/docs
```

Swagger UI

```txt
/redoc
```

ReDoc Documentation

---

# Benefits

- easy API testing
- frontend-backend collaboration
- faster development

---

# 11. Dependency Injection

FastAPI supports:
> Dependency Injection

similar to Spring Boot.

Used for:
- database connections
- authentication
- reusable logic

---

# Example

```python
from fastapi import Depends
```

Dependencies are automatically injected into APIs.

---

# 12. Async Programming in FastAPI

FastAPI supports:
> asynchronous APIs

using:

```python
async def
```

---

# Example

```python
@app.get("/")
async def home():
    return {"message": "Async API"}
```

---

# Why Async Matters

Async APIs handle:
- multiple requests concurrently
- long-running operations efficiently

Useful for:
- API calls
- database queries
- external service communication

---

# 13. FastAPI vs Flask vs Django

| Feature | FastAPI | Flask | Django |
|---|---|---|---|
| Performance | Very Fast | Medium | Medium |
| Async Support | Built-in | Limited | Partial |
| Validation | Built-in | Manual | Manual |
| Auto Docs | Yes | No | No |
| Best For | APIs & Microservices | Small Apps | Full Web Apps |

---

# 14. FastAPI + Database Flow

Typical backend architecture:

```txt
Frontend
    ↓
FastAPI Route
    ↓
Service Layer
    ↓
Database
    ↓
JSON Response
```

---

# Example Real-World Flow

User places order:

```txt
POST /orders
```

Flow:
- FastAPI receives request
- validates JSON
- service processes business logic
- database stores order
- JSON response returned

---

# 15. FastAPI + AI Systems

FastAPI is extremely popular in AI engineering because:
- Python is dominant in AI/ML
- integrates easily with ML models
- lightweight and fast
- easy API deployment

Common use cases:
- LLM APIs
- RAG systems
- AI agents
- model inference APIs

---

# 16. Common Interview Questions

Important FastAPI topics for interviews:
- async vs sync APIs
- request validation
- REST APIs
- Pydantic models
- dependency injection
- middleware
- authentication
- API routing
- FastAPI vs Flask

---

# 17. FastAPI Architecture Flow

```txt
Client
   ↓
FastAPI Route
   ↓
Validation (Pydantic)
   ↓
Business Logic
   ↓
Database / External APIs
   ↓
JSON Response
```

---

# Main Takeaways

FastAPI is widely used because it provides:
- high performance
- clean syntax
- async support
- automatic validation
- easy API development
