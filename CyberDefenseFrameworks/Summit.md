## **Summit**

*A Complete Walkthrough & Pyramid of Pain Practical Implementation*

---

### **📌 Overview**

In this challenge, PicoSecure wants to strengthen its internal detection engineering capabilities.
We work with an external penetration tester in a purple-team loop:

* **Tester executes progressive malware samples**
* **We detect & block each sample using higher layers of the Pyramid of Pain**

Each stage maps to a specific IOC class:

1. Hashes
2. IP Addresses
3. Domains
4. Host/Registry Artifacts
5. Network Patterns
6. Exfiltration Detection (TTP-Level Sigma)

---

### **🧩 Task 1 - Challenge**

We receive malware samples, analyze them inside the Sandbox, and configure security tools:

### Tools We Use:

* Malware Sandbox
* Hash Blocklist
* Firewall Manager
* DNS Filter
* Sigma Rule Builder
* Sysmon-based rule validation
* Internal Mail system (flags delivered here)

---

### **🟥 Sample 1 - Hash Detection (Pyramid Layer: Hashes)**

### **Steps**

1. Open *sample1.exe* → “Submit for Analysis”
2. Copy SHA-256 hash
3. Navigate: **Manage Hashes**
4. Add hash to blocklist
5. Malware execution is prevented
6. New email unlocks the flag

### ✅ **Flag**

```
THM{f3cbf08151a11a6a331db9c6cf5f4fe4}
```

---

### **🟧 Sample 2 - IP Blocking (Pyramid Layer: IP Addresses)**

### **Steps**

1. Analyze *sample2.exe*
2. Network Activity shows suspicious IP:

   * `154.35.10.113`
3. Go to **Firewall Manager → Create Rule**
4. Configure:

   * Type: **Egress**
   * Source: **Any**
   * Destination: *Suspicious IP*
   * Action: **Deny**
5. Malware blocked → Email with flag

### ✅ **Flag**

```
THM{2ff48a3421a938b388418be273f4806d}
```

---

### **🟨 Sample 3 - Malware Domain Blocking (Pyramid Layer: Domain Names)**

### **Steps**

1. Analyze *sample3.exe*
2. Behaviour + Artifacts reveal:

   * Domain: `emudyn.bresonicz.info`
3. Go to **DNS Filter → Create DNS Rule**
4. Configure:

   * Category: Malware
   * Domain: *suspicious domain*
   * Action: Deny

### ✅ **Flag**

```
THM{4eca9e2f61a19ecd5df34c788e7dce16}
```

---

### **🟩 Sample 4 - Registry Modification Sigma Rule (Pyramid Layer: Host Artifacts)**

### **Findings**

Malware disables Windows Defender real-time protection.

Registry modification detected:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
DisableRealtimeMonitoring = 1
```

### **Steps**

1. Go to **Sigma Rule Builder**
2. Choose:

   * **Sysmon Event Logs**
   * **Registry Modifications**
3. Fill fields:

   * Registry Key
   * Value Name
   * Value Data: 1
   * MITRE ATT&CK: **TA0005 - Defense Evasion**
4. Validate rule → Malware detected

### ✅ **Flag**

```
THM{c956f455fc076aea829799c0876ee399}
```

---

### **🟦 Sample 5 - Network Pattern Sigma Rule (Pyramid Layer: Network/Host Artifacts)**

### **Observations from logs**

From `outgoing_connections.log`:

* Destination IP: **51.102.10.19**
* Port: **443**
* Size: **97 bytes**
* Repeats every 30 minutes

### **Steps**

1. Sigma Rule Builder
2. Choose:

   * **Sysmon Event Logs**
   * **Network Connections**
3. Fill parameters:

   * Destination IP: 51.102.10.19
   * Destination Port: 443
   * Size: 97
   * Periodic beaconing pattern
   * MITRE ATT&CK mapping: C2 communication

### **Flag**

```
THM{46b21c4410e47dc5729ceadef0fc722e}
```

---

### **🟪 Sample 6 - Exfiltration Detection Sigma (Pyramid Layer: TTPs)**

### **Observations in `commands.log`**

Malware creates and writes to:

```
%temp%\exfiltr8.log
```

### **Steps**

1. Sigma Rule Builder
2. Choose:

   * **Sysmon Event Logs**
   * **File Creation & Modification**
3. Add:

   * File Path: `%temp%`
   * Filename: `exfiltr8.log`
   * MITRE ATT&CK: **TA0010 - Exfiltration**
4. Validate rule → Detected

### **Final Flag**

```
THM{c8951b2ad24bbcbac60c16cf2c83d92c}
```

---

### **🎉 Final Notes**

We successfully:

* Blocked malware across all IOC levels
* Progressed from hash-based detection → behaviour/TTP detection
* Created Sigma rules mapping to Sysmon logs
* Reinforced Pyramid of Pain concepts in a practical lab

This room is *excellent* for anyone learning Detection Engineering & Purple Team workflows.
