# API Design for System Design Interviews

## What I Learned

Today I learned the fundamentals of:
- API Design
- REST APIs
- GraphQL
- gRPC
- HTTP methods
- idempotency
- pagination
- API versioning

APIs are one of the most important parts of backend engineering because they define how different systems communicate with each other. 

---

# 1. What is an API?

API stands for:

> Application Programming Interface

An API allows different systems to communicate with each other.

Examples:
- Mobile App → Backend Server
- Frontend → Backend API
- Payment Service → Booking Service

APIs define:
- how requests are sent
- how responses are returned
- how data is created/read/updated/deleted

---

# 2. Main API Types

There are 3 major API styles commonly discussed in system design interviews.

| API Type | Best For | Main Idea |
|---|---|---|
| REST | Most web applications | Resource-based APIs |
| GraphQL | Flexible frontend apps | Client chooses exact data |
| gRPC / RPC | Internal microservices | Procedure/function calls |

---

# 3. REST APIs (Most Important)

REST is the default API style in most interviews.

REST mainly works around:
> Resources

Examples:
- users
- bookings
- events
- tickets

REST uses standard HTTP methods:
- GET
- POST
- PUT
- PATCH
- DELETE

---

# 4. REST Resource Design

Good REST APIs focus on:
> things/resources

instead of actions.

---

## Good REST Design

```txt
/events
/bookings
/tickets
```

---

## Bad REST Design

```txt
/createBooking
/bookTicket
```

Resources should usually be:
> plural nouns

---

# 5. Common REST API Examples

```txt
GET /events
GET /events/123
GET /events/123/tickets
POST /events/123/bookings
DELETE /bookings/456
```

---

# 6. HTTP Methods Explained

---

# GET

Used to:
- retrieve data

Example:

```txt
GET /events/123
```

Important:
- does NOT modify data
- safe operation
- idempotent

---

# POST

Used to:
- create resources

Example:

```txt
POST /events/123/bookings
```

Important:
- NOT idempotent
- multiple requests may create duplicates

---

# PUT

Used to:
- completely replace/update resource

Example:

```txt
PUT /users/1
```

Important:
- idempotent
- same request → same final state

---

# PATCH

Used for:
- partial updates

Example:

```txt
PATCH /users/1
```

Important:
- modifies only specific fields
- not always idempotent

---

# DELETE

Used to:
- remove resource

Example:

```txt
DELETE /bookings/1
```

Important:
- idempotent
- deleting multiple times keeps same final state

---

# 7. Idempotency (Very Important Concept)

An API is idempotent if:
> repeating the same request gives the same final result.

---

## Idempotency Table

| Method | Idempotent? |
|---|---|
| GET | ✅ |
| PUT | ✅ |
| DELETE | ✅ |
| POST | ❌ |
| PATCH | Usually ❌ |

---

# Why Idempotency Matters

Network retries happen frequently.

Without idempotency:
- duplicate payments
- duplicate bookings
- duplicate transactions

can happen.

Idempotent APIs make retries safer.

---

# 8. Passing Data in REST APIs

There are 3 common ways.

---

# Path Parameters

Used for:
- identifying specific resource

Example:

```txt
/events/123
```

Where:
```txt
123 = event ID
```

Use when value is:
> required

---

# Query Parameters

Used for:
- filtering
- sorting
- pagination

Example:

```txt
/events?city=NYC&page=2
```

Use when parameters are:
> optional

---

# Request Body

Used to send:
- actual request data

Example:

```json
{
  "tickets": 2,
  "payment_method": "card"
}
```

Mostly used with:
- POST
- PUT
- PATCH

---

# 9. Example Full REST Request

```txt
POST /events/123/bookings?notify=true
```

Request Body:

```json
{
  "tickets": [
    {
      "section": "VIP",
      "quantity": 2
    }
  ],
  "payment_method": "credit_card"
}
```

---

# Breakdown

| Part | Purpose |
|---|---|
| /events/123 | specific event |
| notify=true | optional behavior |
| JSON Body | actual booking data |

---

# 10. API Responses

Responses usually contain:
- status code
- headers
- response body

---

# Common Status Codes

| Code | Meaning |
|---|---|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 500 | Server Error |

---

# 11. GraphQL

GraphQL allows clients to:
> request exactly the data they need

Instead of multiple REST endpoints:

```txt
/events
/venues
/tickets
```

GraphQL usually uses:
> one endpoint

---

# Example GraphQL Query

```graphql
query {
  event(id: "123") {
    name
    date
    venue {
      name
    }
  }
}
```

Client receives:
- only requested fields

---

# Why GraphQL Exists

GraphQL mainly solves:

---

## Over-Fetching

Getting:
- unnecessary data

---

## Under-Fetching

Not getting:
- enough data

Common in:
- mobile apps
- frontend-heavy systems
- dashboards

---

# When to Use GraphQL

Use when:
- frontend flexibility matters
- different clients need different data
- reducing unnecessary data transfer is important

Avoid when:
- system is simple
- REST already works well

REST is still the default interview choice.

---

# GraphQL Challenge — N+1 Query Problem

Example:
- fetch 100 events
- then separately fetch 100 venues

This creates:
- excessive database queries

Solutions:
- batching
- dataloaders

---

# 12. RPC / gRPC

RPC means:
> Remote Procedure Call

Instead of resources,
RPC focuses on:
> actions/functions

Examples:

```txt
getEvent()
createBooking()
checkPermission()
```

---

# Why gRPC is Fast

gRPC uses:
- Protocol Buffers (protobuf)
- binary serialization
- HTTP/2

Faster than:
- JSON REST APIs

---

# Where gRPC is Common

Mostly used for:
- internal microservices
- backend-to-backend communication

Examples:
- Booking Service ↔ Payment Service
- Auth Service ↔ User Service

---

# When to Use gRPC

Use when:
- performance matters
- services communicate frequently
- type safety is important
- internal service communication is heavy

---

# 13. Protocol Buffers (Protobuf)

Protobuf defines:
- API contracts

Example:

```protobuf
service TicketService {
  rpc GetEvent(GetEventRequest) returns (Event);
}
```

Benefits:
- strict typing
- auto-generated code
- smaller payloads
- multi-language support

---

# 14. API Pagination

Never return:
- millions of records at once

Pagination helps:
- scalability
- performance
- memory efficiency

---

# Offset-Based Pagination

Example:

```txt
/events?offset=20&limit=10
```

Simple but can cause:
- duplicate records
- missing records

when data changes.

---

# Cursor-Based Pagination

Example:

```txt
/events?cursor=abc123&limit=10
```

Uses pointer to last record.

Better for:
- real-time systems
- large datasets
- scalable applications

---

# 15. API Versioning

APIs evolve over time.

Versioning prevents:
- breaking old clients

---

# URL Versioning (Most Common)

```txt
/v1/events
/v2/events
```

Easy to understand and commonly preferred in interviews.

---

# 16. REST vs GraphQL vs gRPC

| Feature | REST | GraphQL | gRPC |
|---|---|---|---|
| Style | Resource-based | Query-based | Procedure-based |
| Best For | Web APIs | Flexible frontend apps | Internal services |
| Data Fetching | Fixed | Flexible | Fixed |
| Performance | Good | Good | Excellent |
| Complexity | Low | Medium | Medium/High |
| Interview Default | ✅ | Sometimes | Internal APIs |

---

# 17. Real-World Examples

| System | Likely API Style |
|---|---|
| Instagram Feed API | REST |
| GitHub API | REST + GraphQL |
| Uber Internal Services | gRPC |
| Payment Service Communication | gRPC |
| Mobile Dashboard App | GraphQL |

---

# Main Takeaways

APIs define communication between systems.

Important concepts learned:
- REST API design
- HTTP methods
- idempotency
- GraphQL
- gRPC
- pagination
- versioning

Key interview understanding:
- REST is default choice
- GraphQL solves flexible frontend fetching
- gRPC is best for fast internal service communication

Understanding API design is one of the most important foundations for:
- backend engineering
- distributed systems
- scalable applications
- system design interviews.
