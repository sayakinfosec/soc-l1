# Pyramid of Pain  
A structured overview of indicators, difficulty levels, examples, and practical analysis.

---

## 1. Introduction  
The Pyramid of Pain is a foundational concept used across cybersecurity solutions such as **Cisco Security**, **SentinelOne**, and **SOCRadar**. It enhances the effectiveness of **Cyber Threat Intelligence (CTI)**, **Threat Hunting**, and **Incident Response**.

Understanding each level of the pyramid helps Threat Hunters, SOC Analysts, and Incident Responders prioritize detection efforts and disrupt adversaries more effectively.

---

## 2. Hash Values (Trivial)

### 2.1 Overview  
Hash values uniquely identify files using algorithms such as **MD5**, **SHA-1**, and **SHA-256**. Hashes are widely used by security professionals to reference malware samples and validate file integrity.

### 2.2 Why They’re Trivial  
Even a **one-bit** change in a file completely alters the hash. Attackers can bypass hash-based detection simply by modifying the file slightly.

### 2.3 Demonstration  
Modifying a file with:  
```powershell
echo "AppendTheHash" >> file.msi
````

immediately changes its MD5 hash.

### 2.4 Useful Tools

* VirusTotal
* MetaDefender (OPSWAT)

### 2.5 Q&A

**Filename of the sample (given hash report):** `Sales_Receipt 5606.xls`

---

## 3. IP Addresses (Easy)

### 3.1 Overview

IP addresses identify devices across networks. Blocking malicious IPs is a basic defensive tactic, but attackers circumvent this easily by rotating IPs.

### 3.2 Fast Flux

Attackers use **Fast Flux** to dynamically rotate multiple IPs behind a domain, making blocking efforts ineffective.

### 3.3 Q&A

* **First IP contacted by PID 1632:** `50.87.136.52`
* **First domain contacted by PID 1632:** `craftingalegacy.com`

---

## 4. Domain Names (Simple)

### 4.1 Overview

Domains are harder for attackers to change than IPs because they require registration and DNS modifications. Still, automation and weak registrar policies make the process easier.

### 4.2 Punycode Attacks

Attackers use Unicode characters to mimic legitimate domains.
Example:

* Malicious: `adıdas.de`
* Punycode: `xn--addas-o4a.de`

### 4.3 URL Shorteners

Shortened URLs often hide malicious destinations. Add a **+** to preview:
`tinyurl.com/abc123+`

### 4.4 Q&A

* **First suspicious domain:** `craftingalegacy.com`
* **Term for website address:** *Domain Name*
* **Attack using Unicode mimicry:** *Punycode attack*
* **Preview of shortened URL:** `https://tryhackme.com/`

---

## 5. Host Artifacts (Annoying)

### 5.1 Overview

Host artifacts include:

* Registry modifications
* Suspicious processes
* Dropped files
* Execution patterns

Detecting these forces attackers to reconfigure or rebuild their malware.

### 5.2 Q&A

* **IP receiving POST request:** `96.126.101.6`
* **Dropped malicious executable:** `G_jugk.exe`
* **VirusTotal malicious vendor count:** `9`

---

## 6. Network Artifacts (Annoying)

### 6.1 Overview

Network artifacts include:

* User-Agent strings
* C2 URI patterns
* POST request structures
* PCAP signatures

Unique or unusual User-Agent strings often reveal malware.

### 6.2 Q&A

* **Browser using shown User-Agent:** *Internet Explorer*
* **Number of POST requests in screenshot:** `6`

---

## 7. Tools (Challenging)

### 7.1 Overview

At this stage, detection targets the **tools** adversaries rely on-custom malware, packers, droppers, RATs, malicious macros, etc.
Detecting tools forces attackers to invest significant time and money to rebuild capabilities.

### 7.2 Fuzzy Hashing

Used to compare similarity between files despite small changes.
Example: **SSDeep**

### 7.3 Q&A

* **Similarity method:** *Fuzzy Hashing*
* **Full name for fuzzy hashing:** *Context Triggered Piecewise Hashes*

---

## 8. TTPs (Tough)

### 8.1 Overview

The top of the pyramid: **Tactics, Techniques & Procedures**.
Covers entire adversary tradecraft across the MITRE ATT&CK framework.

Detecting TTPs significantly disrupts adversaries, often forcing them to abandon operations.

### 8.2 Q&A

* **Number of MITRE Exfiltration techniques:** `9`
* **Remote access tool used by Chimera:** *Cobalt Strike*

---

## 9. Summary  

The Pyramid of Pain highlights how different types of indicators affect an attacker’s ability to operate. The higher you detect, the more pain you inflict on the adversary.

### Layers of the Pyramid (Top → Bottom):
- **TTPs (Tough)**
- **Tools (Challenging)**
- **Network Artifacts (Annoying)**
- **Host Artifacts (Annoying)**
- **Domain Names (Simple)**
- **IP Addresses (Easy)**
- **Hash Values (Trivial)**

Focusing detection on the upper layers - Host Artifacts, Network Artifacts, Tools, and TTPs - delivers maximum disruption and forces attackers to invest time, resources, and effort into rebuilding their operations.

