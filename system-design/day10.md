# Sharding Deep Dive - Choosing a Shard Key

When implementing sharding, there are two important decisions:

1. **What to shard by** → The field/column used to split the data.
2. **How to distribute it** → The rule that determines which shard stores the data.

Together, these decisions determine how data is distributed across machines.

---

# Choosing a Shard Key

A shard key is the field used to decide where data lives.

In system design interviews, you'll often hear:

> "I will shard by user_id"

The important part is understanding **why** that field is a good choice.

A poor shard key can cause:

- Uneven data distribution
- Hotspots
- Slow queries
- Scalability issues

A good shard key should:

- Distribute data evenly
- Match common query patterns
- Scale as the system grows

---

# Characteristics of a Good Shard Key

## 1. High Cardinality

The shard key should have many unique values.

### Good Example

```text
user_id
```

Millions of users = millions of unique values.

Easy to distribute across many shards.

### Bad Example

```text
is_premium
```

Only two possible values:

```text
true
false
```

This limits you to only two groups and creates uneven distribution.

---

## 2. Even Distribution

Data should spread evenly across shards.

### Good Example

```text
user_id
```

Users are typically distributed randomly.

Example:

```text
Shard 1 → Users 1-250K
Shard 2 → Users 250K-500K
Shard 3 → Users 500K-750K
Shard 4 → Users 750K-1M
```

Balanced storage and traffic.

### Bad Example

```text
country
```

If:

```text
90% = USA
10% = Other Countries
```

Then:

```text
USA shard → overloaded
Other shards → mostly idle
```

This creates a hotspot.

---

## 3. Align With Query Patterns

Most queries should touch only one shard.

### Good Example

Sharding by:

```text
user_id
```

Queries:

```text
Get user profile
Get user's orders
Update user settings
```

All can be answered by a single shard.

Fast and efficient.

### Bad Example

If queries need to search every shard:

```text
Find all users created today
```

Database must perform scatter-gather operations across all shards.

This increases latency and cost.

---

# Good Shard Keys

## User ID

```text
user_id
```

Why it's good:

- High cardinality
- Even distribution
- Most queries are user-centric

Examples:

```text
Get profile
Get user orders
Get preferences
```

---

## Order ID

```text
order_id
```

Why it's good:

- Millions of unique values
- Naturally distributed
- Queries usually target a single order

Examples:

```text
Get order details
Update order status
Track order
```

---

# Bad Shard Keys

## Boolean Fields

```text
is_premium
```

Possible values:

```text
true
false
```

Problems:

- Only two groups
- Poor scalability
- Uneven traffic

---

## Timestamps

```text
created_at
```

Example:

```text
Orders created in January
Orders created in February
Orders created in March
```

Problem:

All new writes go to the newest shard.

Example:

```text
March shard → Heavy traffic
January shard → Almost idle
February shard → Almost idle
```

This creates a write hotspot.

---

# Hotspots

A hotspot occurs when one shard receives significantly more traffic than others.

Example:

```text
Shard 1 → 70% traffic
Shard 2 → 10% traffic
Shard 3 → 10% traffic
Shard 4 → 10% traffic
```

Result:

- Slow requests
- Higher latency
- Resource exhaustion

Even though other shards have capacity available.

---

> A good shard key has high cardinality, distributes data evenly across shards, aligns with common query patterns, and avoids hotspots. User IDs and Order IDs are common choices because they scale well and allow most queries to target a single shard.
