# 🌐 TCP & UDP

> **Understanding how devices transport data across a network — reliably, quickly, and efficiently.**

---

## 🧠 What are TCP and UDP?

**TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are transport-layer protocols used to deliver data between applications over a network.

They operate at **Layer 4 — Transport Layer** of the OSI Model.

```text
Application
     ↓
Transport        ← TCP / UDP
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

Their main difference is how they handle data delivery.

```text
TCP → Reliable + Connection-oriented
UDP → Fast + Connectionless
```

---

# 🔗 TCP — Transmission Control Protocol

TCP is designed for **reliable communication**.

It establishes a connection between two endpoints before transferring data.

```text
Client
   │
   │ Establish connection
   ▼
Server
   │
   │ Reliable communication
   ▼
Data Transfer
```

TCP provides mechanisms for:

- Reliable delivery
- Ordering
- Error detection
- Retransmission
- Flow control
- Congestion control

---

# 🤝 TCP Connection

TCP uses a process called the **Three-Way Handshake** to establish a connection.

```text
SYN
Client ─────────────────► Server

SYN-ACK
Client ◄───────────────── Server

ACK
Client ─────────────────► Server
```

After this process, the connection can be established.

---

# 🔄 TCP Three-Way Handshake

## 1️⃣ SYN

The client sends a **SYN** packet to request a connection.

```text
Client
  │
  │ SYN
  ▼
Server
```

---

## 2️⃣ SYN-ACK

The server responds with **SYN-ACK**.

```text
Client
  ▲
  │ SYN-ACK
  │
Server
```

---

## 3️⃣ ACK

The client sends an **ACK**.

```text
Client
  │
  │ ACK
  ▼
Server
```

The TCP connection is now established.

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
 ↓
Connection Established
```

---

# 📦 TCP Reliability

TCP ensures that data can be delivered reliably.

Imagine sending:

```text
Packet 1
Packet 2
Packet 3
Packet 4
```

If Packet 3 is lost:

```text
Packet 1 → ✅
Packet 2 → ✅
Packet 3 → ❌
Packet 4 → ✅
```

TCP can detect the missing data and retransmit it.

This makes TCP suitable when data must arrive correctly.

---

# 🔢 Sequence Numbers

TCP uses sequence numbers to help keep data in the correct order.

For example:

```text
Packet 1
Packet 2
Packet 3
Packet 4
```

If packets arrive out of order:

```text
1 → 3 → 2 → 4
```

TCP can use sequence information to reconstruct the correct data stream.

```text
1 → 2 → 3 → 4
```

---

# 📥 Acknowledgements

TCP uses acknowledgements to confirm that data has been received.

Conceptually:

```text
Client
  │
  │ Data
  ▼
Server
  │
  │ ACK
  ▼
Client
```

If expected acknowledgements do not arrive, TCP can retransmit data.

---

# 🚦 TCP Flow Control

TCP includes **flow control** to prevent a sender from overwhelming the receiver.

```text
Fast Sender
     │
     ▼
Slow Receiver
```

Without flow control, the receiver could become overloaded.

TCP uses a **receive window** to communicate how much data the receiver can currently handle.

---

# 🚥 TCP Congestion Control

TCP also manages network congestion.

If a network becomes overloaded, TCP can reduce the sending rate.

Conceptually:

```text
Normal Network
      ↓
Higher Sending Rate

Congested Network
      ↓
Reduced Sending Rate
```

This helps TCP adapt to changing network conditions.

---

# 🔚 TCP Connection Termination

TCP connections can also be closed gracefully.

A simplified example:

```text
FIN
Client ─────────────────► Server

ACK
Client ◄───────────────── Server

FIN
Client ◄───────────────── Server

ACK
Client ─────────────────► Server
```

This is commonly described as a **four-step connection termination process**, although the exact packet exchange can vary.

---

# ⚡ UDP — User Datagram Protocol

UDP is a **connectionless transport protocol**.

Unlike TCP, UDP does not establish a connection using a three-way handshake before sending data.

```text
Client
   │
   │ UDP Datagram
   ├──────────────────►
   │
   │ UDP Datagram
   ├──────────────────►
   │
   ▼
Server
```

UDP focuses on simplicity and low overhead.

---

# 🚀 Characteristics of UDP

UDP provides:

- Low overhead
- No connection establishment
- No built-in retransmission
- No guaranteed delivery
- No guaranteed ordering
- No built-in congestion control like TCP

This makes UDP useful when speed and low latency are more important than guaranteed delivery.

---

# 📦 TCP Segment vs UDP Datagram

TCP data is commonly called a:

```text
TCP Segment
```

UDP data is commonly called a:

```text
UDP Datagram
```

---

# 🆚 TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliability | Yes | No built-in guarantee |
| Ordering | Yes | No built-in guarantee |
| Retransmission | Yes | No |
| Handshake | Yes | No |
| Overhead | Higher | Lower |
| Speed/latency | Generally higher overhead | Generally lower overhead |
| Flow control | Yes | No |
| Congestion control | Yes | No built-in equivalent |
| Data unit | Segment | Datagram |

---

# 🌐 Common Uses of TCP

TCP is useful when reliable and ordered delivery is important.

Examples include:

```text
HTTP/HTTPS
SSH
FTP
SMTP
IMAP
```

Examples:

```text
Web communication
Remote administration
File transfers
Email delivery
```

---

# ⚡ Common Uses of UDP

UDP is useful for applications that can tolerate some packet loss or handle reliability themselves.

Examples include:

```text
DNS
DHCP
VoIP
Online gaming
Streaming
Real-time applications
```

Some modern application protocols can also implement reliability and congestion control at the application layer while using UDP underneath.

---

# 🌐 TCP and UDP Ports

TCP and UDP both use **port numbers** to identify applications or services.

Ports range from:

```text
0 – 65535
```

Example:

```text
TCP 22 → SSH
TCP 80 → HTTP
TCP 443 → HTTPS

UDP 53 → DNS
UDP 67 → DHCP Server
UDP 68 → DHCP Client
```

A port does not identify a physical device.

It identifies a communication endpoint associated with a service or application.

---

# 🔌 Socket Concept

A **socket** can be thought of as an endpoint for network communication.

A connection can involve information such as:

```text
Source IP
Source Port
Destination IP
Destination Port
Protocol
```

Example:

```text
192.168.1.10:51500
        ↓
93.184.216.34:443
        ↓
TCP
```

This helps identify a particular network flow.

---

# 🧩 TCP/IP Communication

A simplified communication flow looks like:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Ethernet / Wi-Fi
     ↓
Physical Network
```

For example:

```text
Browser
  ↓
TCP
  ↓
IP
  ↓
Wi-Fi
  ↓
Internet
  ↓
Web Server
```

---

# 🔐 TCP, UDP & Cybersecurity

Understanding TCP and UDP is extremely important in cybersecurity.

Security professionals need to understand:

- Network connections
- Open ports
- Listening services
- Network traffic
- Packet behavior
- Connection states
- Protocol identification

---

# 🔎 TCP Port Scanning

Security tools can inspect TCP ports to determine whether services may be listening.

For example:

```text
Target
  │
  ├── Port 22  → Open?
  ├── Port 80  → Open?
  ├── Port 443 → Open?
  └── Port 3306 → Open?
```

A common security tool used in authorized labs is:

```bash
nmap
```

Example:

```bash
nmap -sT 192.168.1.10
```

Only scan systems you own or have explicit permission to test.

---

# 🔍 Inspecting Connections on Linux

Linux provides several useful commands.

### View TCP/UDP sockets

```bash
ss -tun
```

### View listening sockets

```bash
ss -tuln
```

Where:

```text
t → TCP
u → UDP
l → Listening
n → Numeric addresses/ports
```

---

# 🧪 Practical Linux Exercise

Run:

```bash
ss -tuln
```

Look for:

```text
Local Address
Port
Protocol
State
```

Then ask:

```text
Which TCP ports are listening?
Which UDP ports are listening?
Which services might be associated with them?
Are all exposed services necessary?
```

---

# 🧪 Compare TCP and UDP

Create this mental model:

```text
             TCP
              │
       "Let's connect."
              ↓
         Handshake
              ↓
      Reliable transfer
              ↓
      Acknowledgements
              ↓
       Ordered delivery
```

Compared with:

```text
             UDP
              │
       "Send this data."
              ↓
       Datagram sent
              ↓
       No handshake
              ↓
    No built-in delivery guarantee
```

---

# 🎮 Real-World Example

Imagine an online multiplayer game.

A player's position changes frequently:

```text
Player → Move
Player → Move
Player → Move
Player → Move
```

For some real-time information, receiving the newest update quickly can be more important than retransmitting an old update.

UDP can be useful in such scenarios.

For something that absolutely must arrive correctly, such as an important file transfer, reliable transport is more appropriate.

The actual protocol choice depends on the application design.

---

# 📞 Real-Time Communication

Voice and video applications often care strongly about:

```text
Low latency
Low delay
Smooth communication
```

If one packet containing a tiny piece of audio is lost, retransmitting it several seconds later may not be useful.

This is one reason UDP is commonly associated with real-time communication.

---

# 🧠 Important Misconception

### ❌ "TCP is always better than UDP."

Not true.

They are designed for different requirements.

```text
Need reliable ordered delivery?
        ↓
       TCP

Need low overhead / real-time transport?
        ↓
       UDP
```

The application requirements determine the appropriate choice.

---

# 🛡️ Security Considerations

Both TCP and UDP can be involved in attacks and defensive monitoring.

Examples include:

### TCP SYN Flood

An attacker can send large numbers of TCP connection requests, potentially consuming server resources.

```text
SYN
SYN
SYN
SYN
SYN
 ↓
Server resources
 ↓
Potential service disruption
```

Defenses can include:

- Rate limiting
- Firewalls
- SYN cookies
- Load balancing
- Traffic monitoring

---

### UDP Flood

Large volumes of UDP traffic can consume network or system resources.

```text
UDP
UDP
UDP
UDP
UDP
 ↓
Target
 ↓
Resource exhaustion
```

Network controls and traffic filtering can help mitigate such attacks.

---

# 🔍 TCP States

TCP connections can exist in different states.

Common states include:

```text
LISTEN
SYN-SENT
SYN-RECEIVED
ESTABLISHED
FIN-WAIT
TIME-WAIT
CLOSE-WAIT
CLOSED
```

You can inspect TCP states with:

```bash
ss -tan
```

Example:

```text
LISTEN
ESTABLISHED
TIME-WAIT
```

Understanding these states is useful when troubleshooting and investigating network activity.

---

# 🧠 TCP vs UDP — Memory Trick

Think:

```text
TCP
T → Trustworthy delivery
C → Connection-oriented
P → Packet ordering/retransmission
```

And:

```text
UDP
U → Unconnected
D → Datagram
P → Prioritizes simplicity and low overhead
```

These are memory aids, not official definitions.

---
