# 🌐 NAT & PAT — Network Address Translation

> **How private networks communicate with the internet using a limited number of public IP addresses.**

---

## 🧠 What is NAT?

**NAT (Network Address Translation)** is a networking technique that modifies IP address information as packets move between networks.

It is commonly used to allow devices with **private IP addresses** to communicate with systems on the public internet.

A typical home network looks like:

```text
          🌐 Internet
               │
        Public IP Address
               │
          🛜 Router
               │
       ┌───────┼───────┐
       ▼       ▼       ▼
    Laptop   Phone    PC
192.168.x.x 192.168.x.x 192.168.x.x
```

The devices inside the network can use private IP addresses while the router communicates with the internet using a public IP address.

---

# 🔒 Private vs Public IP Addresses

## Private IP Addresses

Private addresses are used inside local networks.

Common private IPv4 ranges are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Examples:

```text
10.0.0.15
172.16.5.20
192.168.1.25
```

These addresses are not directly routable across the public internet.

---

## 🌍 Public IP Address

A public IP address is used for communication across the internet.

Example:

```text
203.0.113.10
```

Public IP addresses must be globally routable and are assigned according to internet addressing policies.

---

# 🔄 Why is NAT Needed?

IPv4 provides a limited address space.

NAT allows many devices inside a private network to share one or a small number of public IPv4 addresses.

```text
Private Network

192.168.1.10 ──┐
192.168.1.11 ──┤
192.168.1.12 ──┼──► NAT Router ──► Internet
192.168.1.13 ──┤
192.168.1.14 ──┘
                       │
                       ▼
                  Public IP
```

This helped extend the practical usability of IPv4.

---

# 🔁 Basic NAT Flow

Suppose a laptop has:

```text
Private IP:
192.168.1.10
```

The router has:

```text
Public IP:
203.0.113.10
```

When the laptop accesses an internet service:

```text
Laptop
192.168.1.10
     │
     ▼
NAT Router
     │
     │ Translates address
     ▼
203.0.113.10
     │
     ▼
Internet
```

When the response comes back, the router uses its NAT state to forward the traffic to the correct internal device.

---

# 🧩 NAT Translation Table

A router can maintain information about active translations.

Conceptually:

```text
Inside Private       Public Translation
192.168.1.10:50000 → 203.0.113.10:40001
192.168.1.11:50001 → 203.0.113.10:40002
192.168.1.12:50002 → 203.0.113.10:40003
```

The router uses this information to associate returning traffic with the correct internal connection.

---

# 🔢 What is PAT?

**PAT (Port Address Translation)** is a form of NAT that uses **port numbers** to distinguish between multiple connections sharing the same public IP address.

It is sometimes called:

- NAT overload
- Many-to-one NAT
- NAPT

Example:

```text
192.168.1.10:50000
          │
          ▼
203.0.113.10:40001
```

Another device:

```text
192.168.1.11:50000
          │
          ▼
203.0.113.10:40002
```

Both devices can use the same public IP because the translated port numbers help distinguish their connections.

---

# 🔥 NAT vs PAT

| NAT | PAT |
|---|---|
| Translates IP addresses | Translates IP addresses and ports |
| Can map one address to another | Allows many private devices to share one public IP |
| Doesn't necessarily rely on port translation | Uses port numbers to distinguish connections |
| General translation technique | Common form of NAT used in home networks |

In everyday home networking, what people commonly call **NAT** is often actually **PAT**.

---

# 🧠 Types of NAT

Several NAT behaviors can be used depending on the network design.

## 1️⃣ Static NAT

One private address maps to one public address.

```text
192.168.1.10
      │
      ▼
203.0.113.10
```

This mapping is generally fixed.

Useful when a specific internal system needs a consistent public mapping.

---

## 2️⃣ Dynamic NAT

Private addresses are translated using a pool of public addresses.

```text
Private Network
      │
      ▼
NAT Pool
 ┌────┼────┐
 ▼    ▼    ▼
Public IPs
```

An available public address can be assigned for a connection according to the configured rules.

---

## 3️⃣ PAT

Multiple private devices share one public IP using different port numbers.

```text
192.168.1.10:5000 ──┐
192.168.1.11:5001 ──┼──► 203.0.113.10
192.168.1.12:5002 ──┘
```

This is extremely common in home and small-office networks.

---

# 🚪 Port Forwarding

NAT can also be configured to forward incoming traffic from a public address/port to an internal system.

Example:

```text
Internet
   │
   │ TCP 8080
   ▼
Router
   │
   │ Forward
   ▼
192.168.1.50:80
```

This is commonly called **port forwarding** or **destination NAT**, depending on the implementation.

It can be useful when an internal service needs to be reachable from outside the network.

However, exposing services to the internet increases the attack surface and should be done carefully.

---

# 🌐 NAT and Routing

NAT and routing are related, but they are not the same thing.

### Routing

Determines:

> **Where should the packet go?**

### NAT

Changes relevant address information:

> **Which address should appear in the packet?**

Conceptually:

```text
Packet
  │
  ▼
Routing decision
  │
  ▼
NAT translation
  │
  ▼
Forward packet
```

The exact order depends on the networking platform and direction of traffic.

---

# 🔐 NAT and Cybersecurity

NAT is sometimes described as a security feature because private devices are not directly exposed to unsolicited internet traffic in many common configurations.

However:

> **NAT is not a replacement for a firewall.**

NAT primarily performs address/port translation.

A firewall makes explicit decisions about whether traffic should be allowed or blocked.

```text
NAT
 ↓
Address translation

Firewall
 ↓
Traffic filtering
```

Both can be used together.

---

# 🛡️ NAT Does NOT Make a Network Secure

A common misconception is:

```text
Private IP
   ↓
NAT
   ↓
"Completely secure" ❌
```

A better model is:

```text
NAT
  +
Firewall
  +
Secure Services
  +
Strong Authentication
  +
Updates
  +
Monitoring
```

Security comes from multiple layers.

---

# 🔍 NAT and Network Investigation

NAT creates an important challenge during security investigations.

Suppose a public IP is observed:

```text
203.0.113.10
```

That public IP could represent many internal devices.

```text
203.0.113.10
       │
       ├── 192.168.1.10
       ├── 192.168.1.11
       ├── 192.168.1.12
       └── 192.168.1.13
```

Therefore, investigators may need:

- Source port
- Destination port
- Timestamp
- NAT translation logs
- Firewall logs
- DHCP records

to determine which internal device was responsible for a connection.

---

# 🧪 Practical Example

Imagine three devices:

```text
Laptop
192.168.1.10

Phone
192.168.1.11

Desktop
192.168.1.12
```

The router has:

```text
Public IP
203.0.113.10
```

All three devices access the internet.

PAT could maintain translations such as:

```text
192.168.1.10:51000
        ↓
203.0.113.10:40001

192.168.1.11:51001
        ↓
203.0.113.10:40002

192.168.1.12:51002
        ↓
203.0.113.10:40003
```

The same public IP is shared while the different ports distinguish the connections.

---

# 🐧 Linux Network Inspection

Linux provides commands that help inspect network configuration.

### View IP addresses

```bash
ip addr
```

or:

```bash
ip a
```

---

### View routing table

```bash
ip route
```

---

### View listening sockets

```bash
ss -tuln
```

---

### View network connections

```bash
ss -tun
```

These commands help build an understanding of how a Linux system participates in a network.

---

# 🔎 NAT Troubleshooting

When investigating connectivity problems, consider:

```text
Does the device have an IP?
        ↓
Is the subnet correct?
        ↓
Is there a default gateway?
        ↓
Can the gateway be reached?
        ↓
Is NAT configured?
        ↓
Is the firewall allowing the traffic?
        ↓
Can the destination be reached?
```

NAT problems can appear as:

- No internet access
- Some services working while others fail
- Port-forwarding failures
- Unexpected connection behavior

---

# 🧠 Key Concepts

```text
NAT
│
├── Private IP
├── Public IP
├── Address Translation
│
├── Static NAT
├── Dynamic NAT
├── PAT
│   └── Port Translation
│
├── NAT Table
├── Port Forwarding
├── Routing
│
└── Cybersecurity
    ├── Attack Surface
    ├── Firewall
    ├── Logs
    └── Investigation
```

---

# 📝 Quick Revision

### What is NAT?

A technique used to translate network addresses between networks.

### Why is NAT commonly used?

To allow private networks to communicate with external networks and to conserve public IPv4 addresses.

### What is PAT?

A form of NAT that uses port numbers to allow multiple connections to share a public IP address.

### What are common private IPv4 ranges?

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

### Is NAT a firewall?

**No.**

NAT and firewalls serve different purposes.

### Why are ports important in PAT?

They allow multiple connections using the same public IP to be distinguished.

### Why are NAT logs useful?

They can help correlate public connections with internal devices.

---

# 🧪 Practice Questions

1. Why are private IP addresses used?
2. What problem does NAT help solve?
3. What is the difference between NAT and PAT?
4. Why does PAT use port numbers?
5. What is a NAT translation table?
6. What is port forwarding?
7. Is NAT itself a complete security solution?
8. Why are NAT logs useful during an investigation?

---

# ✅ What I Learned

- [x] NAT
- [x] Private IP addresses
- [x] Public IP addresses
- [x] Address translation
- [x] NAT translation tables
- [x] Static NAT
- [x] Dynamic NAT
- [x] PAT
- [x] Port translation
- [x] Port forwarding
- [x] NAT vs routing
- [x] NAT and firewall differences
- [x] NAT security considerations
- [x] NAT investigation concepts
- [x] Linux network inspection

---

# 🌐 Networking Progress

```text
Networking Fundamentals
        ↓
OSI & TCP/IP
        ↓
IP Addressing
        ↓
MAC & ARP
        ↓
Subnetting
        ↓
Routing
        ↓
Network Protocols
        ↓
Network Troubleshooting
        ↓
Network Security
        ↓
DNS
        ↓
DHCP
        ↓
NAT & PAT
        ↓
HTTP / HTTPS
        ↓
Packet Analysis
        ↓
Practical Network Security
```

---

