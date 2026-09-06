# 🔧 Basic Network Troubleshooting

> **Learning how to systematically find, isolate, and fix network connectivity problems.**

---

## 🧠 What is Network Troubleshooting?

**Network troubleshooting** is the process of identifying and resolving problems that prevent devices, applications, or services from communicating correctly.

Instead of randomly trying commands, a good troubleshooting process works from the simplest possible cause toward more complex causes.

```text
Problem
   ↓
Collect information
   ↓
Check configuration
   ↓
Test connectivity
   ↓
Identify failure point
   ↓
Fix the problem
   ↓
Verify
```

---

# 🌐 The Network Troubleshooting Model

A useful way to think about troubleshooting is:

```text
My Device
   ↓
Network Interface
   ↓
Local Network
   ↓
Default Gateway
   ↓
DNS
   ↓
Internet / Remote Network
   ↓
Destination Service
```

If something fails, the goal is to determine **where** it fails.

---

# 🧩 Common Network Problems

Network issues can be caused by:

- Incorrect IP configuration
- Wrong subnet mask
- Missing default gateway
- DNS problems
- Cable/Wi-Fi problems
- Firewall rules
- Routing problems
- DHCP failures
- Service outages
- Incorrect application configuration
- Network congestion

The same symptom can have multiple causes.

---

# 🔎 Step 1 — Check the Network Interface

First, determine whether the device has an active network interface.

On Linux:

```bash
ip addr
```

or:

```bash
ip a
```

Look for:

```text
Interface
IP address
Subnet prefix
Interface state
```

Example:

```text
eth0
192.168.1.20/24
```

The `/24` indicates the network prefix length.

---

# 🟢 Check Interface State

You can inspect an interface with:

```bash
ip link
```

You may see:

```text
UP
DOWN
```

If the interface is down, network communication may not work.

Conceptually:

```text
Interface
    ↓
Is it UP?
    ↓
Yes → Continue
No  → Investigate interface
```

---

# 📡 Step 2 — Check Your IP Address

Run:

```bash
ip addr
```

Ask:

```text
Do I have an IP address?
Is it from the expected network?
Is the interface using IPv4, IPv6, or both?
```

For example:

```text
192.168.1.25/24
```

If the system has no expected address, investigate DHCP or manual network configuration.

---

# 🚪 Step 3 — Check the Default Gateway

The **default gateway** is the router used to reach destinations outside the local network.

Run:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

This means traffic destined for networks without a more specific route can be sent through:

```text
192.168.1.1
```

---

# 🧪 Test the Gateway

Use:

```bash
ping 192.168.1.1
```

If the gateway responds:

```text
Local network connectivity
        ↓
Likely working
```

If it doesn't:

```text
Check:
- Interface
- Wi-Fi/cable
- IP configuration
- Subnet
- Gateway
- Local firewall
```

> A failed ping does not always prove the network is broken because some devices or firewalls block ICMP.

---

# 🏓 Step 4 — Ping

`ping` is one of the simplest network diagnostic tools.

Example:

```bash
ping 8.8.8.8
```

It commonly uses **ICMP Echo Request** and **ICMP Echo Reply**.

Conceptually:

```text
Your Device
    │
    │ ICMP Echo Request
    ▼
Destination
    │
    │ ICMP Echo Reply
    ▼
Your Device
```

---

# ⏱️ Understanding Ping Results

A successful ping can provide information such as:

```text
Packets transmitted
Packets received
Packet loss
Round-trip time
```

Example:

```text
64 bytes from 8.8.8.8
time=20 ms
```

The exact output varies by operating system.

---

# 🚨 Packet Loss

Suppose:

```text
Packets transmitted: 10
Packets received: 7
```

That indicates:

```text
30% packet loss
```

Possible causes include:

- Congestion
- Weak wireless signal
- Faulty hardware
- Routing problems
- Firewall/filtering
- Destination-side behavior

Packet loss should be interpreted in context.

---

# 🌍 Step 5 — Test Internet Connectivity

Try a known IP address:

```bash
ping 1.1.1.1
```

If this works but a domain name does not:

```bash
ping example.com
```

then DNS may be the problem.

Conceptually:

```text
Ping IP works
      ↓
Network connectivity exists
      ↓
Domain fails
      ↓
Investigate DNS
```

---

# 🔤 Step 6 — Troubleshoot DNS

DNS converts names into IP addresses.

Example:

```text
example.com
     ↓
DNS
     ↓
IP Address
```

Use:

```bash
nslookup example.com
```

or:

```bash
dig example.com
```

You can also use:

```bash
host example.com
```

---

# 🧪 DNS Troubleshooting

Suppose:

```bash
ping 1.1.1.1
```

works.

But:

```bash
ping example.com
```

fails with a name-resolution error.

This suggests:

```text
Internet connectivity
        ↓
Working

DNS resolution
        ↓
Possible problem
```

Possible causes:

- Incorrect DNS server
- DNS server unavailable
- DNS configuration error
- Local resolver problem
- Network filtering

---

# 🧭 Step 7 — Trace the Route

Sometimes you need to determine where traffic stops along the path.

Linux commonly uses:

```bash
traceroute example.com
```

On some Linux distributions, it may need to be installed separately.

Another option is:

```bash
tracepath example.com
```

---

# 🛣️ How Traceroute Works

Traceroute attempts to reveal intermediate network hops.

Conceptually:

```text
Your Device
    ↓
Router 1
    ↓
Router 2
    ↓
Router 3
    ↓
Destination
```

Example:

```text
1   192.168.1.1
2   ISP Router
3   ISP Network
4   ...
5   Destination
```

This can help identify where connectivity may be failing.

---

# ⚠️ Traceroute Limitations

A `*` does not automatically mean a router is broken.

Some routers:

- Block traceroute probes
- Rate-limit responses
- Do not reveal information
- Treat diagnostic traffic differently

Therefore:

```text
No response
≠
Definitely broken
```

Interpret results carefully.

---

# 🔌 Step 8 — Check Ports

A host may be reachable while a particular service is unavailable.

For example:

```text
Server reachable
        ↓
HTTPS port 443
        ↓
Connection works
```

But:

```text
Server reachable
        ↓
Application port
        ↓
Connection fails
```

This means the problem may be service-specific rather than basic network connectivity.

---

# 🐧 Check Listening Ports

On Linux:

```bash
ss -tuln
```

For process information:

```bash
sudo ss -tulpn
```

You can investigate:

```text
Which ports are listening?
Which protocol is being used?
Which service owns the socket?
```

---

# 🌐 Step 9 — Test an HTTP Service

Use:

```bash
curl -I https://example.com
```

This allows you to inspect response headers.

For more detailed output:

```bash
curl -v https://example.com
```

This can help distinguish between:

```text
DNS problem
TCP connection problem
TLS problem
HTTP response problem
```

---

# 🔐 Example HTTPS Troubleshooting

Suppose:

```bash
ping example.com
```

works.

DNS:

```bash
dig example.com
```

works.

But:

```bash
curl https://example.com
```

fails.

You can investigate further:

```text
DNS
 ↓
Working

IP connectivity
 ↓
Working

TCP connection
 ↓
Check

TLS handshake
 ↓
Check

HTTP response
 ↓
Check
```

This is much more useful than simply saying:

> "The internet isn't working."

---

# 🧩 Layer-by-Layer Troubleshooting

Network problems can often be isolated by thinking through layers.

```text
Application
     ↓
Transport
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

Example:

```text
Website not loading
        ↓
Can DNS resolve?
        ↓
Can IP be reached?
        ↓
Can TCP 443 connect?
        ↓
Does TLS succeed?
        ↓
Does HTTP return a response?
```

This approach narrows the problem.

---

# 🧠 OSI-Based Troubleshooting

The OSI model can also help structure troubleshooting.

### Layer 1 — Physical

Check:

```text
Cable
Wi-Fi
Power
Signal
Network interface
```

### Layer 2 — Data Link

Check:

```text
Ethernet/Wi-Fi
MAC address
Switch connection
VLAN configuration
```

### Layer 3 — Network

Check:

```text
IP address
Subnet
Gateway
Routing
```

### Layer 4 — Transport

Check:

```text
TCP
UDP
Ports
Firewall filtering
```

### Layer 7 — Application

Check:

```text
DNS
HTTP
HTTPS
Application configuration
Server response
```

---

# 🔥 A Practical Troubleshooting Flow

Use this sequence:

```text
1. Is the interface UP?
        ↓
2. Do I have an IP?
        ↓
3. Is the subnet correct?
        ↓
4. Do I have a default gateway?
        ↓
5. Can I reach the gateway?
        ↓
6. Can I reach an external IP?
        ↓
7. Does DNS resolve names?
        ↓
8. Can I reach the required port?
        ↓
9. Is the application responding?
```

This gives you a logical path from local configuration to the application.

---

# 🧪 Troubleshooting Example

### Problem:

> "I can connect to Wi-Fi, but websites aren't loading."

Start with:

```bash
ip addr
```

Check the IP.

Then:

```bash
ip route
```

Check the gateway.

Then:

```bash
ping <gateway>
```

Test local connectivity.

Then:

```bash
ping 1.1.1.1
```

Test external IP connectivity.

Then:

```bash
dig example.com
```

Test DNS.

Then:

```bash
curl -I https://example.com
```

Test HTTPS.

---

# 🔍 Possible Results

### Case 1

```text
No IP address
```

Possible issue:

```text
DHCP / network configuration
```

---

### Case 2

```text
IP exists
Gateway unreachable
```

Possible issue:

```text
Local network
Wi-Fi
Subnet
Gateway
```

---

### Case 3

```text
Gateway works
External IP fails
```

Possible issue:

```text
Routing
NAT
ISP/upstream network
Firewall
```

---

### Case 4

```text
External IP works
Domain fails
```

Possible issue:

```text
DNS
```

---

### Case 5

```text
DNS works
HTTPS fails
```

Possible issue:

```text
TCP port 443
Firewall
TLS
Server
```

---

### Case 6

```text
HTTPS connects
Application returns 500
```

The network may be working correctly.

The problem could be on the **server/application side**.

---

# 🧰 Essential Troubleshooting Commands

| Command | Purpose |
|---|---|
| `ip addr` | View IP addresses |
| `ip link` | View interfaces |
| `ip route` | View routing table |
| `ping` | Test reachability |
| `traceroute` | Trace network path |
| `tracepath` | Trace path and network parameters |
| `nslookup` | Query DNS |
| `dig` | Detailed DNS queries |
| `host` | Simple DNS lookup |
| `ss` | Inspect sockets |
| `curl` | Test HTTP/HTTPS |
| `hostname` | View system hostname |

---

# 🛡️ Network Troubleshooting & Cybersecurity

Troubleshooting skills are extremely useful in cybersecurity.

A security analyst may need to determine:

```text
Is this a network problem?
        ↓
Or a firewall rule?
        ↓
Or a service failure?
        ↓
Or suspicious traffic?
```

Understanding normal network behavior makes abnormal behavior easier to recognize.

---

# 🔎 Troubleshooting Security Events

Imagine a server suddenly cannot reach another system.

Possible causes include:

```text
Routing change
Firewall rule
Service failure
DNS problem
Network outage
Malware
Unauthorized configuration change
```

A security analyst should not immediately assume an attack.

The correct approach is:

```text
Observe
 ↓
Collect evidence
 ↓
Test
 ↓
Compare with expected behavior
 ↓
Identify cause
```

---

# 📊 Logs and Troubleshooting

Network problems often leave useful evidence in logs.

Depending on the system, investigate:

```text
System logs
Firewall logs
Authentication logs
Application logs
Network device logs
```

You can search Linux logs using tools such as:

```bash
journalctl
```

For example:

```bash
journalctl -b
```

This can show logs from the current boot.

---

# 🧪 Practice Lab

Run these commands on your Linux system:

### 1. Check interfaces

```bash
ip addr
```

### 2. Check routes

```bash
ip route
```

### 3. Check sockets

```bash
ss -tuln
```

### 4. Test your gateway

```bash
ping <your-gateway>
```

### 5. Test external connectivity

```bash
ping 1.1.1.1
```

### 6. Test DNS

```bash
dig example.com
```

### 7. Test HTTPS

```bash
curl -I https://example.com
```

### 8. Trace the route

```bash
tracepath example.com
```

Record what each command tells you.

---

# 🧠 Troubleshooting Mindset

Avoid:

```text
Try random commands
        ↓
Change random settings
        ↓
Hope it works
```

Instead:

```text
Observe
   ↓
Form a hypothesis
   ↓
Run a targeted test
   ↓
Analyze the result
   ↓
Change one thing
   ↓
Test again
```

This is a much stronger troubleshooting habit.

---
