## Windows Logging For SOC

### Introduction

SOC analysts rely heavily on logs to triage alerts, hunt threats, and investigate incidents. Understanding how Windows logs work, how to interpret them, and what malicious activity looks like is a foundational skill for SOC and DFIR roles.

This room introduces key Windows logging sources such as Security logs, Sysmon, and PowerShell, and prepares you to analyze them in real-world scenarios.

---

### Learning Objectives

* Understand how to locate and interpret Windows event logs
* Learn key log sources like Security logs, Sysmon, and PowerShell
* Prepare for log analysis in SOC environments and labs
* Practice analyzing real event log datasets

---

### What is Logged?

Windows logs events whenever actions occur on the system, such as logins, file creation, or process execution. These logs are stored in EVTX format under `C:\Windows\System32\winevt\Logs`.

Each log entry includes:

* Timestamp (system time)
* Event ID (unique identifier)
* User/account involved
* Action details

Event Viewer is used to analyze logs, providing:

* Log sources (Application, Security, etc.)
* Event list with sortable fields
* Detailed event data (XML/plaintext)
* Filtering and search capabilities

Logs are essential for:

* Incident response
* Threat hunting
* Alerting and detection

Key answer:

* Successful login event: **Security / 4624**

---

### Security Log Authentication

The Security log is the most valuable default Windows log for SOC analysts, especially for authentication events.

Important Event IDs:

* **4624** → Successful login
* **4625** → Failed login

Key fields to analyze:

* Logon Type (3 = network, 10 = RDP)
* Username
* Source IP / hostname
* Logon ID (session identifier)

Detection techniques:

* Brute force → multiple failed logins (4625)
* Password spraying → many usernames attempted
* Suspicious IPs or hostnames
* Unusual workstation names

RDP analysis:

* Look for Logon Type 10
* Correlate with preceding Logon Type 3
* Track activity using Logon ID

Key answers:

* Attacker IP: **10.10.53.248**
* Compromised user: **Administrator**
* Logon ID: **0x183C36D**

---

### Security Log User Management

User management logs help detect persistence and privilege escalation.

Important Event IDs:

* 4720 / 4722 / 4738 → user created/enabled/modified
* 4725 / 4726 → user disabled/deleted
* 4723 / 4724 → password changed/reset
* 4732 / 4733 → group membership changes

Event structure:

* Subject → who performed the action
* Object → target user/account
* Details → changes made

Detection techniques:

* Unknown or suspicious user creation
* Privileged group additions
* Activity during off-hours
* Naming inconsistencies

Correlation:

* Use Logon ID to link with login events

Key answers:

* Created user: **svc_sysrestore**
* Privileged groups: **Backup Operators, Remote Desktop Users**
* Logon ID match: **Yea**

---

### Sysmon Process Monitoring

Process monitoring provides deep visibility into system activity.

Two approaches:

* Event ID 4688 → basic process logging (disabled by default)
* Sysmon Event ID 1 → advanced logging (recommended)

Sysmon provides:

* Process details (image, command line)
* Parent process info
* File hashes and signatures
* User context with Logon ID

Detection techniques:

* Suspicious file paths (Temp, Public)
* Random or unusual filenames
* Malicious hashes
* Unusual parent-child relationships

Process tracing:

* Follow parent process chain
* Correlate using Process ID and Logon ID

Key answers:

* Browser used: **Google Chrome**
* Downloaded file: **C:\Users\sarah.miller\Downloads\ckjg.exe**
* Download URL: **http ://gettsveriff.com/bgj3/ckjg.exe**

---

### Sysmon Files & Network

Sysmon also logs file, registry, and network activity for deeper investigation.

Important Event IDs:

* 11 / 13 → file creation / registry changes
* 3 / 22 → network connections / DNS queries

These logs:

* Detect malware persistence
* Identify command & control (C2) communication
* Reveal exfiltration paths

Correlation:

* Use ProcessId to link with Event ID 1 for full context

Detection techniques:

* Unexpected file creation in startup locations
* Connections to suspicious IPs
* Malicious domains

Key answers:

* Persistence file: **C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url**
* C2 server: **193.46.217.4:7777**
* Domain: **hkfasfsafg.click**

---

### PowerShell Logging Commands

PowerShell is heavily abused by attackers due to its flexibility and stealth.

Problem:

* Sysmon logs only show `powershell.exe` execution
* Commands inside PowerShell are not captured

Solution:

* PowerShell history file

Location:
`C:\Users\<USER>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt`

Features:

* Stores executed commands
* Persists across reboots
* Separate file per user

Limitations:

* No command output
* No script content visibility

Detection use cases:

* System discovery commands
* File access
* Malware downloads

Key answers:

* First command: **Get-ComputerInfo**
* Execution date: **May 18, 2025**
* Flag: **THM{it_was_me!}**

---

### Conclusion

Windows logging is essential for detecting and investigating attacks. By understanding Security logs, Sysmon, and PowerShell logging, analysts can reconstruct attack chains and identify malicious behavior.

Key takeaways:

* Master Event IDs like 4624 and 4625
* Correlate logs using Logon ID and Process ID
* Use Sysmon for deeper visibility
* Monitor PowerShell activity closely

These skills form the foundation for effective SOC analysis and incident response.
