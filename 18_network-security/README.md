# 🛡️ Network Security Fundamentals

> **Understanding how networks are protected, monitored, and defended against unauthorized access and attacks.**

---

## 🧠 What is Network Security?

**Network security** is the practice of protecting networks, devices, services, and data from unauthorized access, misuse, disruption, and attacks.

It combines:

```text
People
  +
Processes
  +
Technology
  ↓
Network Security
```

The goal is not simply to "block hackers."

A secure network should:

- Prevent unauthorized access
- Protect sensitive information
- Detect suspicious activity
- Maintain availability
- Reduce attack surface
- Respond to security incidents

---

# 🔐 The CIA Triad

One of the most important concepts in cybersecurity is the **CIA Triad**.

```text
             Confidentiality
                  /\
                 /  \
                /    \
               /      \
              /        \
             /__________\
        Integrity      Availability
```

---

## 🔒 Confidentiality

Ensures that information is accessible only to authorized people or systems.

Examples:

```text
Encryption
Access control
Authentication
```

---

## 🧾 Integrity

Ensures that information is not changed without authorization.

Examples:

```text
Hashing
Digital signatures
File integrity monitoring
```

---

## ⚡ Availability

Ensures that systems and services remain accessible when needed.

Examples:

```text
Redundancy
Backups
DDoS protection
Failover systems
```

---

# 🧩 Authentication vs Authorization

These two concepts are closely related but different.

### Authentication

> **Who are you?**

Examples:

```text
Password
MFA
SSH key
Biometric authentication
```

### Authorization

> **What are you allowed to do?**

Example:

```text
User
 ↓
Authenticated
 ↓
Can access website
 ↓
Cannot access administrator settings
```

---

# 🔑 Strong Authentication

Weak authentication can make a network easier to compromise.

Good practices include:

- Strong unique passwords
- Multi-factor authentication
- SSH key authentication
- Account protection
- Limiting administrative access

---

# 🧱 Firewalls

A **firewall** controls network traffic according to defined rules.

Conceptually:

```text
Internet
   │
   ▼
┌───────────┐
│ Firewall  │
└───────────┘
   │
   ▼
Internal Network
```

A firewall can make decisions based on information such as:

```text
Source IP
Destination IP
Protocol
Port
Connection state
Application
```

---

# 🚦 Firewall Example

Imagine a server where only HTTPS should be publicly accessible.

```text
TCP 443 → Allow
TCP 22  → Restricted
Other unnecessary ports → Block
```

The exact rules depend on the network's requirements.

---

# 🛡️ Firewall Types

Common categories include:

### Network Firewall

Protects traffic between networks.

```text
Internet
   ↓
Firewall
   ↓
Internal Network
```

### Host-Based Firewall

Runs directly on a system.

```text
Computer
 └── Firewall
```

Examples on Linux include:

```text
nftables
ufw
firewalld
```

---

# 🐧 Linux Firewall Basics

### UFW

On systems where UFW is installed:

```bash
sudo ufw status
```

Example of viewing firewall rules:

```bash
sudo ufw status verbose
```

UFW is a user-friendly interface for managing firewall rules on many Debian/Ubuntu-based systems.

---

# 🔍 Network Monitoring

Network security requires visibility.

Security teams monitor things such as:

```text
Connections
Traffic volume
Source IPs
Destination IPs
Ports
Protocols
Authentication events
Firewall events
```

The goal is to identify:

```text
Normal behavior
       ↓
Compare
       ↓
Unusual behavior
       ↓
Investigate
```

---

# 📊 Logs

Logs provide evidence about what happened on a system or network.

Examples:

```text
Authentication logs
Firewall logs
Web server logs
DNS logs
VPN logs
System logs
```

A security analyst may investigate:

```text
Who connected?
When?
From where?
To what?
Using which protocol?
Was access successful?
```

---

# 🚨 Common Network Attacks

Understanding attacks is important for building defenses.

Common examples include:

- Port scanning
- Phishing
- Sniffing
- Man-in-the-middle attacks
- DoS
- DDoS
- DNS spoofing
- DNS cache poisoning
- Brute-force attacks
- Session attacks
- Malware-based network activity

---

# 🔎 Port Scanning

Port scanning attempts to identify reachable ports and potentially exposed services.

Example:

```text
Target
 │
 ├── 22   → SSH
 ├── 80   → HTTP
 ├── 443  → HTTPS
 └── 3389 → RDP
```

Security professionals can use scanning for authorized security assessments.

A commonly used tool is:

```bash
nmap
```

Example:

```bash
nmap 192.168.1.10
```

Only scan systems you own or have explicit permission to test.

---

# 👀 Network Sniffing

**Network sniffing** involves capturing and analyzing network traffic.

Security professionals use packet capture to:

- Troubleshoot networks
- Investigate incidents
- Analyze protocols
- Detect suspicious traffic

Tools include:

```text
Wireshark
tcpdump
```

---

# 🧪 tcpdump

Linux commonly provides `tcpdump` for packet capture.

Example:

```bash
sudo tcpdump
```

To capture traffic on a specific interface:

```bash
sudo tcpdump -i eth0
```

The interface name may differ on your system.

To inspect DNS traffic, for example:

```bash
sudo tcpdump -i any port 53
```

Use packet capture only on systems and networks you are authorized to monitor.

---

# 🕵️ Man-in-the-Middle Attack

A **Man-in-the-Middle (MITM)** attack occurs when an attacker positions themselves between communicating parties and attempts to observe or manipulate their communication.

Conceptually:

```text
Client
   │
   ▼
Attacker
   │
   ▼
Server
```

Strong encryption and proper authentication help defend against MITM attacks.

---

# 🔐 Encryption

Encryption transforms readable information into protected data.

```text
Plaintext
   ↓
Encryption
   ↓
Ciphertext
```

The intended recipient can use the appropriate cryptographic mechanism to recover the information.

---

# 🌐 Encryption in Networking

Examples include:

```text
HTTPS → TLS
SSH   → Encrypted remote administration
VPN   → Protected network tunnel
```

Encryption helps provide confidentiality and, depending on the protocol, integrity and authentication.

---

# 🧅 VPN

A **Virtual Private Network (VPN)** creates a protected connection across an underlying network.

Conceptually:

```text
Device
  │
  │ Encrypted tunnel
  ▼
VPN Server
  │
  ▼
Network / Internet
```

VPNs can be useful for:

- Secure remote access
- Connecting private networks
- Protecting traffic over untrusted networks

A VPN does not make a user completely anonymous or automatically secure every activity.

---

# 🚫 DoS and DDoS

## DoS

**Denial of Service**

Attempts to make a service unavailable by overwhelming or exhausting resources.

```text
Attacker
   ↓
Target
   ↓
Resource exhaustion
   ↓
Service disruption
```

---

## DDoS

**Distributed Denial of Service**

Traffic comes from multiple systems or locations.

```text
Device ─┐
Device ─┤
Device ─┼──► Target
Device ─┤
Device ─┘
```

Defenses can include:

- Rate limiting
- Traffic filtering
- Load balancing
- DDoS mitigation services
- Network monitoring
- Redundancy

---

# 🎣 Phishing

Phishing uses deceptive communication to trick users into revealing information or performing an unsafe action.

Examples:

```text
Fake login page
Malicious email
Fake password reset
Fraudulent message
```

Network security is not only about technology.

**Users are part of the security boundary.**

---

# 🌐 DNS Security

DNS can be abused in several ways.

Examples include:

```text
DNS spoofing
DNS cache poisoning
DNS tunneling
DNS amplification
```

Security measures can include:

```text
DNSSEC
Secure DNS configuration
Monitoring
Filtering
```

---

# 🔐 Secure Protocols

Whenever possible, use secure alternatives.

```text
HTTP  → HTTPS
Telnet → SSH
FTP → SFTP / FTPS
```

The general principle is:

```text
Unprotected communication
        ↓
Replace with
        ↓
Authenticated + protected communication
```

---

# 🧱 Network Segmentation

Network segmentation divides a network into separate logical or physical sections.

Instead of:

```text
Everything
   │
   ▼
One Large Network
```

you might have:

```text
Internet
   │
   ▼
Firewall
   │
   ├── User Network
   ├── Server Network
   ├── Guest Network
   └── Security Management Network
```

Segmentation can limit the impact of a compromised system.

---

# 🔐 Principle of Least Privilege

Give users and systems only the access they actually need.

```text
Required access
      ↓
Grant access

Unnecessary access
      ↓
Do not grant
```

This reduces the potential impact of compromised accounts or systems.

---

# 🛡️ Defense in Depth

Security should not depend on a single control.

For example:

```text
Firewall
   ↓
Network Segmentation
   ↓
Authentication
   ↓
Encryption
   ↓
Endpoint Security
   ↓
Logging
   ↓
Monitoring
   ↓
Incident Response
```

If one layer fails, additional layers can still provide protection.

---

# 🚨 Intrusion Detection

An **Intrusion Detection System (IDS)** monitors activity for potentially malicious behavior.

Conceptually:

```text
Network Traffic
      ↓
     IDS
      ↓
Analyze
      ↓
Suspicious?
   ↙      ↘
 Yes       No
  ↓         ↓
Alert     Normal
```

---

# 🛡️ Intrusion Prevention

An **Intrusion Prevention System (IPS)** can detect suspicious activity and take configured preventive action.

Conceptually:

```text
Traffic
   ↓
IPS
   ↓
Analyze
   ↓
Suspicious
   ↓
Block / Prevent
```

A simplified distinction:

```text
IDS → Detect + Alert
IPS → Detect + Prevent
```

Actual capabilities depend on the product and configuration.

---

# 📡 Network Access Control

Network access controls can determine which devices or users are allowed to connect to network resources.

Possible controls include:

```text
Authentication
Device validation
Network segmentation
Access policies
```

The goal is to prevent unauthorized devices from gaining inappropriate network access.

---

# 🔎 Security Monitoring

A security analyst might investigate an unusual event like:

```text
Large outbound traffic
        ↓
Check source device
        ↓
Check destination
        ↓
Check port
        ↓
Check process
        ↓
Check user activity
        ↓
Check logs
        ↓
Determine whether behavior is expected
```

This is why networking fundamentals are so important for cybersecurity.

---

# 🧠 Incident Response

When a security incident occurs, organizations typically follow a structured process.

A simplified lifecycle:

```text
Preparation
    ↓
Detection
    ↓
Analysis
    ↓
Containment
    ↓
Eradication
    ↓
Recovery
    ↓
Lessons Learned
```

The exact framework may vary between organizations.

---

# 🧪 Basic Security Investigation

Suppose you notice an unexpected connection.

Start with:

```text
1. Identify source IP
2. Identify destination IP
3. Identify port
4. Identify protocol
5. Check timestamp
6. Identify process/service
7. Review logs
8. Determine whether the connection is expected
```

Do not immediately assume malicious activity.

**Evidence first.**

---

# 🐧 Useful Linux Security Commands

### View interfaces

```bash
ip addr
```

### View routes

```bash
ip route
```

### View connections

```bash
ss -tun
```

### View listening services

```bash
ss -tuln
```

### View processes

```bash
ps aux
```

### View system logs

```bash
journalctl
```

### Inspect network traffic

```bash
sudo tcpdump
```

### Check firewall status

```bash
sudo ufw status
```

The exact commands and available tools depend on the Linux distribution and configuration.

---

# 🧠 Network Security Checklist

When securing a network, consider:

```text
☐ Strong authentication
☐ MFA where appropriate
☐ Secure protocols
☐ Firewall
☐ Network segmentation
☐ Least privilege
☐ Regular updates
☐ Secure configuration
☐ Logging
☐ Monitoring
☐ Backups
☐ Incident response plan
```

---

# 🌐 Putting the Roadmap Together

You have now connected the major networking concepts:

```text
IP Addressing
      ↓
Subnetting
      ↓
MAC Addresses
      ↓
DNS
      ↓
DHCP
      ↓
NAT & PAT
      ↓
TCP & UDP
      ↓
HTTP & HTTPS
      ↓
Protocols & Ports
      ↓
Troubleshooting
      ↓
Network Security
```

Each topic builds on the previous one.

---

# 🔥 From Networking to Cybersecurity

Networking knowledge is one of the foundations of cybersecurity.

For example:

```text
Networking
    ↓
Understand normal traffic
    ↓
Identify abnormal traffic
    ↓
Investigate connections
    ↓
Analyze logs
    ↓
Detect threats
    ↓
Respond to incidents
```

This knowledge can support future areas such as:

- SOC analysis
- Network security
- Incident response
- Digital forensics
- Penetration testing
- Threat detection
- Security monitoring

---
