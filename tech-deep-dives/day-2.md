# Behind the Scenes of WhatsApp’s Double Tick

When we send a message on WhatsApp, most of us only notice the small ticks:

- sending...
- single gray tick
- double gray tick

But behind these tiny icons, a lot happens in real time.

---

# Step 1 — You Type and Hit Send

When you press send:

- your phone creates a message packet
- the message gets encrypted
- WhatsApp sends it to their servers through the internet

At this point:
- your phone acts as the client
- WhatsApp backend acts as the server

---

# Step 2 — Single Gray Tick

A single gray tick means:

> “WhatsApp servers successfully received your message.”

It does NOT mean:
- the other person saw the message
- the other person is online
- the message reached their phone

It only confirms:
- the message safely reached WhatsApp servers

Simple analogy:
> Your package reached the courier warehouse.

---

# Step 3 — Why It Sometimes Stays on One Tick

Sometimes the message stays on a single tick for a few seconds because:

- receiver has no internet connection
- their phone is turned off
- poor network connectivity
- WhatsApp is restricted in the background
- temporary network/server delays

During this time:
WhatsApp servers temporarily store the message and wait for the receiver to reconnect.

---

# Step 4 — Double Gray Tick

The second tick appears when:

> The receiver’s phone successfully receives the message.

Now the message has:
- left WhatsApp servers
- reached the other device

But:
- the person may still not have opened the chat yet

Simple analogy:

> The package reached the person’s house.

---

# The Interesting Part — How Is This So Fast?

This is where WebSockets become important.

---

# What Are WebSockets?

In traditional web apps, the app repeatedly asks:

```txt
"Any new message?"
"Any new message?"
"Any new message?"
```

This approach is called:

> Polling

Polling is inefficient because the app keeps sending repeated requests.

Instead, WhatsApp uses:

> WebSockets

A WebSocket creates:
- one long-lived connection
- between your phone and WhatsApp servers

Instead of reconnecting repeatedly, the connection stays open continuously.

This allows messages to be pushed instantly in real time.

---

# Simple Analogy

Without WebSockets:

> Like repeatedly calling your friend asking:
> “Anything new?”

With WebSockets:

> Like staying on an active phone call continuously.

This is why:
- messages arrive instantly
- typing indicators update live
- online status changes quickly
- double ticks update in real time

---

# Simplified Message Flow

```txt
User A → WhatsApp Server → User B
```

1. User A sends message
2. Server receives it → single tick
3. Server pushes message to User B through WebSocket
4. User B receives it → double tick
5. User B opens chat → blue tick

---

# Why WebSockets Matter

WebSockets are heavily used in:
- WhatsApp
- Discord
- Slack
- Uber live tracking
- stock trading apps
- multiplayer games
- live notifications

Because they provide:
- low latency
- real-time communication
- fewer repeated HTTP requests
- efficient persistent connections

---

# Small Technical Insight

Under the hood:

- WebSockets start with an HTTP handshake
- then upgrade to a persistent TCP connection

After that:
- both client and server can send data anytime

This is called:

> Full-duplex communication

Meaning:
- both sides can communicate simultaneously

---

# What Makes WhatsApp Engineering Interesting?

Even a simple double tick involves:
- distributed servers
- message queues
- encryption
- persistent socket connections
- delivery acknowledgements
- retry mechanisms
- offline message storage
- massive scalability

That tiny double tick is actually a large distributed systems problem being solved in milliseconds.
