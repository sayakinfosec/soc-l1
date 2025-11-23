### MITRE

---

### Introduction ✨

MITRE is a not-for-profit organization working across cybersecurity, AI, healthcare, and more. In this room, you explore its major cybersecurity frameworks: **ATT&CK®, CAR, D3FEND, Engage™, Caldera**, and others.

**Learning Objectives:**

* Understand ATT&CK® structure and purpose
* Learn how security teams use ATT&CK
* Use CTI + ATT&CK to profile threats
* Explore CAR, D3FEND, ATLAS, AADAPT

---

### ATT&CK® Framework

MITRE ATT&CK® is a global knowledge base of real-world adversary behavior.

**TTP Breakdown:**

* **Tactic:** The *why*
* **Technique:** The *how*
* **Procedure:** The specific execution

**Coverage:** Windows, macOS, Linux, Cloud, Mobile, ICS.

**Matrix Example:**

* **Tactic:** Reconnaissance
* **Technique:** Active Scanning
* **Sub-techniques:** IP Block Scanning, Vulnerability Scanning, Wordlist Scanning

---

### ATT&CK in Operation

Why ATT&CK matters: standard terminology, mapping threat intel, building detections.

**Who Uses It:**

* CTI Teams → map threat actor behavior
* SOC Analysts → add context to alerts
* Detection Engineers → align SIEM/EDR rules
* Incident Responders → map attack timelines
* Red/Purple Teams → build adversary emulation

---

### Case Study: Mustang Panda (G0129)

A threat group known for targeting governments and NGOs.

**Mapped Behaviors:**

* Phishing for Initial Access
* Scheduled Tasks for Persistence
* Obfuscation for Defense Evasion
* Ingress Tool Transfer for C2

---

### ATT&CK for Threat Intelligence

Scenario: Analyst in aviation sector researching APTs.

**Example Findings:**

* APT targeting aviation since 2013 → **APT33**
* Key Office365 concern → **Cloud Accounts sub-technique**
* Related tool → **Ruler**
* Mitigation → **User Account Management**
* Detection Strategy → **DET0546**

---

### Cyber Analytics Repository (CAR)

CAR is a set of ATT&CK-aligned detection analytics.

Each analytic contains:

* Description
* Mapped tactics/techniques
* Pseudocode
* SIEM queries (Splunk, EQL, LogPoint)
* Sometimes unit tests

Example: **CAR-2020-09-001: Scheduled Task - File Access**

---

### MITRE D3FEND

D3FEND focuses on defensive techniques.

**Seven Tactics:** Model, Harden, Detect, Isolate, Deceive, Evict, Restore.

Example: **Credential Rotation (D3-CRO)** — regularly rotate credentials to reduce reuse risk.

---

### Other MITRE Projects

**Emulation Plans:** Real-world adversary emulations.

**Caldera:** Automated adversary emulation tool.

**AADAPT:** Framework for digital asset (blockchain) threats.

* Example: Scrape Blockchain Data → **ADT3025**

**ATLAS:** Framework for AI/ML security.

* Example: LLM Prompt Obfuscation → Defense Evasion 🛡️
