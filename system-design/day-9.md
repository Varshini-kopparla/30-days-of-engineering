# Sharding & Partitioning

Your app is taking off. Traffic is growing, users are signing up, and your database keeps getting bigger.

At first, you can solve this by upgrading to a larger database instance with more CPU, memory, and storage (vertical scaling). Eventually, however, a single machine reaches its limits:

- Queries become slow
- Writes become a bottleneck
- Storage approaches its maximum capacity

When a single database can no longer keep up, the solution is to split data across multiple machines.

This is called **Sharding**.

---

## Partitioning vs Sharding

People often use these terms interchangeably, but there is a difference:

### Partitioning
Splitting data within a single database instance.

### Sharding
Splitting data across multiple database machines.

In practice, many engineers use the terms loosely, so focus on understanding whether the data lives on one machine or many.

---

# What is Partitioning?

Partitioning means splitting a large table into smaller pieces inside a single database instance.

It does **not** add more machines. Instead, it organizes data so the database can manage and query data more efficiently.

### Example

Suppose we have an Orders table:

- 500 million rows
- 2 TB of data

Without partitioning:

- Queries may scan huge amounts of data
- Indexes become very large
- Maintenance operations become slower

With partitioning:

- Data is divided into smaller partitions
- Queries only scan relevant partitions
- Indexes are smaller and easier to maintain

### Benefits

- Faster queries
- Smaller indexes
- Easier maintenance
- Better database performance

---

## Types of Partitioning

### 1. Horizontal Partitioning

Split rows across partitions.

Example:

- Orders_2023
- Orders_2024
- Orders_2025

Characteristics:

- Same columns
- Different rows

Think: **Split by rows**

---

### 2. Vertical Partitioning

Split columns across partitions.

Example:

Frequently used columns:

- Order ID
- Customer Name
- Product

Rarely used columns:

- Large Notes
- Metadata

Characteristics:

- Same rows
- Different columns

Think: **Split by columns**

---

# What is Sharding?

Sharding is horizontal partitioning across multiple machines.

Each shard stores a subset of the data, and together all shards represent the complete dataset.

Unlike partitioning, sharding distributes data across multiple independent databases.

### Example

Shard 1:

- Order IDs 1 – 1,000,000

Shard 2:

- Order IDs 1,000,001 – 2,000,000

Shard 3:

- Order IDs 2,000,001 – 3,000,000

Each shard is a separate database with its own:

- CPU
- Memory
- Storage
- Connection pool

No single machine stores all data or handles all traffic.

---

## Benefits of Sharding

### 1. Increased Storage Capacity

Data is distributed across multiple machines.

### 2. Higher Read Throughput

Read traffic is spread across shards.

### 3. Higher Write Throughput

Writes are distributed rather than hitting one database.

### 4. Horizontal Scalability

Instead of buying a bigger server, we can add more database servers.

---

# Challenges of Sharding

While sharding solves scaling problems, it introduces new challenges.

### 1. Choosing a Shard Key

A shard key determines where data is stored.

Example:

```text
user_id % 4
```

The result determines which shard stores the data.

---

### 2. Query Routing

The application must know which shard contains the required data.

Example:

```text
12345 % 4 = 1
```

Query is sent to Shard 1.

---

### 3. Hotspots

Some shards may receive significantly more traffic than others.

This causes:

- Uneven load distribution
- Performance bottlenecks

---

### 4. Rebalancing

As data grows:

- Some shards become larger than others
- New shards may need to be added
- Data may need to be moved between shards

This process is called rebalancing.

## One-Line Definition

**Sharding is the process of horizontally partitioning data across multiple database servers so that storage and traffic can scale beyond the limits of a single machine.**
