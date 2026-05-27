# Data Modeling Fundamentals for System Design

## What I Learned

Today I learned the fundamentals of:
- data modeling
- database design
- SQL vs NoSQL databases
- schema design
- normalization
- denormalization
- indexing
- sharding

Data modeling is one of the most important parts of system design because it defines:
> how application data is stored, structured, and accessed. 

---

# 1. What is Data Modeling?

Data modeling is the process of designing:
- entities
- relationships
- tables
- collections
- database structure

for an application.

It helps define:
- what data exists
- how data is connected
- how data is queried efficiently

---

# Example

For a social media app:

Main entities could be:
- Users
- Posts
- Comments
- Likes

These usually become:
> database tables or collections

---

# Why Data Modeling is Important

A good schema helps with:
- scalability
- performance
- consistency
- maintainability
- efficient querying

Bad schema design can cause:
- slow queries
- duplicate data
- scaling issues
- difficult maintenance

---

# 2. Database Model Options

Different applications use different database models.

The main database types learned today:

| Database Type | Best For |
|---|---|
| Relational Databases (SQL) | Structured applications |
| Document Databases | Flexible schemas |
| Key-Value Stores | Fast lookups & caching |
| Wide-Column Databases | Massive write-heavy systems |
| Graph Databases | Relationship-heavy systems |

---

# 3. Relational Databases (SQL)

Relational databases organize data into:
> tables with fixed schemas

Rows represent:
- entities

Columns represent:
- attributes

---

# Example Tables

## Users Table

| id | username | email |
|---|---|---|
| 1 | varshini | varshini@example.com |

---

## Posts Table

| id | user_id | content |
|---|---|---|
| 1 | 1 | Hello World |

---

# Key Concepts

- Primary Keys
- Foreign Keys
- Relationships
- ACID transactions
- Joins

---

# Why SQL is Commonly Preferred

SQL databases are great for:
- structured data
- relationships
- transactions
- strong consistency

Examples:
- PostgreSQL
- MySQL
- SQLite

---

# SQL Advantages

- strong consistency
- supports joins
- ACID guarantees
- easier relational querying

---

# Important Learning

Most system design interviews:
> default to SQL databases

unless requirements clearly need something else. 

---

# 4. Document Databases

Document databases store data as:
> JSON-like documents

instead of relational tables.

---

# Example

```json
{
  "username": "varshini",
  "posts": [
    {
      "content": "Hello World"
    }
  ]
}
```

---

# Key Idea

Related data is often:
> embedded together

instead of normalized across multiple tables.

---

# When Document DBs Are Useful

- flexible schema
- rapidly changing data structures
- nested JSON-style data

Examples:
- MongoDB
- Firestore
- CouchDB

---

# Tradeoff

Advantages:
- flexible schema
- easier nested storage

Disadvantages:
- harder consistency management
- data duplication
- limited joins

---

# 5. Key-Value Stores

Key-value databases store:
> value by exact key

Example:

```txt
user:1001 → user data
```

---

# Best Use Cases

- caching
- session storage
- feature flags
- high-speed lookups

Examples:
- Redis
- DynamoDB
- Memcached

---

# Key Learning

Usually used together with SQL.

Example:

```txt
Application
    ↓
Redis Cache
    ↓
PostgreSQL Database
```

Redis improves:
- read performance
- latency
- scalability

---

# 6. Wide-Column Databases

Wide-column databases are optimized for:
- massive write workloads
- time-series data
- analytics systems

Examples:
- Cassandra
- HBase

---

# Common Use Cases

- telemetry systems
- event logging
- IoT systems
- analytics platforms

---

# Key Learning

Data modeling focuses heavily on:
> query patterns

and time-based storage.

---

# 7. Graph Databases

Graph databases store:
- nodes
- edges
- relationships

Examples:
- Neo4j
- Amazon Neptune

---

# Common Use Cases

- recommendation systems
- social networks
- relationship-heavy data

---

# Important Interview Learning

Even graph-heavy companies often still use:
> SQL databases

for core systems.

Graph databases are usually unnecessary complexity for interviews.

---

# 8. Schema Design Fundamentals

Schema design should always depend on:

| Factor | Meaning |
|---|---|
| Data Volume | How much data exists |
| Access Patterns | How data is queried |
| Consistency Requirements | How strict data consistency must be |

These factors drive:
- indexing
- partitioning
- denormalization
- database selection

---

# 9. Entities, Keys & Relationships

Every entity needs:
> Primary Key

Example:

```txt
users.id
posts.id
```

Relationships connect entities together.

---

# Relationship Types

| Relationship | Example |
|---|---|
| One-to-Many | User → Posts |
| Many-to-Many | Users ↔ Likes |
| One-to-One | Rare |

---

# Example Schema

```txt
users:
id, username, email

posts:
id, user_id, content

comments:
id, post_id, user_id, content
```

---

# Primary Keys

Uniquely identify rows.

Example:

```txt
user_id
post_id
```

---

# Foreign Keys

Create relationships between tables.

Example:

```txt
posts.user_id → users.id
```

---

# Key Learning

Foreign keys help maintain:
> referential integrity

preventing invalid references.

---

# 10. Indexing

Indexes help databases:
> find records quickly

without scanning entire tables.

Similar to:
> book index

---

# Common Index Examples

```txt
INDEX posts(user_id)
INDEX posts(created_at)
INDEX (user_id, created_at)
```

---

# Why Indexing Matters

Indexes improve:
- query performance
- sorting speed
- filtering speed

---

# Important Learning

Indexes should support:
> major API query patterns

Example:

```txt
GET /users/{id}/posts
```

needs:
```txt
INDEX posts(user_id)
```

---

# 11. Normalization

Normalization means:
> storing data only once

to avoid duplication.

---

# Example

Instead of storing:
- username inside every post

store:
- user_id reference

---

# Benefits

- avoids duplicate data
- easier updates
- better consistency

---

# 12. Denormalization

Denormalization means:
> intentionally duplicating data

for performance optimization.

---

# Example

Store:
- username directly inside post record

to avoid expensive joins.

---

# Tradeoff

Advantages:
- faster reads
- fewer joins

Disadvantages:
- duplicate data
- harder consistency management

---

# Important Interview Learning

Start with:
> normalized schema

Only denormalize:
> when scaling/performance requires it.

---

# 13. Scaling and Sharding

When one database becomes too large:
> data is split across multiple machines

This is called:
> sharding

---

# Example

Shard by:

```txt
user_id
```

so one user's data stays together.

---

# Why Sharding Matters

Sharding improves:
- scalability
- write throughput
- storage distribution

---

# Important Learning

Bad shard keys can create:
> hot shards

where one database receives too much traffic.

---

# 14. Cross-Shard Queries

If related data exists on different shards:
- queries become slower
- system complexity increases

Good sharding tries to:
> minimize cross-shard communication

---

# Main Takeaways

- SQL is usually default choice
- schema should match query patterns
- indexing is critical for performance
- normalization improves consistency
- denormalization improves read speed
- sharding helps scale databases
