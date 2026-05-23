# Behind the Scenes of Uber Eats Orders Using Apache Kafka

## What I Learned

When we place an order on apps like Uber Eats, a lot happens within seconds:

- payment gets processed
- restaurant gets notified
- delivery partner gets assigned
- notifications are sent
- live tracking starts
- analytics systems update

Handling all of this reliably at massive scale is a distributed systems problem.

One important technology used in such systems is:

> Apache Kafka

---

# What is Apache Kafka?

Apache Kafka is a high-throughput event streaming platform used for communication between backend services.

Instead of every service directly calling every other service:

```txt
Order Service → Payment Service
             → Notification Service
             → Delivery Service
             → Analytics Service
```

systems often communicate through Kafka like this:

```txt
Order Service → Kafka → Multiple services consume events
```

This creates a more scalable and loosely coupled architecture.

---

# What Happens When an Order is Placed?

When the order is created:

The Order Service publishes an event like:

```json
{
  "event": "ORDER_CREATED",
  "orderId": 5001
}
```

Kafka stores this event inside something called a:

> Topic

Multiple backend services can then independently consume the same event.

For example:
- Payment Service processes payment
- Notification Service sends updates
- Delivery Service assigns a driver
- Analytics Service tracks metrics

All of this happens asynchronously.

---

# Why Event-Driven Architecture Matters

Because services communicate through events:
- systems scale better
- services don’t block each other
- failures stay isolated
- traffic spikes are easier to handle

This is one reason event-driven systems are widely used in large-scale applications.

---

# Kafka Offsets

Kafka stores messages safely using:

> Offsets

Offsets help services track:
- which messages were already processed
- where to continue reading after restart

So if a service crashes temporarily, it can restart later and continue processing without losing events.

---

# Where Kafka is Commonly Used

Kafka is heavily used in:
- food delivery platforms
- banking systems
- ride-sharing apps
- analytics pipelines
- recommendation systems
- real-time platforms

Companies like Uber, Netflix, and LinkedIn use Kafka at massive scale to process millions of real-time events every second.

---

# Main Takeaway

Modern backend systems rely heavily on asynchronous event-driven communication.

Technologies like Kafka help distributed systems become:
- scalable
- fault tolerant
- loosely coupled
- reliable under heavy traffic

Backend engineering becomes much more interesting once you start understanding what happens behind the scenes of everyday applications.
