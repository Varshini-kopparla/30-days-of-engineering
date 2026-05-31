# DynamoDB

## What is DynamoDB?

DynamoDB is AWS's fully managed NoSQL database service.

Unlike relational databases such as MySQL or PostgreSQL, DynamoDB stores data as key-value pairs and documents rather than tables with fixed schemas.

AWS manages:

- Servers
- Scaling
- Replication
- Backups
- Availability

This allows developers to focus on building applications instead of managing database infrastructure.

---

## Why DynamoDB?

Traditional databases often require:

- Capacity planning
- Manual scaling
- Maintenance
- Performance tuning

DynamoDB automatically scales to handle large workloads while maintaining low latency.

### Benefits

- Fully managed
- Serverless
- High availability
- Automatic scaling
- Single-digit millisecond latency

---

## DynamoDB vs Relational Databases

| Feature | DynamoDB | MySQL/PostgreSQL |
|----------|----------|------------------|
| Type | NoSQL | Relational |
| Schema | Flexible | Fixed |
| Scaling | Horizontal | Mostly Vertical |
| Joins | Not Supported | Supported |
| Performance | Very Fast | Query Dependent |
| Infrastructure | Managed by AWS | Managed by User/Cloud |

---

# Core Concepts

## 1. Table

Data is stored in tables.

Example:

```text
Users
```

---

## 2. Item

An item is equivalent to a row in a relational database.

Example:

```json
{
  "UserId": "101",
  "Name": "Varshini",
  "Role": "Developer"
}
```

---

## 3. Attribute

Attributes are equivalent to columns.

Example:

```text
UserId
Name
Role
```

---

## 4. Primary Key

Every DynamoDB table must have a primary key.

### Partition Key

A single unique identifier.

Example:

```text
UserId
```

AWS uses this value to determine where data is stored.

---

### Composite Key

Combination of:

```text
Partition Key + Sort Key
```

Example:

```text
UserId + Timestamp
```

Useful when storing multiple records for the same user.

---

# Partition Key

The partition key is the most important design decision in DynamoDB.

Example:

```text
UserId = 101
```

DynamoDB hashes the partition key and determines which partition stores the item.

### Good Partition Key

```text
UserId
```

Provides even data distribution.

### Bad Partition Key

```text
Country = USA
```

Can create hotspots if most traffic goes to the same partition.

---

# Secondary Indexes

Indexes allow querying data using attributes other than the primary key.

## Global Secondary Index (GSI)

Example:

Primary Key:

```text
UserId
```

GSI:

```text
Email
```

Now users can be searched using email addresses.

---

# Capacity Modes

## Provisioned Mode

You specify read and write capacity beforehand.

Example:

```text
1000 reads/sec
500 writes/sec
```

Best for predictable workloads.

---

## On-Demand Mode

AWS automatically scales based on traffic.

Best for:

- Startups
- Variable workloads
- Unpredictable traffic patterns

---

# Consistency Models

## Eventually Consistent Reads

Default mode.

Recent writes may take a short time to appear.

Advantages:

- Faster
- Cheaper

---

## Strongly Consistent Reads

Always returns the latest data.

Advantages:

- Most accurate

Disadvantages:

- Higher latency
- Higher cost

---

# Real-World Use Cases

### User Profiles

```text
UserId → Profile Data
```

### Shopping Carts

```text
UserId → Cart Items
```

### Session Management

```text
SessionId → Session Data
```

### Gaming Applications

```text
PlayerId → Game Statistics
```

### IoT Applications

```text
DeviceId → Sensor Data
```

---

# DynamoDB in My Experience

At the UF Marketing Analytics Lab, I used DynamoDB alongside AWS Lambda and FastAPI for campaign validation workflows.

Architecture:

```text
User Request
      ↓
FastAPI
      ↓
AWS Lambda
      ↓
DynamoDB
      ↓
Validation Results
```

Why DynamoDB?

- Fast lookups
- Serverless architecture
- Automatic scaling
- Seamless AWS integration

This helped process large campaign datasets while maintaining low response times.

---

# Advantages

- Fully managed by AWS
- Automatic scaling
- High availability
- Low latency
- Serverless
- Easy integration with Lambda

---

# Limitations

- No joins
- Query patterns must be designed upfront
- Poor partition key choices can cause hotspots
- Complex relationships are harder than in relational databases

