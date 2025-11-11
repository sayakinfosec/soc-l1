## SOC L1 Alert Reporting

### 1. Introduction

During or after alert triage, L1 analysts may be uncertain about how to classify the alert, requiring senior support or information from the system owner.
They may also deal with real cyberattacks and breaches that require immediate attention and remediation.

This room introduces three essential SOC practices: **alert reporting**, **escalation**, and **communication**.

#### Learning Objectives

* Understand the need for SOC alert reporting and escalation.
* Learn how to write alert comments or case reports properly.
* Explore escalation methods and communication best practices.
* Apply the knowledge in a simulated SOC environment.
* Build confidence for SOC Simulator and SAL1 certification.

#### Prerequisites

* Completion of the SOC L1 Alert Triage room.
* Basic understanding of common attacks.
* Familiarity with L1 analyst responsibilities.

---

### 2. Alert Funnel

Alerts originate from SIEM, EDR, or ticket platforms.
Most are closed as **False Positives**, but some are **True Positives** requiring escalation to L2 analysts for remediation.

Three new terms define this transition:

* **Reporting:** Documenting the investigation and findings.
* **Escalation:** Handing off alerts needing deeper analysis.
* **Communication:** Coordinating with relevant teams or departments.

*(Visual: L1 handles 100 alerts → 10 escalated to L2 → 1 incident needs DFIR)*

---

### 3. Alert Reporting

Before closing or escalating an alert, L1 analysts must report it.
Reports should include detailed findings and evidence - especially for **True Positives**.

A well-documented alert report:

* Provides **context** for escalation.
* Preserves **records** beyond SIEM log retention.
* Enhances **investigation and communication** skills.

---

### 4. Reporting Guide

#### 4.1 Purpose of Alert Reports

| Purpose                            | Explanation                                               |
| ---------------------------------- | --------------------------------------------------------- |
| **Provide context for escalation** | Helps L2 analysts quickly understand what happened.       |
| **Save findings for records**      | Alerts remain stored indefinitely, ensuring traceability. |
| **Improve investigation skills**   | Writing reports clarifies and strengthens understanding.  |

#### 4.2 Report Format – “Five Ws” Approach

Follow these five questions when documenting an alert:

* **Who:** Which user or system performed the action.
* **What:** What actions or events occurred.
* **When:** The exact time of suspicious activity.
* **Where:** The affected device, IP, or website.
* **Why:** The reasoning behind your final verdict.

💡 *Example Insight:*

> Even legitimate-looking addresses like `support@microsoft.com` can be suspicious if SPF/DKIM checks fail - indicating possible spoofing.

---

### 5. Alert Escalation

After documenting your verdict:

* **Escalate** to L2 if the alert requires deeper investigation or remediation.
* The report provides L2 with immediate context and saves analysis time.

#### 5.1 When to Escalate

Escalate alerts if:

* Indicators of a major cyberattack are present.
* Remediation (e.g., host isolation, password reset) is needed.
* External communication (customers, partners, or law enforcement) is required.
* You’re uncertain about the alert and need senior input.

#### 5.2 Escalation Process

* Change alert status to *In Progress*.
* Assign the alert to the on-shift L2.
* Notify them via chat or escalation channel.
* L2 reviews your report and proceeds with investigation or DFIR.

💡 *Tip:* Requesting L2 support is **always acceptable**, especially in your early months. It promotes collaboration and clarity.

---

### 6. SOC Communication

Effective communication ensures smooth coordination during critical or uncertain cases.
Crisis communication procedures help analysts act fast and consistently under pressure.

#### 6.1 Common Communication Scenarios

| Situation                                       | Recommended Action                                                        |
| ----------------------------------------------- | ------------------------------------------------------------------------- |
| **Critical alert; L2 unavailable for 30+ mins** | Escalate through emergency contacts → call L2 → L3 → manager.             |
| **Account compromise on Slack/Teams**           | Never use compromised channels - contact via phone or alternate email.    |
| **Overwhelming number of alerts**               | Prioritize per severity, then inform L2 immediately.                      |
| **Misclassified alert discovered days later**   | Report to L2 at once - threat actors can stay dormant before impact.      |
| **Logs missing or not parsed correctly**        | Investigate what’s possible and report parsing issues to L2/SOC engineer. |

---

### 7. Key Takeaways

* **Reporting ensures clarity**, not redundancy - it strengthens SOC handoffs.
* **Escalation is a responsibility**, not a weakness - it maintains detection integrity.
* **Communication keeps the SOC functional**, especially under pressure.
