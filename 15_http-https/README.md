# 🌐 HTTP & HTTPS

> **Understanding how web browsers, servers, and applications communicate across the internet.**

---

## 🧠 What is HTTP?

**HTTP (Hypertext Transfer Protocol)** is an application-layer protocol used for communication between clients and servers.

It is one of the fundamental protocols of the web.

A simple web request looks like:

```text
Browser
   │
   │ HTTP Request
   ▼
Web Server
   │
   │ HTTP Response
   ▼
Browser
```

HTTP is used to transfer resources such as:

- HTML pages
- CSS
- JavaScript
- Images
- JSON data
- API responses
- Other web resources

---

# 🌐 Client and Server

Web communication usually involves two sides.

### Client

The client requests a resource.

Examples:

- Web browser
- Mobile application
- API client

### Server

The server receives requests and sends responses.

Examples:

- Web server
- Application server
- API server

```text
        Client
           │
           │ Request
           ▼
        Server
           │
           │ Response
           ▼
        Client
```

---

# 🔄 HTTP Request & Response

HTTP communication follows a request-response model.

```text
CLIENT                         SERVER

  │
  │──── HTTP Request ─────────►│
  │                            │
  │                            │
  │◄──── HTTP Response ────────│
  │
```

For example:

```text
GET /index.html HTTP/1.1
```

The server may respond with:

```text
HTTP/1.1 200 OK
```

---

# 📤 HTTP Request

An HTTP request can contain:

```text
Request Method
URL / Path
HTTP Version
Headers
Body
```

Example:

```http
GET /login HTTP/1.1
Host: example.com
User-Agent: Browser
Accept: text/html
```

---

# 📥 HTTP Response

An HTTP response can contain:

```text
HTTP Version
Status Code
Headers
Body
```

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html

<html>
...
</html>
```

---

# 🔤 HTTP Methods

HTTP methods describe what the client wants to do.

Common methods include:

| Method | Purpose |
|---|---|
| GET | Retrieve data |
| POST | Submit/create data |
| PUT | Replace/update a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |
| HEAD | Retrieve headers without the response body |
| OPTIONS | Discover supported communication options |

---

# 🔎 GET

`GET` is commonly used to retrieve information.

Example:

```http
GET /products HTTP/1.1
```

Conceptually:

```text
Client
  │
  │ "Give me the products."
  ▼
Server
  │
  │ Product data
  ▼
Client
```

---

# 📤 POST

`POST` is commonly used to submit data to a server.

Example:

```http
POST /login HTTP/1.1
```

The request may contain data in its body.

For example:

```text
username=student
password=example
```

⚠️ Never use real passwords in practice examples or learning labs.

---

# ✏️ PUT and PATCH

Both can be used to update resources.

### PUT

Typically replaces the representation of a resource.

```http
PUT /users/10
```

### PATCH

Typically modifies part of a resource.

```http
PATCH /users/10
```

The exact behavior depends on how the application API is designed.

---

# 🗑️ DELETE

`DELETE` is commonly used to request removal of a resource.

Example:

```http
DELETE /users/10
```

---

# 📊 HTTP Status Codes

HTTP responses contain status codes that describe the result.

They are grouped into five categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

---

## 🟢 2xx — Success

### 200 OK

The request succeeded.

```text
200 OK
```

### 201 Created

A resource was successfully created.

```text
201 Created
```

### 204 No Content

The request succeeded but there is no response body.

---

## 🔵 3xx — Redirection

### 301 Moved Permanently

The resource has been permanently moved.

### 302 Found

The server is redirecting the client.

### 304 Not Modified

The cached version can still be used.

---

## 🟠 4xx — Client Errors

### 400 Bad Request

The request is invalid or malformed.

### 401 Unauthorized

Authentication is required or has not been successfully provided.

### 403 Forbidden

The server understood the request but refuses to authorize it.

### 404 Not Found

The requested resource could not be found.

---

## 🔴 5xx — Server Errors

### 500 Internal Server Error

A general server-side error occurred.

### 502 Bad Gateway

A server acting as a gateway received an invalid response from an upstream server.

### 503 Service Unavailable

The server is temporarily unable to handle the request.

---

# 🧠 401 vs 403

This distinction is important in cybersecurity.

### 401

```text
Authentication problem
```

Think:

> "You need to authenticate."

### 403

```text
Authorization problem
```

Think:

> "I know who you are, but you're not allowed to access this."

---

# 📦 HTTP Headers

Headers provide additional information about an HTTP request or response.

Examples include:

```text
Host
User-Agent
Accept
Content-Type
Content-Length
Authorization
Cookie
Cache-Control
```

Example:

```http
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

---

# 🍪 Cookies

HTTP itself is **stateless**: each request can be handled independently.

Web applications often use **cookies** to maintain state between requests.

Example:

```text
Browser
   │
   │ Login
   ▼
Server
   │
   │ Set-Cookie
   ▼
Browser
   │
   │ Cookie
   ▼
Server
```

Cookies can be used for:

- Sessions
- Preferences
- Authentication state
- Tracking

---

# 🪪 Sessions

A server can associate a session identifier with a user's session.

Conceptually:

```text
Browser
   │
   │ Session ID
   ▼
Server
   │
   ▼
User Session
```

Session security is extremely important.

Poor session management can lead to vulnerabilities such as **session hijacking**.

---

# 📦 HTTP Request Body

Some requests contain data in their body.

For example, an API request might contain JSON:

```json
{
  "username": "student",
  "role": "user"
}
```

The `Content-Type` header tells the server what kind of data is being sent.

Example:

```http
Content-Type: application/json
```

---

# 🌍 HTTP Port

HTTP commonly uses:

```text
TCP 80
```

Example:

```text
Browser
   │
   │ TCP 80
   ▼
HTTP Server
```

---

# 🔒 What is HTTPS?

**HTTPS (HTTP Secure)** is HTTP communication protected using **TLS (Transport Layer Security)**.

Conceptually:

```text
HTTP
 +
TLS
 ↓
HTTPS
```

HTTPS helps protect communication between the client and server.

---

# 🛡️ Why HTTPS Matters

HTTPS provides important security properties including:

### 🔐 Confidentiality

Helps prevent unauthorized parties from reading protected traffic.

### 🧾 Integrity

Helps detect unauthorized modification of traffic.

### 🪪 Authentication

TLS certificates help the client authenticate the server's identity, assuming certificate validation succeeds.

```text
HTTPS
 │
 ├── Confidentiality
 ├── Integrity
 └── Authentication
```

---

# 🔑 TLS

**TLS (Transport Layer Security)** is the cryptographic protocol used to protect modern HTTPS connections.

A simplified model:

```text
Browser
   │
   │ TLS Handshake
   ▼
Web Server
   │
   │ Secure connection established
   ▼
Encrypted HTTP Data
```

Modern HTTPS uses TLS rather than the older SSL protocols.

---

# 🤝 Simplified TLS Handshake

A simplified TLS connection can be thought of as:

```text
Client
  │
  │ ClientHello
  ▼
Server
  │
  │ ServerHello + Certificate
  ▼
Client
  │
  │ Key establishment
  ▼
Secure Session
```

The actual TLS handshake is more detailed and depends on the TLS version and cryptographic configuration.

---

# 🔐 HTTP vs HTTPS

| Feature | HTTP | HTTPS |
|---|---|---|
| Security | No TLS protection | TLS protected |
| Common port | TCP 80 | TCP 443 |
| Encryption | ❌ | ✅ |
| Integrity protection | ❌ | ✅ |
| Server authentication | ❌ | ✅ via TLS certificates |
| Typical web use | Legacy/unprotected traffic | Modern web traffic |

---

# 🌐 HTTPS Port

HTTPS commonly uses:

```text
TCP 443
```

Example:

```text
Browser
   │
   │ TCP 443
   ▼
Web Server
   │
   ▼
TLS
   │
   ▼
Encrypted HTTP
```

---

# 📜 TLS Certificates

HTTPS commonly relies on digital certificates.

A certificate can contain information such as:

- Domain name
- Public key
- Certificate authority information
- Validity period
- Digital signature

The browser verifies the certificate according to its trust rules.

Conceptually:

```text
Website
   ↓
Certificate
   ↓
Certificate Authority
   ↓
Browser validates certificate
   ↓
Trusted connection
```

---

# 🏛️ Certificate Authorities

A **Certificate Authority (CA)** is an entity that issues and signs digital certificates.

Operating systems and browsers maintain trusted CA information.

This creates a chain of trust.

```text
Trusted Root CA
       ↓
Intermediate CA
       ↓
Website Certificate
       ↓
Browser
```

---

# ⚠️ HTTP Security Risks

Unprotected HTTP traffic can expose sensitive information.

Potential risks include:

- Traffic interception
- Credential exposure
- Session theft
- Content modification
- Man-in-the-middle attacks

For example:

```text
User
 │
 │ Unprotected HTTP
 ▼
Network
 │
 ▼
Server
```

An attacker positioned appropriately on the network may be able to observe or manipulate unencrypted traffic.

---

# 🛡️ HTTPS and Man-in-the-Middle Attacks

HTTPS helps defend against attackers attempting to intercept and modify communication.

Conceptually:

```text
Client
   │
   │ Encrypted TLS traffic
   ▼
Internet
   │
   ▼
Server
```

However, HTTPS security depends on correct TLS configuration and proper certificate validation.

HTTPS does **not** automatically make the website itself trustworthy.

A malicious website can also use HTTPS.

---

# 🔎 HTTP & Cybersecurity

HTTP/HTTPS knowledge is extremely important in cybersecurity because web applications are a major part of modern infrastructure.

Security professionals analyze:

- Requests
- Responses
- Headers
- Cookies
- Sessions
- Status codes
- Authentication
- APIs
- TLS certificates
- Web traffic

Understanding normal HTTP behavior makes unusual behavior easier to recognize.

---

# 🕵️ Common Web Security Concepts

HTTP knowledge forms the foundation for understanding vulnerabilities such as:

- Cross-Site Scripting (XSS)
- SQL Injection
- Cross-Site Request Forgery (CSRF)
- Broken authentication
- Broken access control
- Session-related attacks
- Insecure API behavior

These vulnerabilities are application-level issues; understanding HTTP helps explain how the attacks interact with web applications.

---

# 🔍 Inspecting HTTP with Browser Developer Tools

Modern browsers provide developer tools that allow you to inspect web traffic.

Open:

```text
Developer Tools
      ↓
Network
      ↓
Reload page
      ↓
Inspect requests
```

You can often see:

```text
Request URL
Method
Status Code
Request Headers
Response Headers
Cookies
Response Data
Timing
```

This is one of the best ways to understand HTTP practically.

---

