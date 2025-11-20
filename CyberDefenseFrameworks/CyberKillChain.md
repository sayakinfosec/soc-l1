# Cyber Kill Chain  
A structured overview of all phases, attacker perspective, tools, and Q&A.


## 1. Introduction  

The **Cyber Kill Chain®**, created by Lockheed Martin in 2011, is based on the military “kill chain” concept.  
It breaks down the **sequence of steps** an adversary must go through to successfully execute a cyber attack.

Understanding the Kill Chain helps SOC Analysts, Threat Hunters, Incident Responders, and Security Researchers:

- Identify missing security controls  
- Detect intrusions early  
- Understand attacker goals and techniques  
- Protect against APTs, breaches, and ransomware attacks  

This room explores the **7 phases** of the Cyber Kill Chain:

1. Reconnaissance  
2. Weaponization  
3. Delivery  
4. Exploitation  
5. Installation  
6. Command & Control  
7. Actions on Objectives  

---

## 2. Reconnaissance  

Reconnaissance is the **research and planning phase**.  
Attackers gather information about the target through OSINT, scanning, and public data.

### 2.1 OSINT Sources  
- Search engines  
- Media sites  
- Social networks  
- Forums & blogs  
- Public record databases  
- WHOIS & DNS data  

### 2.2 Types of Recon  
- **Passive Recon:** No direct interaction  
  (WHOIS lookups, social scraping, breach databases)  
- **Active Recon:** Direct probing  
  (scanning, banner grabbing, social engineering)

### 2.3 Tooling Examples  
- **theHarvester** - email, names, subdomains, IPs  
- **Hunter.io** - domain-related email discovery  
- **OSINT Framework** - a web-based interface to OSINT tools  

### Q&A  
- *Intel gathering tool with web-based interface:* **OSINT Framework**  
- *Email-gathering process:* **Email Harvesting**

---

## 3. Weaponization  

The attacker turns collected info into **malicious tools**, exploits, and payloads.

### 3.1 Key Terms  
- **Malware** - software intended to damage or compromise  
- **Exploit** - code leveraging vulnerabilities  
- **Payload** - malicious code executed on the system  

### 3.2 Weaponization Techniques  
- Malicious Office documents with macros/VBA  
- Dropping infected USB drives  
- Setting up C2 servers  
- Installing backdoors  
- Crafting phishing templates  

### Q&A  
- *Automated scripts in Office documents:* **Macro**

---

## 4. Delivery  

The attacker chooses the **method to deliver the payload** to the target.

### 4.1 Common Delivery Methods  
- **Phishing Emails** - links or malicious attachments  
- **USB Drop Attacks** - infected physical media  
- **Watering Hole Attacks** - compromising frequently visited websites  

### Q&A  
- *Attack infecting a group via their common website:* **Watering Hole Attack**

---

## 5. Exploitation  

The attacker's code **executes on the target** by exploiting vulnerabilities.

### 5.1 Common Exploitation Methods  
- Malicious macro execution  
- **Zero-day exploits** (unknown vulnerabilities)  
- **Known CVEs** that remain unpatched  

### 5.2 Signs of Exploitation  
- Unexpected process creation  
- New services or registry changes  
- Suspicious command-line usage  

### Q&A  
- *Attack exploiting unknown software vulnerability:* **Zero-day**

---

## 6. Installation  

The attacker establishes **persistence** to maintain long-term access.

### Persistence Methods  
- **Web Shells** (malicious scripts on servers)  
- **Backdoors** (e.g., Meterpreter)  
- **Windows Services manipulation** (MITRE T1543.003)  
- **Registry Run Keys / Startup folder** entries  
- **Timestomping** to hide file modifications  

### Q&A  
- *Technique modifying file timestamps:* **Timestomping**  
- *Malicious script on web servers for persistent access:* **Web Shell**

---

## 7. Command & Control (C2)  

The attacker establishes remote **communication channels** with the compromised host.

### Common C2 Channels  
- **HTTP/HTTPS** (blends with normal traffic)  
- **DNS Tunneling** (constant DNS requests to attacker's server)  
- Legacy IRC (rare today)

### Q&A  
- *C2 communication using regular DNS requests:* **DNS Tunneling**

---

## 8. Actions on Objectives (Exfiltration)  

The final phase where the attacker executes their **end goals**.

### Common Objectives  
- Credential harvesting  
- Privilege escalation  
- Internal reconnaissance  
- Lateral movement  
- Data collection & exfiltration  
- Deleting backups & shadow copies  
- Data corruption or destruction  

### Q&A  
- *Microsoft technology creating snapshots/backups:* **Shadow Copy**

---

## 9. Summary  

The Cyber Kill Chain provides a **full view of an attacker’s workflow**.  
Stopping an adversary **at any phase** breaks their entire attack path.

### Kill Chain Phases (Start → End)
- **Reconnaissance**  
- **Weaponization**  
- **Delivery**  
- **Exploitation**  
- **Installation**  
- **Command & Control**  
- **Actions on Objectives**  

Defenders benefit most by detecting and blocking attackers **early in the chain**, ideally before exploitation or persistence occurs.
