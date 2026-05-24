# Load Balancing, Networking Reliability & Scaling

## What I Learned

Today I learned how large-scale distributed systems handle:
- scaling
- traffic distribution
- persistent connections
- regional latency
- failures and retries
- high availability

These concepts are extremely important in system design because modern applications must handle millions of users reliably and efficiently.

---

# 1. Vertical vs Horizontal Scaling

There are two main ways to scale systems:

## Vertical Scaling
Increase server power:
- more CPU
- more RAM
- larger machine

Example:
```txt
Small Server → Bigger Server
```

Advantages:
- simpler architecture
- easier management

Limitations:
- hardware limits
- expensive at large scale
- single machine dependency

---

## Horizontal Scaling

Add more servers to distribute traffic.

Example:

```txt
1 Server → Multiple Servers
```

Advantages:
- better scalability
- fault tolerance
- handles massive traffic

Challenge:
- clients now need to know:
  > which server to send requests to

This is solved using:

> Load Balancing

---

# 2. What is Load Balancing?

Load balancing means:
- distributing incoming traffic across multiple servers

Goals:
- prevent overload
- improve availability
- improve scalability
- reduce failures

---

# 3. Client-Side Load Balancing

In client-side load balancing:
- client decides which server to contact

Client usually:
- fetches list of servers
- chooses one server directly

Example flow:

```txt
Client → Service Registry → Server List
Client → Selected Server
```

---

## Advantages
- fast
- avoids extra network hop
- efficient routing

## Disadvantages
- clients must track server updates
- harder with millions of external clients

---

## Real Examples

### Redis Cluster
Client knows:
- cluster nodes
- shard locations

Client directly contacts correct node.

---

### DNS Load Balancing
DNS rotates IP addresses.

Different users receive:
- different server IPs

This naturally spreads traffic.

---

# 4. Dedicated Load Balancers

Instead of clients handling routing:
- dedicated load balancer sits between client and servers

Example:

```txt
Client → Load Balancer → Backend Servers
```

Advantages:
- centralized routing
- fast server updates
- easier management
- health monitoring

Tradeoff:
- extra network hop

---

# 5. Layer 4 (L4) Load Balancers

Operate at:
- Transport Layer (TCP/UDP)

Routing decisions based on:
- IP addresses
- ports

L4 does NOT inspect application data.

---

## Characteristics
- very fast
- efficient
- persistent TCP connections
- minimal packet inspection

---

## Best Use Cases
- WebSockets
- real-time communication
- high-performance networking

---

# 6. Layer 7 (L7) Load Balancers

Operate at:
- Application Layer

Can inspect:
- URLs
- headers
- cookies
- HTTP requests

---

## Characteristics
- smarter routing
- more flexible
- more CPU intensive
- creates new backend connections

---

## Best Use Cases
- HTTP traffic
- APIs
- websites
- content-based routing

---

# 7. L4 vs L7 Load Balancers

| Feature | L4 | L7 |
|---|---|---|
| Operates On | TCP/UDP | HTTP/Application |
| Speed | Faster | Slightly slower |
| Packet Inspection | No | Yes |
| Persistent Connections | Excellent | Limited |
| Best For | WebSockets | APIs/Websites |

---

# 8. Health Checks & Fault Tolerance

Load balancers continuously monitor server health.

If server crashes:
- traffic automatically stops routing there

This improves:
- availability
- reliability
- fault tolerance

---

## Types of Health Checks

### TCP Health Check
Checks:
- can server accept connections?

Fast and lightweight.

---

### HTTP Health Check
Makes HTTP request and checks:
- response status
- application health

Example:
```txt
200 OK → healthy
500 Error → unhealthy
```

---

# 9. Load Balancing Algorithms

Different algorithms distribute traffic differently.

---

## Round Robin
Requests distributed sequentially.

```txt
Server1 → Server2 → Server3
```

Simple and common.

---

## Random
Requests sent randomly.

---

## Least Connections
Send traffic to server with:
- fewest active connections

Great for:
- WebSockets
- long-lived connections

---

## Least Response Time
Traffic sent to:
- fastest responding server

---

## IP Hash
Client IP determines server.

Useful for:
- session persistence

---

# 10. Real-World Load Balancers

Examples:
- NGINX
- HAProxy
- Envoy
- AWS ELB / ALB / NLB
- Google Cloud Load Balancing

Large enterprises may also use:
- hardware load balancers

---

# 11. Regionalization & Latency

Global systems have servers distributed worldwide.

Problem:
- physical distance increases latency

Example:
- New York ↔ London requests naturally take longer

Because:
- network communication is limited by speed of light

---

# 12. Data Locality

Best performance happens when:
- computation stays close to data
- users stay close to servers

This reduces:
- network latency
- slow database queries

---

# 13. Content Delivery Networks (CDNs)

CDNs are globally distributed edge servers.

Purpose:
- cache frequently accessed content closer to users

Used for:
- images
- videos
- static assets
- cached search results

Benefits:
- lower latency
- reduced backend load
- faster user experience

---

# 14. Regional Partitioning

Large systems often partition data by geography.

Example:
- Uber users in Miami do not need drivers from New York

So systems create:
- regional databases
- regional services

Benefits:
- faster queries
- lower latency
- reduced cross-region traffic

---

# 15. Handling Failures in Distributed Systems

Networks are NOT perfectly reliable.

Possible failures:
- server crashes
- packet loss
- router failures
- network delays
- timeout issues

Distributed systems must expect failures.

---

# 16. Timeouts & Retries

If request takes too long:
- timeout occurs
- system retries request

Useful for:
- temporary/transient failures

---

# 17. Exponential Backoff

Retrying immediately can overload systems.

Instead:
- wait before retrying
- increase delay gradually

Example:

```txt
1s → 2s → 4s → 8s
```

Often combined with:
> jitter (random delay)

to avoid synchronized retry spikes.

---

# 18. Idempotency

Retries can be dangerous for operations like payments.

Example:
- retrying payment multiple times could double charge users

Solution:
> Idempotent APIs

Meaning:
- repeating same request produces same result

Common solution:
- idempotency keys

---

# 19. Circuit Breakers

Circuit breakers prevent:
- cascading failures

If service keeps failing:
- requests temporarily stop reaching it

Instead:
- fail fast
- allow service recovery

---

## Circuit Breaker Flow

### Closed State
Normal requests allowed.

### Open State
Requests blocked because failures exceeded threshold.

### Half-Open State
Small number of test requests allowed.

If successful:
- circuit closes again

---

## Benefits
- prevents system overload
- improves stability
- avoids retry storms
- helps failing services recover

---

# 20. Main Takeaways

Modern distributed systems depend heavily on:
- load balancing
- fault tolerance
- regional infrastructure
- retries and recovery patterns

Key concepts learned:
- horizontal scaling
- client-side vs dedicated load balancing
- L4 vs L7 load balancers
- CDNs
- regional partitioning
- retries & backoff
- idempotency
- circuit breakers

System design is not just about handling traffic.

It’s also about:
- surviving failures
- reducing latency
- maintaining reliability
- scaling efficiently under heavy load.
