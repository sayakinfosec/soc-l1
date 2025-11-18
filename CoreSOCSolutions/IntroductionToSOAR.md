## Introduction to SOAR

### 1. Introduction

To defend against attacks, SOC teams rely on SIEM, EDR, firewalls, threat intelligence platforms, and close communication with IT and management. As threats grow more advanced, SOCs struggle with alert fatigue, manual workflows, unintegrated tools, and communication gaps.

This module explores how **Security Orchestration, Automation, and Response (SOAR)** helps overcome these challenges.

#### 1.1 Learning Objectives

* Understand traditional SOC operations and challenges
* Explore how SOAR solves these challenges
* Learn SOAR playbooks
* Walk through a threat intelligence workflow

---

### 2. Traditional SOC and Challenges

#### 2.1 How Traditional SOCs Work

A Security Operations Center (SOC) is a centralized unit responsible for monitoring, detecting, responding to, and mitigating security threats. Its capabilities include:

* **Monitoring & Detection:** Continuous threat monitoring via SIEM (e.g., failed logins, unusual login locations).
* **Recovery & Remediation:** First responders who isolate endpoints, remove malware, block IPs, disable accounts, etc.
* **Threat Intelligence:** Consuming feeds of malicious IPs, domains, and hashes.
* **Communication:** Coordinating with IT and management using tickets and reporting workflows.

#### 2.2 Challenges Faced by SOCs

* **Alert Fatigue:** Overload of alerts, many low-quality or false positives.
* **Disconnected Tools:** Multiple independent platforms with no integration.
* **Manual Processes:** Lack of documentation and reliance on tribal knowledge.
* **Talent Shortage:** Too few analysts to handle increasing alert volumes.

**Answer:** *How would you describe an overload of security events in a SOC?*
➡ **Alert Fatigue**

---

### 3. Overcoming SOC Challenges with SOAR

SOAR centralizes all SOC tools into one interface, integrates ticketing/case management, and reduces manual workloads through automation.

#### 3.1 What is SOAR?

A unified platform that brings together SIEM, EDR, IAM, firewalls, threat intel, and ticketing systems under one dashboard.

#### 3.2 Core Capabilities of SOAR

##### 3.2.1 Orchestration

Integration of multiple security tools into coordinated workflows. SOAR uses **playbooks** to define how alerts should be investigated.

Example (VPN brute force):

1. Receive alert
2. Check user's typical login IPs
3. Check IP reputation
4. Check for successful logins
5. Escalate or contain

##### 3.2.2 Automation

Automates the entire workflow-querying SIEM, checking TI, disabling users, opening tickets-without analyst intervention.

##### 3.2.3 Response

Enables taking actions (e.g., blocking IPs, disabling accounts) through a unified interface, often automatically.

#### 3.3 Do We Still Need SOC Analysts?

Yes. Automation reduces repetitive work, but analysts are crucial for judgment calls, contextual decision-making, and designing the playbooks themselves.

**Answers:**

* *Connecting and integrating security tools into workflows is known as:* **Orchestration**
* *A predefined list of actions to handle an incident is a:* **Playbook**

---

### 4. Building SOAR Playbooks

Playbooks define the sequence of automated or semi-automated steps that SOAR follows for specific alert types.

#### 4.1 Phishing Playbook

Phishing investigations involve URL/attachment checks, threat intel lookups, sandboxing, and user notification. SOAR automates these steps:

* Alert received → Ticket created
* Check for URL or attachment

  * If none → Notify user
  * If present → Extract, analyze, verify reputation
* Remediate if malicious

#### 4.2 CVE Patching Playbook

For each new CVE:

1. Fetch CVE from advisory lists
2. Analyze severity
3. Create patching ticket
4. Test patch
5. Deploy patch
6. If still vulnerable → Develop mitigation plan

Even in automated workflows, analysts step in for critical validation points.

**Answers:**

* *Is manual analysis vital in SOAR workflows?* ➝ **Yay**
* *Where does the CVE Patching playbook fetch new CVEs from?* ➝ **Advisory lists**
* *If assets remain vulnerable after patching, what is developed next?* ➝ **Mitigation plan**
