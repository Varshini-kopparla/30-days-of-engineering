# AWS Lambda Fundamentals

## What I Learned

Today I learned about AWS Lambda, one of the most commonly used serverless services in AWS.

Lambda allows developers to run code without managing servers, making it ideal for:
- event-driven applications
- REST APIs
- microservices
- automation workflows

---

# 1. What is AWS Lambda?

AWS Lambda is a:

> Serverless Compute Service

It executes code in response to events without requiring developers to manage servers.

Instead of:

```txt
Create Server
Install Software
Maintain Server
Scale Server
```

AWS handles everything automatically.

Developers only focus on:
> Writing Business Logic

---

# 2. Why Use Lambda?

## Traditional Server (EC2)

```txt
User Request
      ↓
EC2 Server Running 24/7
      ↓
Execute Code
```

Even when no users are active:
- server remains running
- infrastructure costs continue

---

## AWS Lambda

```txt
User Request
      ↓
Lambda Triggered
      ↓
Code Executes
      ↓
Stops
```

Benefits:
- no idle servers
- pay only when code runs
- automatic scaling

---

# 3. Key Features

## Serverless

No infrastructure management.

AWS manages:
- servers
- operating systems
- scaling
- availability

---

## Auto Scaling

If:

```txt
10 users
```

Lambda creates enough instances.

If:

```txt
10,000 users
```

Lambda automatically scales further.

No manual intervention required.

---

## Pay Per Use

Charges are based on:
- number of executions
- execution duration

No charges when function is idle.

---

## Event Driven

Lambda runs only when an event occurs.

Examples:
- API request
- file upload
- database update
- scheduled task

---

# 4. How Lambda Works

Basic flow:

```txt
Event
   ↓
Lambda
   ↓
Result
```

Example:

```txt
File Uploaded to S3
        ↓
Lambda Triggered
        ↓
Process File
        ↓
Store Result
```

---

# 5. Common Lambda Triggers

## API Gateway

Used for REST APIs.

```txt
Frontend
   ↓
API Gateway
   ↓
Lambda
```

---

## S3

File upload events.

```txt
File Upload
    ↓
Lambda
```

---

## DynamoDB

Database events.

```txt
Record Inserted
     ↓
Lambda
```

---

## EventBridge

Scheduled jobs.

Example:

```txt
Every Day 9 AM
      ↓
Lambda
```

---

## SQS

Queue processing.

```txt
Message Queue
      ↓
Lambda
```

---

# 6. Lambda + API Flow

One of the most common serverless architectures.

```txt
Frontend
   ↓
API Gateway
   ↓
Lambda
   ↓
DynamoDB
   ↓
Response
```

Example:

```txt
User submits campaign
        ↓
API Gateway receives request
        ↓
Lambda validates request
        ↓
Reads/Writes DynamoDB
        ↓
Returns response
```

---

# 7. Real Example From My Experience

In the UF Marketing Analytics Lab project, we used AWS Lambda to process campaign validation and decisioning workflows.

Flow:

```txt
Campaign Data Arrives
        ↓
Lambda Triggered
        ↓
Validation Logic Executes
        ↓
Data Stored in DynamoDB
        ↓
Files Stored in S3
```

Benefits:
- no server management
- automatic scaling
- cost-efficient processing

---

# 8. Lambda vs EC2

| Feature | Lambda | EC2 |
|----------|----------|----------|
| Type | Serverless | Virtual Server |
| Scaling | Automatic | Manual |
| Pricing | Pay Per Request | Pay While Running |
| Infrastructure | Managed by AWS | Managed by Developer |
| Best For | Event-Driven Apps | Long-Running Applications |

---

# 9. When Should You Use Lambda?

Lambda works best for:

### Event-Driven Systems

Examples:
- file processing
- notifications
- workflow automation

---

### REST APIs

Small backend services.

---

### Microservices

Independent services that scale separately.

---

### Scheduled Tasks

Cron jobs and recurring workflows.

---

# 10. When NOT To Use Lambda

Lambda is not ideal for:

### Long Running Jobs

Examples:
- video rendering
- heavy batch processing
- hours-long computations

---

### Heavy Continuous Workloads

Always-running applications are usually better on:
- EC2
- ECS
- Kubernetes

---

### Full Server Control Requirements

If you need:
- custom OS configuration
- direct server access

use EC2 instead.

---

# 11. Cold Start vs Warm Start

A very common interview question.

---

## Cold Start

If Lambda hasn't been used recently:

```txt
Request Arrives
      ↓
AWS Creates Execution Environment
      ↓
Function Starts
```

This startup delay is called:

> Cold Start

---

## Warm Start

Lambda environment already exists.

```txt
Request Arrives
      ↓
Execute Immediately
```

Much faster response time.

---

# 12. Lambda Execution Flow

```txt
Event Arrives
      ↓
AWS Invokes Lambda
      ↓
Runtime Starts
      ↓
Function Executes
      ↓
Result Returned
      ↓
Resources Released
```

---

# 13. Lambda in Microservices

A common serverless architecture:

```txt
User Service
Order Service
Payment Service
Notification Service
```

Each service can have its own Lambda function.

Benefits:
- independent deployment
- automatic scaling
- lower operational overhead

---

# 14. AWS Services Commonly Used with Lambda

## API Gateway

Expose REST APIs.

---

## DynamoDB

NoSQL database.

Lambda reads and writes data.

---

## S3

Object storage.

Examples:
- CSV files
- images
- documents

---

## CloudWatch

Monitoring and logging.

---

## SQS

Message queue processing.

---

# Common Interview Questions

### Why Lambda instead of EC2?

Lambda removes server management, automatically scales, and reduces costs because you only pay when code executes.

---

### How does Lambda scale?

AWS automatically creates additional Lambda instances as request volume increases.

---

### What triggers Lambda?

Examples:
- API Gateway
- S3 uploads
- DynamoDB events
- SQS messages
- EventBridge schedules

---

### What is Serverless?

Serverless means developers do not manage servers directly. AWS handles infrastructure, scaling, and availability while developers focus on application logic.

---

# Main Takeaways

AWS Lambda is a serverless compute service that executes code in response to events.

Key concepts learned:
- Serverless Architecture
- Event-Driven Systems
- API Gateway Integration
- DynamoDB Integration
- Auto Scaling
- Pay Per Use
- Cold Starts
- Microservices

Lambda is especially useful for:
- APIs
- microservices
- automation workflows
- event-driven applications
- cloud-native systems

Understanding Lambda is important for:
- backend engineering
- cloud computing
- AWS interviews
- modern distributed systems
