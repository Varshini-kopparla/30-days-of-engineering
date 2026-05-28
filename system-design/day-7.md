# Caching Fundamentals for System Design

## What I Learned

Today I learned the fundamentals of:
- caching
- Redis
- CDN caching
- cache architectures
- cache eviction policies
- cache consistency
- cache stampede
- hot keys

Caching is one of the most important concepts in system design because it helps systems:
- reduce latency
- reduce database load
- improve scalability
- handle massive read traffic efficiently.

---

# 1. Why Caching is Important

Databases are slower because:
- data is stored on disk

Caches are much faster because:
- data is stored in memory (RAM)

Example:
- PostgreSQL query → ~50ms
- Redis cache lookup → ~1ms

This can improve latency by:
> 50x or more

---

# Main Benefits of Caching

- faster responses
- lower database load
- better scalability
- reduced latency
- improved user experience

---

# 2. Where Caching Happens

Caching can exist at multiple layers of a system.

---

# External Cache (Most Important)

Most common interview answer.

Architecture:

```txt
Application
     ↓
Redis Cache
     ↓
Database
```

Application first checks cache:
- if data exists → return immediately
- otherwise → fetch from DB

Examples:
- Redis
- Memcached

---

# Why External Caching is Popular

- shared across servers
- scalable
- centralized caching
- supports TTL & eviction policies

---

# 3. CDN (Content Delivery Network)

CDNs cache content:
> close to users geographically

Used mainly for:
- images
- videos
- static assets
- media files

Examples:
- Cloudflare
- Fastly
- Akamai

---

# CDN Flow

```txt
User
   ↓
Nearest CDN Edge Server
   ↓
Origin Server (if cache miss)
```

---

# Why CDN Matters

Without CDN:
- request travels far distance

With CDN:
- nearby edge server responds quickly

This dramatically reduces:
- latency
- origin server traffic

---

# 4. Client-Side Caching

Caching on:
- browser
- mobile app
- local storage
- device memory

Examples:
- browser image cache
- offline mobile app data
- localStorage

---

# Benefits

- avoids repeated API calls
- improves app speed
- supports offline access

---

# Limitation

Harder to:
- invalidate stale data
- synchronize updates

---

# 5. In-Process Caching

Cache stored directly inside:
> application memory

Example:
- configuration values
- feature flags
- hot frequently-used data

---

# Architecture

```txt
Application Memory Cache
        ↓
Redis
        ↓
Database
```

---

# Advantages

- extremely fast
- no network calls

---

# Limitations

Each application server has:
> separate local cache

Data is NOT shared automatically across servers.

---

# 6. Cache-Aside (Most Important Pattern)

Most common caching strategy.

---

# Flow

```txt
Application
     ↓
Check Cache
     ↓
Cache Hit → Return Data
     ↓
Cache Miss
     ↓
Fetch From Database
     ↓
Store In Cache
     ↓
Return Response
```

---

# Why Cache-Aside is Popular

- simple
- efficient
- cache stores only useful data
- commonly used with Redis

---

# Important Learning

In interviews:
> Cache-Aside should usually be your default answer.

---

# 7. Write-Through Cache

Application writes:
- cache
- database

at the same time.

---

# Flow

```txt
Application
    ↓
Cache
    ↓
Database
```

Write completes only after:
- both cache and DB succeed

---

# Advantages

- cache always fresh

---

# Disadvantages

- slower writes
- more complexity
- consistency issues possible

---

# 8. Write-Behind (Write-Back)

Application writes only to:
> cache

Cache asynchronously updates database later.

---

# Advantages

- extremely fast writes
- high throughput

---

# Disadvantages

If cache crashes before DB write:
> data loss may happen

---

# Common Use Cases

- analytics
- metrics pipelines
- logging systems

where occasional data loss is acceptable.

---

# 9. Read-Through Cache

Application talks only to:
> cache layer

Cache itself fetches missing data from DB.

---

# Flow

```txt
Application
    ↓
Cache
    ↓
Database
```

---

# Important Learning

Less common than:
> Cache-Aside

Usually seen in:
- CDNs
- specialized caching systems

---

# 10. Cache Eviction Policies

Caches have limited memory.

Eviction policies decide:
> what data gets removed

when cache becomes full.

---

# LRU (Least Recently Used)

Removes:
> least recently accessed item

Most common eviction policy.

---

# LFU (Least Frequently Used)

Removes:
> least frequently accessed item

Useful when:
- some keys stay popular consistently

---

# FIFO (First In First Out)

Removes:
> oldest inserted item

Simple but less efficient.

---

# TTL (Time To Live)

Cache entries expire automatically after:
> fixed time

Example:

```txt
TTL = 60 seconds
```

Commonly used with:
- Redis
- API caching
- sessions

---

# 11. Cache Stampede (Thundering Herd)

Happens when:
- popular cache entry expires
- many requests hit database simultaneously

This can overload database suddenly.

---

# Example

```txt
Popular Feed Cache Expires
        ↓
Thousands of Requests Miss Cache
        ↓
Database Overloaded
```

---

# Solutions

## Request Coalescing

Allow:
> only one request

to rebuild cache while others wait.

---

## Cache Warming

Refresh important cache entries:
> before expiration

---

# 12. Cache Consistency Problem

Cache and database may contain:
> different values temporarily

Example:
- user updates profile picture
- DB updated
- cache still has old image

Users may see stale data.

---

# Common Solutions

## Cache Invalidation

Delete cache after DB update.

Next request reloads fresh data.

---

## Short TTL

Allow temporary stale data.

Useful for:
- feeds
- analytics
- metrics

---

## Eventual Consistency

Accept small delays between:
- DB updates
- cache refresh

---

# 13. Hot Keys

A hot key receives:
> extremely high traffic

Example:

```txt
user:taylor_swift
```

Millions of requests hitting one Redis key can overload one cache node.

---

# Solutions

## Replicate Hot Keys

Store same value on:
- multiple cache nodes

---

## Local In-Process Cache

Store extremely hot data:
- directly in application memory

---

## Rate Limiting

Prevent abusive traffic patterns.

---

# 14. Real-World Cache Architecture

Modern systems often combine multiple cache layers.

Example:

```txt
User
   ↓
Browser Cache
   ↓
CDN
   ↓
Application
   ↓
Redis Cache
   ↓
Database
```

This dramatically reduces:
- latency
- backend traffic
- database pressure

---

# Main Takeaways

Key understanding:
- Redis is default interview cache
- cache-aside is most common strategy
- caching improves performance dramatically
- consistency becomes harder with caching
- CDN helps reduce global latency
