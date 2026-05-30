# Caching in System Design Interviews

## What I Learned

Caching is one of the most important topics in System Design because it helps:

- reduce latency
- reduce database load
- improve scalability
- handle high read traffic efficiently

A cache stores frequently accessed data in memory so applications can serve requests much faster than querying a database every time. 
---

# 1. When Should You Use Caching?

Do not immediately add caching to every design.

First identify a bottleneck.

Common scenarios:

### Read-Heavy Workloads

Example:

```txt
10M users
20 requests/user/day
= 200M reads/day
```

Database becomes overloaded serving repeated reads.

Cache can reduce latency from:

```txt
30-50ms → 1-2ms
```

---

### Expensive Queries

Example:

Computing a personalized feed requires:
- posts
- followers
- likes

across multiple tables.

Instead of recomputing every request:

```txt
Cache feed for 60 seconds
```

and serve instantly.

---

### High Database Load

Example:

```txt
Database CPU = 80%
```

because the same queries are repeatedly executed.

Caching frequently requested data dramatically reduces load.

---

### Strict Latency Requirements

If system requires:

```txt
< 10ms response time
```

but database queries take:

```txt
30-50ms
```

caching becomes necessary.

---

# 2. How to Introduce Caching in Interviews

A simple framework:

## Step 1 — Identify the Bottleneck

Example:

```txt
User profile requests are hitting database 500 times/sec.
Each query takes 30ms.
```

Clearly explain:
- what is slow
- why it is slow

---

## Step 2 — Decide What to Cache

Good candidates for caching:

- frequently read data
- expensive queries
- rarely changing data

Examples:

### User Profiles

```txt
user:123:profile
```

Read often, updated rarely.

---

### Trending Feed

```txt
trending:posts:global
```

Expensive computation but can tolerate slight staleness.

---

## Step 3 — Choose Cache Architecture

The most common interview answer:

### Cache-Aside Pattern

```txt
Application
      ↓
Check Redis
      ↓
Cache Hit → Return
      ↓
Cache Miss
      ↓
Database
      ↓
Store in Cache
      ↓
Return Response
```

Advantages:
- simple
- widely used
- efficient

---

### Other Patterns

#### Write Through

```txt
Application
    ↓
Cache
    ↓
Database
```

Pros:
- cache always fresh

Cons:
- slower writes

---

#### Write Behind

```txt
Application
    ↓
Cache
    ↓
Database (later)
```

Pros:
- extremely fast writes

Cons:
- risk of data loss

---

# 3. Cache Keys

Cache keys uniquely identify cached data.

Examples:

```txt
user:123:profile

post:456

trending:global
```

Good key design is critical for cache efficiency.

---

# 4. Eviction Policies

Caches have limited memory.

Eventually old data must be removed.

---

## LRU (Least Recently Used)

Removes:

```txt
Least Recently Accessed Item
```

Most common answer in interviews.

---

## LFU (Least Frequently Used)

Removes:

```txt
Least Frequently Accessed Item
```

Useful when certain keys remain popular.

---

## TTL (Time To Live)

Automatically expires data.

Example:

```txt
TTL = 10 minutes
```

Prevents stale data from remaining forever.

---

# 5. Cache Invalidation

One of the hardest problems in distributed systems.

Question:

> How do we keep cache and database synchronized?

---

## Common Solution

When data changes:

```txt
Update Database
      ↓
Delete Cache Entry
```

Next request reloads fresh data.

---

Example:

User updates profile.

```txt
Delete user:123:profile
```

Next request fetches updated data.

---

# 6. What Happens If Cache Fails?

Suppose Redis crashes.

Requests now hit database directly.

```txt
Application
      ↓
Database
```

Potential problem:

```txt
Database overload
```

---

## Common Solutions

### Circuit Breakers

Prevent overwhelming database.

---

### In-Process Cache

Keep small local cache inside application memory.

Acts as emergency backup layer.

---

# 7. Cache Stampede (Thundering Herd)

Occurs when:

```txt
Popular Cache Entry Expires
```

and thousands of requests simultaneously hit database.

---

Example:

```txt
Trending Feed Cache Expires
        ↓
10,000 Requests
        ↓
Database Overloaded
```

---

## Solutions

### Request Coalescing

Only one request rebuilds cache.

Other requests wait.

---

### Cache Warming

Refresh important cache entries before expiration.

---

# 8. Hot Keys

A hot key receives extremely high traffic.

Example:

```txt
user:taylor_swift
```

Millions of requests may hit a single Redis node.

---

## Solutions

### Replicate Hot Keys

Store same value across multiple nodes.

---

### Local Cache

Store frequently requested values in application memory.

---

### Rate Limiting

Prevent excessive traffic.

---

# 9. CDN Caching

Used for:

- images
- videos
- static assets

Architecture:

```txt
User
   ↓
CDN
   ↓
Origin Server
```

Examples:
- Cloudflare
- Akamai
- Fastly

Benefits:
- lower latency
- reduced server load
- global performance improvements

---

# 10. Main Takeaways

Caching should be introduced when:

- database becomes bottleneck
- latency is too high
- expensive queries are repeated
- read traffic dominates

Key concepts learned:

- Cache-Aside
- Write Through
- Write Behind
- Cache Keys
- TTL
- LRU
- LFU
- Cache Invalidation
- Cache Stampede
- Hot Keys
- CDN Caching

### Interview Strategy

Whenever you identify:

```txt
High Read Traffic
High Latency
Database Overload
```

Think:

```txt
Redis Cache
```

Then explain:

```txt
What to Cache
↓
Cache Pattern
↓
Eviction Policy
↓
Invalidation Strategy
↓
Failure Handling
```

This structured approach works extremely well in system design interviews.
