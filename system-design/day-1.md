# Networking Basics for System Design

## What I Learned

Networking fundamentals are extremely important for system design because every distributed system depends on computers communicating efficiently over a network.

---

# 1. What is Networking?

Networking simply means:

> Different computers communicating with each other.

Examples:
- opening a website
- sending API requests
- watching YouTube
- online gaming
- using WhatsApp

All of these involve devices exchanging data over a network.

---

# 2. What is the Internet?

The internet is a massive network of connected computers.

Every device connected to the internet gets an identity called an:

> IP Address

Example: 142.250.190.78

Without IP addresses, computers wouldn’t know where to send data.

---

# 3. DNS (Domain Name System)

Humans remember names like: google.com

But computers communicate using IP addresses.

DNS converts: google.com → 142.250.190.78

---

# 4. What Happens When You Open a Website?

When you type: google.com

multiple things happen behind the scenes.

### Step 1 — DNS Lookup
Browser finds the server’s IP address.

### Step 2 — Connection Setup
Your device connects to the server.

### Step 3 — HTTP Request
Browser sends a request like: GET /home

### Step 4 — Server Processing
Server:
- processes request
- fetches data
- queries database if needed

### Step 5 — HTTP Response
Server returns:
- HTML
- CSS
- JSON
- images
- other assets

Browser then renders the webpage.

---

# 5. Networking Layers

Networking is divided into layers to keep responsibilities organized.

The 3 most important layers for system design are:

| Layer | Responsibility |
|---|---|
| Network Layer | Routing packets |
| Transport Layer | Reliable communication | 
| Application Layer | HTTP, DNS, WebSockets |

---

# 6. Network Layer (IP)

The main protocol here is:

> IP (Internet Protocol)

Responsibilities:
- assigning addresses
- routing packets
- sending packets across networks

---

## What is a Packet?

Data is broken into small chunks called:

> Packets

Instead of sending huge data all at once:
- data is split into packets
- packets travel independently
- destination rebuilds original data

---

## Limitation of IP

IP only handles:
- addressing
- routing

It does NOT guarantee:
- delivery
- ordering
- reliability

That responsibility belongs to the transport layer.

---

# 7. Transport Layer

This layer handles communication between applications.

Main protocols:
- TCP
- UDP
- QUIC

---

# 8. TCP (Transmission Control Protocol)

TCP is:

> Reliable but slower.

Most websites and APIs use TCP.

---

## TCP Features

### Reliable Delivery
Ensures data reaches destination.

### Ordering
Packets arrive in correct order.

Correct: 1 → 2 → 3

Not: 3 → 1 → 2

### Error Checking
Detects corrupted or missing data.

### Retransmission
Lost packets are automatically resent.

---

## TCP Three-Way Handshake

Before communication begins: SYN → SYN-ACK → ACK

Purpose:
- confirm both systems are ready
- establish reliable connection

---

## TCP Use Cases

Used in:
- websites
- REST APIs
- databases
- banking systems
- file uploads

Basically:
> whenever reliability matters.

---

# 9. UDP (User Datagram Protocol)

UDP is:

> Fast but unreliable.

---

## UDP Features

### No Connection Setup
Data is sent immediately.

### No Guaranteed Delivery
Packets may be lost.

### No Ordering
Packets may arrive randomly.

### Low Latency
Very fast because there’s very little overhead.

---

## Why Use UDP?

Sometimes speed matters more than perfect reliability.

Example:
In video calls, losing one audio packet is acceptable.

Waiting for retransmission would create lag.

---

## UDP Use Cases

Used in:
- gaming
- live streaming
- video calls
- VoIP
- DNS

---

# TCP vs UDP

| TCP | UDP |
|---|---|
| Reliable | Faster |
| Ordered | Unordered |
| Connection-oriented | Connectionless |
| Higher overhead | Lightweight |
| Websites/APIs | Streaming/Gaming |

---

# 10. HTTP

HTTP is the protocol browsers use to communicate with servers.

Example: GET /users

HTTP works on top of TCP.

Used for:
- websites
- APIs
- frontend-backend communication

---

# 11. HTTPS

HTTPS = Secure HTTP

Adds:
- encryption
- security
- authentication

Protects:
- passwords
- payments
- personal data

Most modern websites use HTTPS.

---

# 12. Ports

Ports help identify which application should receive data.

Examples:
- Port 80 → HTTP
- Port 443 → HTTPS

Analogy:
- IP address = apartment building
- Port = apartment number

---

# 13. Latency

Latency means:

> Delay in communication.

Caused by:
- DNS lookup
- network travel
- TCP handshake
- server processing

Reducing latency is a major goal in system design.

---

# 14. Persistent Connections

Creating new TCP connections repeatedly is expensive.

Modern systems improve performance using:
- HTTP Keep-Alive
- HTTP/2 multiplexing

This allows:
- reusing connections
- multiple requests over the same connection

---

# 15. WebSockets

Normal HTTP: Request → Response → Close

WebSockets: Persistent two-way connection

Used for:
- chats
- live notifications
- stock updates
- multiplayer games

---

# 16. QUIC and HTTP/3

Modern protocols designed for:
- lower latency
- faster connection setup
- improved performance

QUIC:
- built on UDP
- adds TCP-like reliability
- reduces handshake overhead

Used heavily in modern browsers and large-scale systems.

---

# Key System Design Takeaways

## Use TCP When:
- reliability matters
- building APIs/websites/databases

## Use UDP When:
- real-time speed matters
- small packet loss is acceptable

Networking directly affects:
- scalability
- latency
- reliability
- system performance

Understanding networking fundamentals helps build better distributed systems.

---

# Final Understanding

The internet works because multiple networking layers work together: DNS → IP → TCP/UDP → HTTP/WebSockets

Each layer solves a specific problem:
- DNS finds servers
- IP routes packets
- TCP/UDP handles communication
- HTTP/WebSockets power applications

These networking fundamentals form the foundation of backend engineering and system design.
