## Detecting Web DDoS

### Introduction

Denial-of-Service (DoS) and Distributed Denial-of-Service (DDoS) attacks aim to disrupt or completely block access to web services by overwhelming them with traffic or resource-intensive requests. These attacks primarily target availability, making applications unusable for legitimate users.

In this room, we explore how these attacks work at the application layer, why attackers launch them, how to detect them using logs and SIEM tools, and how defenders can mitigate them effectively.

---

### Objectives

* Understand how DoS and DDoS attacks function
* Learn attacker motives behind disruptions
* Identify attack patterns in web logs
* Analyze attack scenarios using logs and SIEM
* Explore detection and mitigation strategies

---

### DoS and DDoS Attacks

Denial-of-Service (DoS) attacks use a single system to overwhelm a target, while Distributed Denial-of-Service (DDoS) attacks use a botnet of compromised devices to generate large-scale traffic.

DoS attacks may involve:

* Flooding endpoints like search or login forms
* Sending malformed or oversized inputs

DDoS attacks scale this using multiple systems, making them harder to block and more impactful.

Common attack types include:

* Slowloris → keeps connections open with partial requests
* HTTP Flood → large volume of requests
* Cache Bypass → forces origin server processing
* Oversized Queries → resource-heavy processing
* Login/Form Abuse → overload authentication systems
* Faulty Input Abuse → exploit weak validation

Key answers:

* Attack class: **Denial-of-Service**
* Bot network: **Botnet**

---

### Attack Motives

Attackers launch DoS/DDoS attacks for various reasons depending on their goals and targets.

Common motives include:

* Financial Loss → disrupt revenue-generating services
* Extortion → demand payment to stop attacks
* Hacktivism → political or ideological disruption
* Distraction → divert attention from other attacks
* Competition → harm rival businesses
* Denial of Wallet → increase operational costs
* Reputational Damage → reduce user trust

Real-world examples include:

* BBC outage (2015)
* Microsoft outages (2023, Anonymous Sudan)

Key answers:

* Loss of trust motive: **Reputational Damage**
* Microsoft attack motive: **Hacktivism**

---

### Log Analysis

Web server logs are critical for detecting DoS/DDoS attacks by revealing abnormal traffic patterns.

Key indicators include:

* High request rate → e.g., thousands of requests to `/login`
* Suspicious user-agents → curl, python scripts, outdated browsers
* Geographic anomalies → traffic from multiple global IPs
* Burst timestamps → many requests in seconds
* Server errors → spikes in 5xx (e.g., 503)
* Logic abuse → queries like `/products?limit=999999`

Attackers typically target resource-heavy endpoints such as:

* `/login`, `/search`, `/api`, `/register`, `/checkout`

Typical attack flow:

* Normal traffic → sudden spike → server overload → 503 errors

Key answers:

* Attacker IP: **203.12.23.195**
* Targeted page: **/login**
* Error code: **503**

---

### Leveraging SIEMs

SIEM platforms improve detection by enabling centralized log analysis, filtering, and correlation.

Using tools like Splunk, analysts can:

* Filter logs by fields such as URI, IP, and user-agent
* Identify traffic spikes and anomalies
* Use commands like `timechart` for visualization

Key findings from analysis:

* Most requested URI: **/search**
* Top attacking IP: **203.0.113.7**
* Botnet size: **60**
* Common user-agent: **Java/1.8.0_181**
* Peak requests per second: **207**
* First affected legitimate IP: **10.10.0.27**

---

### Defense

Effective defense against DoS/DDoS requires a layered approach across application and infrastructure.

Application-level defenses:

* Input validation to prevent abuse
* Rate limiting on critical endpoints
* Challenges like CAPTCHA and JavaScript validation

Infrastructure defenses:

* CDN → caches content and absorbs traffic
* Load balancing → distributes traffic across servers
* WAF → filters and blocks malicious requests

Advanced mitigation:

* Large-scale providers absorb massive traffic spikes
* Detection based on patterns and threat intelligence

Attackers may attempt to bypass defenses using:

* Random query parameters
* Spoofed user-agents
* Distributed IP sources

Key answers:

* Bot challenge: **CAPTCHA**
* Traffic distribution: **Load-balancing**

---

### Conclusion

DoS and DDoS attacks target availability by overwhelming web applications with malicious traffic. Detecting them requires identifying abnormal patterns such as high request rates, unusual user-agents, and spikes in server errors through logs and SIEM tools.

Defending against these attacks involves secure coding, traffic filtering, and scalable infrastructure like CDNs and WAFs. A layered defense strategy ensures systems remain resilient even under large-scale attack conditions.
