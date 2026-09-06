# 🔌 Common Network Protocols & Ports

> **Learning the protocols and port numbers that make network communication possible.**

---

## 🧠 What is a Network Protocol?

A **network protocol** is a set of rules that defines how devices communicate and exchange data.

Different protocols are designed for different purposes.

For example:

```text
DNS
↓
Domain name resolution

DHCP
↓
Automatic network configuration

HTTP
↓
Web communication

SSH
↓
Secure remote access

SMTP
↓
Sending email
```

---

# 🔢 What is a Port?

A **port number** helps identify a specific service or application on a device.

Port numbers range from:

```text
0 – 65535
```

A network connection can be identified using information such as:

```text
Source IP
Source Port
Destination IP
Destination Port
Protocol
```

Example:

```text
192.168.1.20:51500
        ↓
93.184.216.34:443
        ↓
TCP
```

---

# 🧩 Port Number Ranges

Port numbers are commonly divided into three ranges.

### 0–1023

**Well-known ports**

Common system and network services use ports in this range.

Examples:

```text
22
53
80
443
```

---

### 1024–49151

**Registered ports**

These can be assigned for specific applications and services.

---

### 49152–65535

**Dynamic / Private ports**

These are commonly used as temporary client-side ports.

For example:

```text
Client
192.168.1.20:52341
       │
       ▼
Server
93.184.216.34:443
```

The client may use a temporary source port while connecting to a server's well-known service port.

---

# 🌐 Important Protocols & Ports

## 🔐 SSH

**Secure Shell**

```text
TCP 22
```

Used for secure remote administration.

```text
Administrator
     │
     │ SSH
     ▼
Linux Server
```

Example:

```bash
ssh user@server
```

### Security relevance

SSH is commonly used to administer Linux systems remotely.

Security considerations include:

- Strong authentication
- Key-based authentication
- Disabling unnecessary access
- Limiting exposed services
- Monitoring login attempts

---

# 📁 FTP

**File Transfer Protocol**

Commonly associated with:

```text
TCP 21 → Control
TCP 20 → Traditional active-mode data
```

FTP is an older protocol and does not provide encryption by itself.

For secure file transfer, alternatives such as **SFTP** or **FTPS** may be used.

---

# 🔒 SFTP

**SSH File Transfer Protocol**

SFTP operates through SSH.

```text
TCP 22
```

It provides encrypted file transfer and remote file management over an SSH connection.

Important:

```text
FTP ≠ SFTP
```

SFTP is not simply "secure FTP"; it is a different protocol built on SSH.

---

# 🌐 HTTP

**Hypertext Transfer Protocol**

```text
TCP 80
```

Used for web communication.

```text
Browser
   │
   │ HTTP
   ▼
Web Server
```

HTTP traffic is not protected by TLS.

---

# 🔐 HTTPS

**HTTP Secure**

Commonly:

```text
TCP 443
```

HTTPS uses HTTP over TLS.

```text
HTTP
 +
TLS
 ↓
HTTPS
```

It helps provide:

- Confidentiality
- Integrity
- Server authentication

---

# 🌍 DNS

**Domain Name System**

Commonly:

```text
UDP 53
TCP 53
```

DNS translates domain names into IP addresses and performs other naming functions.

Example:

```text
example.com
     ↓
DNS
     ↓
IP Address
```

DNS commonly uses UDP for ordinary queries, while TCP is also used in situations such as larger responses and zone transfers.

---

# 📡 DHCP

**Dynamic Host Configuration Protocol**

Common ports:

```text
UDP 67 → Server
UDP 68 → Client
```

DHCP can automatically provide network configuration such as:

- IP address
- Subnet mask
- Default gateway
- DNS server

A simplified process is:

```text
Discover
   ↓
Offer
   ↓
Request
   ↓
Acknowledgement
```

This is known as **DORA**.

---

# 📧 SMTP

**Simple Mail Transfer Protocol**

Commonly associated with:

```text
TCP 25
TCP 587
TCP 465
```

SMTP is primarily used for **sending and relaying email**.

Port 587 is commonly used for message submission with authentication.

Port 465 is commonly used for SMTP over TLS.

---

# 📥 POP3

**Post Office Protocol version 3**

```text
TCP 110
```

Secure variant commonly uses:

```text
TCP 995
```

POP3 is used for retrieving email.

A simplified model:

```text
Mail Server
    │
    │ Download messages
    ▼
Email Client
```

POP3 commonly focuses on downloading messages rather than maintaining a synchronized mailbox across multiple devices.

---

# 📬 IMAP

**Internet Message Access Protocol**

```text
TCP 143
```

Secure IMAP commonly uses:

```text
TCP 993
```

IMAP allows email clients to manage messages while keeping the mailbox primarily on the server.

This makes it well suited to accessing the same mailbox from multiple devices.

---

# 🖥️ Telnet

```text
TCP 23
```

Telnet provides remote terminal access but does **not** provide modern encrypted protection by itself.

```text
Telnet
  ↓
Unencrypted communication
```

SSH is generally preferred for secure remote administration.

```text
Telnet ❌
SSH    ✅
```

---

# 🗄️ SMB

**Server Message Block**

Commonly:

```text
TCP 445
```

SMB is used for:

- File sharing
- Printer sharing
- Network resources

It is widely used in Windows environments.

### Security relevance

Exposed SMB services can increase attack surface, especially when poorly configured or unpatched.

---

# 🗃️ LDAP

**Lightweight Directory Access Protocol**

Commonly:

```text
TCP/UDP 389
```

Secure LDAP commonly uses:

```text
TCP 636
```

LDAP can be used to access and manage directory information.

It is commonly associated with:

- User directories
- Authentication systems
- Organizational information

---

# 🛡️ RDP

**Remote Desktop Protocol**

Commonly:

```text
TCP 3389
```

RDP allows remote graphical access to systems.

```text
User
 │
 │ RDP
 ▼
Remote Desktop
```

### Security relevance

Exposed RDP services are attractive targets for attackers.

Security measures can include:

- Strong authentication
- Multi-factor authentication
- Network-level controls
- VPN or private access
- Account lockout policies
- Monitoring

---

# 🧭 NTP

**Network Time Protocol**

```text
UDP 123
```

NTP synchronizes system clocks.

```text
Time Server
     │
     ▼
Client System
     │
     ▼
Correct System Time
```

Accurate time is extremely important in cybersecurity because logs often need to be correlated across multiple systems.

---

# 🖨️ SNMP

**Simple Network Management Protocol**

Commonly:

```text
UDP 161
```

SNMP is used for monitoring and managing network devices.

For example:

```text
Monitoring System
       │
       ▼
    Switch
       │
       ▼
    Router
```

SNMP traps commonly use:

```text
UDP 162
```

---

# 🔄 ICMP

**Internet Control Message Protocol**

ICMP does not use TCP or UDP ports.

It is used for network control, diagnostics, and error reporting.

For example:

```bash
ping example.com
```

Ping commonly uses ICMP Echo Request and Echo Reply messages.

Therefore:

```text
ICMP ≠ TCP
ICMP ≠ UDP
```

And:

```text
ICMP → No port number
```

---

# 🧠 Important Protocol & Port Table

| Protocol | Purpose | Common Port | Transport |
|---|---|---:|---|
| SSH | Secure remote access | 22 | TCP |
| FTP | File transfer | 20/21 | TCP |
| SFTP | Secure file transfer | 22 | TCP |
| Telnet | Remote terminal | 23 | TCP |
| SMTP | Email sending/relay | 25 | TCP |
| DNS | Name resolution | 53 | UDP/TCP |
| DHCP | Network configuration | 67/68 | UDP |
| HTTP | Web communication | 80 | TCP |
| POP3 | Email retrieval | 110 | TCP |
| IMAP | Email access | 143 | TCP |
| HTTPS | Secure web communication | 443 | TCP |
| SMB | File/printer sharing | 445 | TCP |
| LDAP | Directory services | 389 | TCP/UDP |
| LDAPS | LDAP over TLS | 636 | TCP |
| RDP | Remote desktop | 3389 | TCP |
| NTP | Time synchronization | 123 | UDP |
| SNMP | Network management | 161 | UDP |

> Port assignments can have multiple valid variants depending on the protocol version and configuration. Treat this table as a learning reference, not an exhaustive port registry.

---

# 🧠 Protocol vs Port

These concepts are related but different.

### Protocol

Defines **how communication works**.

Example:

```text
HTTP
```

### Port

Identifies a communication endpoint associated with a service.

Example:

```text
443
```

So:

```text
HTTPS
   +
TCP 443
```

does not mean that "443 is HTTPS."

It means HTTPS commonly operates using TCP port 443.

---

# 🔥 Why Ports Matter in Cybersecurity

Ports help security professionals understand what services may be exposed on a system.

For example:

```text
Target
 │
 ├── 22   → SSH
 ├── 80   → HTTP
 ├── 443  → HTTPS
 └── 3389 → RDP
```

An open port does not automatically mean a vulnerability exists.

It means that a service may be reachable.

The next questions are:

```text
What service is running?
What version is it?
Is it required?
Is it securely configured?
Is it patched?
Who can access it?
```

---

# 🔎 Port Scanning

A port scanner can check which ports are reachable on a target.

One commonly used tool is:

```text
Nmap
```

Example for an authorized lab system:

```bash
nmap 192.168.1.10
```

Specific ports:

```bash
nmap -p 22,80,443 192.168.1.10
```

Service detection:

```bash
nmap -sV 192.168.1.10
```

⚠️ Only scan systems you own or have explicit permission to test.

---

# 🐧 Linux Port Inspection

You can inspect local sockets using:

```bash
ss -tuln
```

Remember:

```text
-t → TCP
-u → UDP
-l → Listening
-n → Numeric output
```

For more information about listening processes:

```bash
sudo ss -tulpn
```

---

# 🔍 Understanding a Listening Port

Suppose you see:

```text
TCP 0.0.0.0:22 LISTEN
```

This indicates that a TCP service is listening on port 22 on the available IPv4 interfaces represented by `0.0.0.0`.

Conceptually:

```text
Network
   │
   ▼
Port 22
   │
   ▼
SSH Service
```

You should then determine whether the service is actually needed and appropriately protected.

---

# 🛡️ Attack Surface

Every exposed service can contribute to a system's **attack surface**.

Example:

```text
Server
 │
 ├── 22  SSH
 ├── 80  HTTP
 ├── 443 HTTPS
 └── 3389 RDP
```

If a service is unnecessary:

```text
Disable / remove it
        ↓
Smaller attack surface
```

But simply closing ports is not a substitute for proper security.

---

# 🚨 Common Security Risks

Poorly secured network services can lead to:

- Unauthorized access
- Credential attacks
- Information disclosure
- Exploitation of vulnerable software
- Lateral movement
- Data exposure
- Denial-of-service attacks

Examples:

```text
Exposed SSH
     ↓
Credential attacks

Outdated web server
     ↓
Potential exploitation

Exposed SMB
     ↓
Increased attack surface
```

---

# 🧪 Practical Exercise

On your Linux system, run:

```bash
ss -tuln
```

Record:

```text
Protocol
Local Address
Port
State
```

Then investigate each listening service.

Ask:

```text
What service is using this port?
Why is it running?
Does it need to be accessible?
Is it securely configured?
```

---

# 🧪 Port Matching Practice

Try matching these:

```text
22
53
67
68
80
123
143
443
445
3389
```

with:

```text
DNS
DHCP Server
DHCP Client
HTTP
HTTPS
SSH
IMAP
SMB
RDP
NTP
```

### Answers

```text
22   → SSH
53   → DNS
67   → DHCP Server
68   → DHCP Client
80   → HTTP
123  → NTP
143  → IMAP
443  → HTTPS
445  → SMB
3389 → RDP
```

---

# 🌐 Connecting Everything I've Learned

The networking roadmap is now becoming one connected system.

Imagine opening a website:

```text
DHCP
  ↓
Your device gets network configuration
  ↓
DNS
  ↓
Domain becomes an IP address
  ↓
NAT/PAT
  ↓
Private network communicates externally
  ↓
TCP
  ↓
Transport connection
  ↓
TLS
  ↓
Secure communication
  ↓
HTTPS
  ↓
Web request
  ↓
Server response
```

This is how the individual topics begin to fit together.

---

# 🔐 Cybersecurity Perspective

When investigating a system, understanding protocols and ports helps answer:

```text
What services are exposed?
        ↓
Which protocols are being used?
        ↓
Which ports are reachable?
        ↓
Are the services necessary?
        ↓
Are they securely configured?
        ↓
Are there suspicious connections?
```

This is foundational knowledge for areas such as:

- Network security
- SOC analysis
- Incident response
- Vulnerability assessment
- Penetration testing
- Digital forensics
- Threat detection
