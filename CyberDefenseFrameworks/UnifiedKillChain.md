# Unified Kill Chain (UKC)

## 1. Introduction
The **Unified Kill Chain (UKC)** combines the Lockheed Martin Cyber Kill Chain + MITRE ATT&CK.  
It provides a **holistic, attacker-first view** of intrusion campaigns across **3 macro stages** and **18 phases**.

---

## 2. Why the UKC Matters
- Gives visibility into **full attack lifecycle**, not only initial compromise.
- Helps SOC analysts link alerts to **campaign-level thinking**, not isolated events.
- Useful for threat hunting, detection engineering, and adversary emulation.

---

## 3. The 18 Phases (Grouped by Stages)

### **Stage 1 — Initial Foothold**
1. **Reconnaissance** - attacker gathers information about the target.
2. **Weaponization** - creating payloads, phishing kits, malware.
3. **Delivery** - sending the malicious content (email, USB, drive-by).
4. **Social Engineering** - tricking the user into enabling the attack.
5. **Exploitation** - exploiting a vulnerability or user action.
6. **Command & Control Setup** - establishing a communication channel.
7. **Execution** - running the malicious payload.


### **Stage 2 — Network Propagation**
8. **Persistence** - ensuring long-term access.
9. **Defense Evasion** - hiding from detection (obfuscation, clearing logs).
10. **Credential Access** - stealing creds, hash dumping, keylogging.
11. **Privilege Escalation** - gaining higher-level privileges.
12. **Discovery** - mapping network, users, machines.
13. **Lateral Movement** - pivoting across systems.
14. **Collection** - gathering data of interest.


### **Stage 3 — Mission Completion**
15. **Exfiltration** - sending data out of the environment.
16. **Impact / Effects** - encryption, wiping, manipulation.
17. **Objectives** - fulfilling attacker goals (ransom, espionage).
18. **Cleanup** - deleting traces, covering tracks.

---

## 4. Why UKC Is More Realistic Than Cyber Kill Chain
- CKC stops early (Exfiltration not covered properly).  
- UKC handles **post-exploitation**, **lateral movement**, **privilege escalation**, **collection**, **impact** — all missing in CKC.
- More aligned with **modern incident response**, **APT behaviour**, and **multi-stage attacks**.

---

## 5. SOC Analyst Use-Cases
- Understand where your SIEM detection gaps lie.
- Map alerts or IOCs to specific UKC phases.
- Build better detections by aligning with the **post-exploitation** phases.
- Use UKC stages to communicate attack progress during IR.

---

## 6. High-Value Detection Phases (SOC Priorities)
- **Credential Access** → prevents lateral movement.
- **Privilege Escalation** → high-risk activity.
- **Lateral Movement** → campaign pivot point.
- **Exfiltration** → data theft.
- **Impact** → ransomware, disruption.

Catching activity here **prevents full mission success** even if initial compromise succeeded.

---

## 7. Simple Mental Model
Think of UKC as:
> “What the attacker wants next.”

Every alert is a breadcrumb pointing to the next possible phase.

---

## 8. Quick Comparison Table

| Kill Chain | MITRE ATT&CK | UKC |
|-----------|--------------|-----|
| Linear | Techniques view | Full lifecycle |
| Good for initial compromise | Deep & detailed | Strategic + operational |
| Limited post-exploitation | Big technique list | 18 clear phases |
| Older model | Very granular | Maps both CKC + ATT&CK |

---

## 9. Final Takeaways
- UKC offers a **complete**, **modern**, and **practical** view of an attack.  
- Best for SOC analysts, threat hunters, and IR teams.  
- Helps you understand **how small alerts fit into large intrusion campaigns**.  
- Use it to prioritize detections, investigations, and threat hunts.
