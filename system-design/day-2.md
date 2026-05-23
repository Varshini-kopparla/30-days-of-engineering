# Application Layer Protocols & Real-Time Communication

## What I Learned

Today I learned how modern applications communicate over the internet using protocols like:

- HTTP
- HTTPS
- REST
- GraphQL
- gRPC
- WebSockets
- WebRTC

These protocols form the foundation of APIs, backend systems, real-time applications, and distributed systems. 

---

# 1. What is the Application Layer?

The Application Layer is the top networking layer where applications communicate with each other.

This is the layer developers mostly work with.

Examples:
- browsers
- mobile apps
- APIs
- chat applications
- streaming platforms

It works on top of lower networking layers like:
- TCP
- UDP
- IP

Simple flow:

```txt
Application
↓
HTTP / WebSocket / gRPC
↓
TCP / UDP
↓
Internet
```

---

# 2. HTTP — Foundation of the Web

HTTP (HyperText Transfer Protocol) is the standard protocol used for communication between clients and servers.

Simple flow:

```txt
Browser → Request → Server
Server → Response → Browser
```

Most websites and APIs use HTTP.

---

# 3. HTTP is Stateless

HTTP is called a:

> Stateless protocol

Meaning:
- every request is independent
- server does not automatically remember previous requests

Example:
- Request 1 → Login
- Request 2 → Fetch profile

The second request does not automatically know about the first.

This is why applications use:
- cookies
- sessions
- JWT tokens

to maintain user state.

---

# 4. HTTP Request Structure

An HTTP request mainly contains:

## Method

Defines the action.

Common methods:

| Method | Purpose |
|---|---|
| GET | Fetch data |
| POST | Create data |
| PUT | Update full resource |
| PATCH | Partial update |
| DELETE | Delete resource |

---

## Headers

Extra metadata sent with request.

Examples:
- Content-Type
- Authorization
- Accept-Encoding

---

## Body

Actual data sent to server.

Usually JSON.

Example:

```json
{
  "name": "Varshini"
}
```

---

# 5. HTTP Response Structure

Server sends back:
- status code
- headers
- response body

---

## Common Status Codes

### Success

| Code | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |

### Redirects

| Code | Meaning |
|---|---|
| 301 | Permanent Redirect |
| 302 | Temporary Redirect |

### Client Errors

| Code | Meaning |
|---|---|
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 429 | Too Many Requests |

### Server Errors

| Code | Meaning |
|---|---|
| 500 | Internal Server Error |
| 502 | Bad Gateway |

---

# 6. HTTPS

HTTPS = Secure HTTP

HTTPS adds:
- encryption
- authentication
- security

using:
- TLS - Transport Layer Security 
- SSL - Secure Sockets Layer

Without HTTPS:
- anyone on the network could potentially read traffic

With HTTPS:
- communication becomes encrypted and secure

Used for:
- passwords
- payments
- personal information
- authentication tokens

---

# 7. REST APIs

REST (Representational State Transfer) is the most common API architecture style.

REST APIs mainly use:
- HTTP methods
- URLs
- JSON responses

---

# 8. REST Resource Design

REST focuses on:

> Resources, not actions

Good REST design:

```txt
GET /users/1
```

Avoid action-based APIs like:

```txt
getUser()
```

---

# 9. Common REST API Examples

```txt
GET /users/1
```
Fetch user

```txt
POST /users
```
Create user

```txt
PUT /users/1
```
Update user

```txt
DELETE /users/1
```
Delete user

---

# 10. Why REST is Popular

## Advantages
- simple
- easy to understand
- human readable
- works everywhere
- browser friendly

## Disadvantages
- over-fetching data
- under-fetching data
- larger JSON payloads

---

# 11. GraphQL

GraphQL was created by Facebook to solve some REST limitations.

Instead of fixed API responses,
frontend requests exactly the data it needs.

Example:

```graphql
{
  user {
    name
    profile
  }
}
```

---

# 12. Why GraphQL Exists

With REST:
frontend may need:
- multiple API calls
- or very large responses with unnecessary data

GraphQL solves this by:
- returning only requested fields

---

# 13. GraphQL Advantages & Disadvantages

## Advantages
- flexible
- less data transfer
- faster frontend iteration
- great for mobile apps

## Disadvantages
- more backend complexity
- caching becomes harder
- expensive queries possible

---

# 14. gRPC

gRPC (Google Remote Procedure Call) is a high-performance communication protocol.

It uses:
- HTTP/2
- Protocol Buffers

instead of JSON.

---

# 15. Protocol Buffers

Protocol Buffers are:
- compact
- binary-based
- faster than JSON

JSON is human-readable but heavier.

Protocol Buffers are optimized for performance.

---

# 16. Why gRPC is Fast

gRPC is fast because it uses:
- binary serialization
- smaller payloads
- HTTP/2
- streaming support

---

# 17. Where gRPC is Used

Mostly used for:
- internal microservices
- backend-to-backend communication

Less common for:
- public browser APIs

---

# 18. REST vs GraphQL vs gRPC

| Feature | REST | GraphQL | gRPC |
|---|---|---|---|
| Easy to use | ✅ | Medium | Hard |
| Flexible | Medium | High | Low |
| Performance | Medium | Medium | Very High |
| Human readable | ✅ | ✅ | ❌ |
| Browser friendly | ✅ | ✅ | Limited |
| Best For | Public APIs | Flexible frontend | Internal microservices |

---

# 19. Real-Time Communication

Traditional HTTP works like:

```txt
Request → Response → Connection closes
```

But applications like:
- WhatsApp
- Uber
- Discord
- trading apps
- multiplayer games

need continuous real-time updates.

---

# 20. Server-Sent Events (SSE)

SSE allows:
- server → client streaming

using one long-lived HTTP connection.

Used for:
- notifications
- stock updates
- live feeds

---

# 21. SSE Limitations

SSE supports:
- only one-way communication

Limitations:
- client cannot continuously send messages back
- proxy/firewall compatibility issues possible

---

# 22. WebSockets

WebSockets provide:

> Full-duplex communication

Meaning:
- client and server can both send messages anytime

Connection remains open continuously.

---

# 23. How WebSockets Work

### Step 1
Start as normal HTTP connection.

### Step 2
Connection upgrades to WebSocket.

### Step 3
Persistent connection stays open.

### Step 4
Both sides exchange messages in real time.

---

# 24. Why WebSockets Matter

WebSockets are heavily used in:
- WhatsApp
- Discord
- online gaming
- live collaboration tools
- chat systems

Because they provide:
- low latency
- persistent connection
- real-time bidirectional communication

---

# 25. WhatsApp Double Tick Example

### Single Tick
```txt
User → WhatsApp Server
```

Server received message.

---

### Double Tick
```txt
WhatsApp Server → Receiver Device
```

Receiver device got the message.

---

### Blue Tick

Receiver opened/read the message.

---

# 26. Why WebSockets Are Useful

Without WebSockets:
applications repeatedly ask:

```txt
"Any new message?"
```

This is called:
> Polling

Polling creates unnecessary network requests.

With WebSockets:
- server pushes updates instantly
- communication becomes real time

---

# 27. WebSocket Advantages & Disadvantages

## Advantages
- real-time communication
- low latency
- bidirectional messaging
- persistent connection

## Disadvantages
- stateful connections
- harder load balancing
- infrastructure complexity at scale

---

# 28. WebRTC

WebRTC enables:

> Peer-to-peer communication

directly between devices.

Used for:
- video calls
- voice calls
- conferencing
- screen sharing

Examples:
- Google Meet
- Discord calls
- Zoom (partially)

---

# 29. Why WebRTC Uses UDP

Unlike HTTP/WebSockets,
WebRTC mainly uses:

> UDP

because:
- lower latency matters more
- small packet loss is acceptable
- better for audio/video streaming

---

# 30. NAT Problem

Most devices sit behind:
- routers
- firewalls

which block direct incoming connections.

This creates connection challenges for peer-to-peer systems.

---

# 31. STUN Server

STUN servers help devices discover:
- public IP address
- public port

Used for establishing direct peer-to-peer communication.

---

# 32. TURN Server

If direct connection fails:
- traffic is routed through TURN server

TURN acts as a relay between devices.

---

# 33. WebRTC Connection Flow

### Step 1
Clients contact signaling server.

### Step 2
Exchange connection information.

### Step 3
Attempt direct connection.

### Step 4
Fallback to TURN server if needed.

---

# Final Understanding

Modern distributed systems rely heavily on communication protocols.

Different protocols solve different problems:

- HTTP → standard web communication
- REST → simple APIs
- GraphQL → flexible frontend queries
- gRPC → high-performance internal services
- WebSockets → real-time bidirectional communication
- WebRTC → peer-to-peer media communication

Understanding these protocols is essential for:
- backend engineering
- distributed systems
- scalability
- system design interviews
- real-world application architecture
