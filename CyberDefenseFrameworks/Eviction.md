## Eviction

A concise and structured summary of the **Eviction** room on THM, focused on analysing APT28's behaviour using the **MITRE ATT&CK Navigator**.

---

### 1. Introduction

The *Eviction* room simulates real-world adversary tracking using MITRE ATT&CK. The storyline follows **Sunny**, a SOC analyst at **E‑corp**, who must investigate possible activity from **APT28**, an advanced persistent threat group known for targeting organisations with high-value data.

Using an ATT&CK Navigator layer provided in the room, Sunny must trace potential TTPs (Tactics, Techniques, and Procedures) used by the threat actor-covering reconnaissance, initial access, execution, persistence, defense evasion, discovery, lateral movement, collection, and exfiltration.

---

### 2. Task: Understand the Adversary

Below are the ATT&CK-based insights derived during the investigation.

### **Q1. Technique used for both Recon & Initial Access**

* **Spearphishing link**

APT28 frequently uses crafted phishing links to gather information and deliver malicious payloads.

### **Q2. Accounts APT Might Compromise During Resource Development**

* **Email accounts**

Threat actors often compromise legitimate email accounts to prepare phishing infrastructure.

### **Q3. Techniques for User Execution (via Social Engineering)**

* **Malicious file** and **malicious link**

These represent classic user-driven execution vectors.

### **Q4. Scripting Interpreters to Look For (Execution Stage)**

* **PowerShell** and **Windows Command Shell**

Suspicious interpreter activity often indicates post-compromise execution.

### **Q5. Registry Keys Related to Persistence**

* **Registry Run keys**

These keys enable programs to execute at startup, a common persistence mechanism.

### **Q6. System Binary Used for Proxy Execution**

* **rundll32**

APT28 frequently abuses LOLBins (Living-Off-The-Land Binaries).

### **Q7. Discovery Technique Indicated by Presence of tcpdump**

* **Network sniffing**

Capturing network traffic points to discovery or credential harvesting attempts.

### **Q8. Remote Services Exploited for Lateral Movement**

* **SMB / Windows Admin Shares**

Common lateral movement technique leveraging administrative shares.

### **Q9. High-Value Information Repository Targeted**

* **SharePoint**

APT28 likely targets organisational repositories storing intellectual property.

### **Q10. Proxies Used for Possible Exfiltration Attempts**

* **External proxy** and **multi-hop proxy**

Used to hide exfiltration traffic and circumvent blocked C2 connections.

---

### 3. Outcome

Sunny successfully mapped APT28 behaviour across MITRE ATT&CK phases and implemented defensive measures to stop the group from exfiltrating E‑corp’s intellectual property.

This room reinforces the importance of:

* Working with ATT&CK Navigator layers
* Understanding adversary TTP patterns
* Linking threat intel to SOC investigations
