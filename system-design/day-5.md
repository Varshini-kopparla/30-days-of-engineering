# Advanced API Design Concepts

## What I Learned

Today I learned some important real-world API design concepts used in scalable backend systems, including:
- pagination
- API versioning
- authentication
- authorization
- JWT tokens
- API keys
- RBAC
- rate limiting

These concepts are heavily used in production systems and are commonly discussed in system design interviews.

---

# 1. Pagination

When APIs return large datasets,
they should NOT send everything at once.

Example:
- millions of events
- bookings
- messages
- users

Returning huge datasets:
- increases latency
- consumes memory
- slows applications

Solution:
> Pagination

Pagination breaks results into smaller chunks.

---

# 2. Offset-Based Pagination

Simplest pagination approach.

Example:

```txt
/events?offset=20&limit=10
```

Meaning:
- skip first 20 records
- return next 10 records

---

## Advantages
- simple
- easy to implement
- easy to understand

---

## Problems

If new data gets inserted while paging:
- records may shift
- duplicates may appear
- some records may be skipped

Not ideal for:
- real-time systems
- frequently changing datasets

---

# 3. Cursor-Based Pagination

Instead of counting records,
cursor pagination uses:
> pointer to last record

Example:

First request:

```txt
/events?limit=10
```

Response:

```json
{
  "events": [...],
  "next_cursor": "abc123"
}
```

Next request:

```txt
/events?cursor=abc123&limit=10
```

---

## Advantages
- more stable
- better for large datasets
- handles real-time inserts better

---

## Disadvantages
- harder to implement
- difficult to jump directly to page numbers

---

# Key Learning

For interviews:
- offset pagination is usually acceptable
- cursor pagination is preferred for large-scale real-time systems

---

# 4. API Versioning

APIs evolve over time.

Without versioning:
- old clients may break when APIs change

Versioning helps maintain:
- backward compatibility

---

# URL Versioning (Most Common)

Example:

```txt
/v1/events
/v2/events
```

Advantages:
- simple
- explicit
- easy to understand

Most common approach in interviews.

---

# Header Versioning

Version passed inside HTTP headers.

Example:

```txt
Accept-Version: v2
```

Cleaner URLs but less visible.

---

# Key Learning

In interviews:
> URL versioning is usually safest and easiest to explain.

---

# 5. Authentication vs Authorization

These are different concepts.

---

# Authentication

Answers:
> “Who are you?”

Verifies user identity.

Examples:
- login
- JWT verification
- sessions

---

# Authorization

Answers:
> “What are you allowed to do?”

Checks permissions after authentication.

Example:
- customer can cancel own booking
- admin can access everything

---

# 6. API Keys

API keys are long secret strings used to identify applications.

Example:

```txt
Authorization: Bearer sk_live_abc123
```

Mostly used for:
- server-to-server communication
- third-party developer APIs

---

## Advantages
- simple
- easy to implement

---

## Limitations
- no user context
- usually long-lived
- less suitable for user sessions

---

# 7. JWT Tokens

JWT stands for:
> JSON Web Token

JWT stores user information directly inside token.

Example payload:

```json
{
  "user_id": "123",
  "email": "john@example.com",
  "role": "customer"
}
```

---

# Why JWT is Powerful

Server can:
- verify token signature
- identify user
- read permissions

without database lookup every time.

---

## Advantages
- stateless authentication
- scalable
- works well in distributed systems
- ideal for web/mobile apps

---

# Common JWT Flow

```txt
User Login
    ↓
Server generates JWT
    ↓
Client stores token
    ↓
Client sends JWT with requests
    ↓
Server validates JWT
```

---

# Key Learning

Use:
- API Keys → service communication
- JWT → user authentication

---

# 8. Role-Based Access Control (RBAC)

Different users have different permissions.

Example roles:

```txt
customer
venue_manager
admin
```

---

# Example Permissions

| Role | Permissions |
|---|---|
| Customer | Book tickets |
| Venue Manager | Create events |
| Admin | Full system access |

---

# API Authorization Example

```txt
GET /bookings/123
```

System checks:
1. Is user authenticated?
2. Does user own booking?
3. Is user admin?

---

# 9. Rate Limiting

Rate limiting prevents:
- abuse
- spam
- excessive traffic

Limits how many requests users can make.

---

# Example Limits

```txt
100 requests/hour
10 booking attempts/minute
```

---

# Why Rate Limiting Matters

Protects systems from:
- DDoS attacks
- bots
- ticket scalping
- accidental overload

---

# Common Response

When limit exceeded:

```txt
429 Too Many Requests
```

---

# 10. Where Rate Limiting is Applied

Usually implemented at:
- API Gateway
- Load Balancer
- Middleware layer

---

# Main Takeaways

Modern APIs need more than just endpoints.

Important production concepts include:
- pagination
- API versioning
- authentication
- authorization
- JWT tokens
- RBAC
- rate limiting

Key interview understanding:
- offset pagination is simpler
- cursor pagination scales better
- JWT is ideal for user authentication
- API keys work well for service communication
- RBAC manages permissions
- rate limiting protects systems

These concepts are critical for:
- backend engineering
- distributed systems
- scalable APIs
- secure production systems
- system design interviews.
