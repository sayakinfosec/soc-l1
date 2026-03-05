## DetectingWebAttacks
### Introduction
Web attacks are one of the most common ways attackers gain access to systems. Public-facing web applications often sit in front of sensitive infrastructure such as databases, making them attractive targets. Detecting these attacks requires analyzing logs, network traffic, and understanding common web attack patterns.

### Objectives
- Learn common **client-side and server-side web attacks**
- Understand the **benefits and limitations of log-based detection**
- Explore **network traffic-based detection techniques**
- Understand the role of **Web Application Firewalls (WAF)**
- Practice identifying attacks using **logs and packet captures**

---

### Client-Side Attacks
Client-side attacks exploit weaknesses in **user behavior, browsers, or user devices**. Instead of attacking the server directly, attackers target the **user’s browser environment** to execute malicious actions.

These attacks often rely on:
- Malicious scripts
- Social engineering
- Exploiting browser vulnerabilities
- Injecting malicious third-party content

A typical scenario involves a malicious script embedded within a webpage that silently executes in the user’s browser and steals session cookies or sensitive information.

### SOC Visibility Limitations
From a **SOC analyst perspective**, client-side attacks are difficult to detect because they occur inside the user’s browser.

Security teams typically rely on:
- Server logs
- Network traffic monitoring

However, these tools provide **little to no visibility into browser activity**, making many client-side attacks invisible without:
- Endpoint monitoring
- Browser security controls
- Client-side security solutions

### Common Client-Side Attacks

**Cross-Site Scripting (XSS)**  
Malicious JavaScript is injected into a trusted website and executed in the victim’s browser.

Example payload:
```
<script>alert('You have been hacked');</script>
```

Possible impact:
- Session hijacking
- Cookie theft
- Account takeover

**Cross-Site Request Forgery (CSRF)**  
The victim’s browser is tricked into sending unauthorized requests to a web application where they are already authenticated.

**Clickjacking**  
Attackers place invisible elements over legitimate webpage components to trick users into clicking unintended actions.

### Key Takeaway
- Client-side attacks exploit **user behavior or browser vulnerabilities**
- **XSS** is the most common client-side web attack

---

### Server-Side Attacks
Server-side attacks exploit vulnerabilities in:
- Web servers
- Application code
- Backend services
- Databases

Unlike client-side attacks, server-side attacks target the **application infrastructure itself**.

Many web applications process **user input through forms**, such as:
- Login forms
- Search queries
- Account management pages

Improper handling of this input can lead to serious vulnerabilities.

### Detecting Server-Side Attacks
Server-side attacks leave **observable traces**, making them easier to detect compared to client-side attacks.

Evidence sources include:
- Web server logs
- Application logs
- Network traffic captures

By analyzing these sources, analysts can identify:
- Suspicious request patterns
- Exploit attempts
- Unauthorized access behavior

### Common Server-Side Attacks

**Brute Force Attack**  
Attackers repeatedly attempt login credentials using automated tools.

Indicators:
- Multiple rapid login attempts
- Repeated POST requests
- Authentication failures followed by success

**SQL Injection (SQLi)**  
Occurs when applications construct database queries using unsanitized user input.

Example payload:
```
' OR '1'='1
```

Impact:
- Database data extraction
- Authentication bypass
- Data modification

**Command Injection**  
User input is passed directly to the operating system without proper validation.

Attackers can execute system commands with the application's privileges.

### Key Takeaway
- Server-side attacks target **application infrastructure**
- **SQL Injection** is one of the most critical server-side vulnerabilities

---

### Log-Based Detection
Web server **access logs** are valuable for detecting malicious activity because every request made to the server can leave a trace.

Security analysts can identify:
- Attack patterns
- Exploitation attempts
- Automated scanning behavior

### Typical Access Log Fields

| Field | Description | Suspicious Indicators |
|------|-------------|----------------------|
| Client IP | Source of request | Known malicious IP |
| Timestamp | Time of request | Unusual frequency |
| Requested Page | URL requested | Sensitive endpoints |
| Status Code | Server response | Repeated errors |
| Response Size | Size of returned data | Abnormal response sizes |
| Referrer | Origin page | Unexpected sources |
| User-Agent | Client identifier | Attack tools |

Common malicious user agents include:
- sqlmap
- wpscan
- ffuf

### Example Attack Sequence in Logs
A typical attack chain may appear as:

1. **Directory Fuzzing**
   - Attacker scans directories
   - Successful responses return HTTP **200**

2. **Brute Force Login**
   - Repeated POST requests to `/login.php`
   - One request returns **302 redirect** indicating successful login

3. **SQL Injection Attempts**
   - Malicious query strings used in search or form fields
   - Payloads like `' OR '1'='1`

### Log Limitations
While useful, logs have important limitations.

Access logs often **do not record request bodies**, meaning analysts cannot see:
- Submitted passwords
- POST data
- Full payloads

Example log entry:
```
10.10.10.100 [12/Aug/2025:14:32:10] "POST /login HTTP/1.1" 200 532 "/home.html" "Mozilla/5.0"
```

This entry shows the request occurred but **not the credentials used**.

### Key Investigation Findings
- Directory fuzzing tool used: **FFUF v2.1.0**
- Brute force target page: **/login.php**
- SQL injection payload used:

```
%' OR '1'='1
```

---

### Network-Based Detection
Network traffic analysis allows analysts to inspect **raw packets exchanged between client and server**.

Tools like **Wireshark** provide visibility into:
- HTTP headers
- Cookies
- POST request bodies
- Uploaded files
- Server responses

Compared to logs, packet captures provide **much deeper visibility**.

### Encryption Limitations
Protocols like:
- HTTPS
- SSH

Encrypt packet contents, preventing payload inspection unless:
- Decryption keys are available
- TLS inspection is performed

For analysis exercises, HTTP traffic is typically used.

### Detecting Attacks in Packet Captures
Network traffic reveals the full attack chain:

1. **Directory fuzzing requests**
2. **Brute force login attempts**
3. **SQL injection exploitation**

Unlike logs, packet captures allow analysts to view **actual credentials and payloads** used in attacks.

### Investigation Findings

Successful brute-force password:

```
astrongpassword123
```

SQL injection revealed database flag:

```
THM{dumped_the_db}
```

### Key Takeaway
Network traffic analysis allows analysts to:
- See **complete request payloads**
- Identify **actual credentials used**
- Observe **database responses**

---

### Web Application Firewall (WAF)
A **Web Application Firewall (WAF)** protects web applications by inspecting incoming HTTP requests before they reach the server.

It acts as a **security gatekeeper**, analyzing requests and blocking malicious activity.

WAFs can also:
- Decrypt TLS traffic
- Inspect full HTTP packets
- Apply filtering rules

### WAF Rule Types

**Block Common Attack Patterns**
- Detect known malicious payloads
- Example: block SQL injection patterns

**Deny Known Malicious Sources**
- Block traffic from malicious IP addresses
- Use threat intelligence feeds

**Custom Security Rules**
- Restrict allowed request types
- Example: allow only GET/POST on login pages

**Rate Limiting**
- Prevent abuse such as brute force attacks
- Example: limit login attempts per IP

### Example Custom Rule

```
IF User-Agent CONTAINS "sqlmap"
THEN BLOCK
```

### Challenge-Response Mechanisms
Instead of blocking traffic outright, WAFs can challenge suspicious requests using:

- CAPTCHA
- Bot verification
- Behavioral analysis

This helps reduce **false positives** while preventing automated attacks.

### Threat Intelligence Integration
Modern WAFs integrate with **global threat intelligence feeds** to automatically block:

- Known botnet IPs
- Malicious proxies
- Attack tool signatures
- Exploited CVEs

### Example Firewall Rule

```
IF User-Agent CONTAINS "BotTHM"
THEN BLOCK
```

### Key Takeaway
WAFs inspect and filter **web requests** before they reach the application server.

---

### Conclusion
Detecting web attacks requires correlating multiple data sources.

Key detection layers include:
- **Client-side attack awareness**
- **Server log analysis**
- **Network packet inspection**
- **Web Application Firewall protection**

By combining log analysis, network traffic investigation, and defensive controls such as WAFs, analysts can develop a **stronger and more effective detection strategy** against web-based attacks.
