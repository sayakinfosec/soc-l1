## Phishing Prevention

### 1. Introduction

Phishing remains one of the most common and effective ways for attackers to gain initial access to systems. Defenders use multiple tools and controls to protect users from malicious emails.

The MITRE ATT&CK Framework defines *Phishing for Information* as attempts to trick users into divulging sensitive information.

**Learning Objectives:**

* Understand core email security controls (SPF, DKIM, DMARC, S/MIME)
* Analyze SMTP network traffic and email content
* Explore anti-phishing protection measures

---

### 2. Sender Policy Framework (SPF)

**Definition:** SPF is a DNS-based mechanism that verifies whether a sending mail server is authorized to send email on behalf of a domain.

**Verification Results:**

* **Pass / Neutral / None** → Accept
* **SoftFail / PermError** → Flag as suspicious
* **Fail / TempError** → Reject

**Sample SPF Record:**

```
v=spf1 ip4:127.0.0.1 include:_spf.google.com -all
```

* `v=spf1` → SPF record start
* `ip4:` → Authorized IP
* `include:` → Authorized domain
* `-all` → Reject all unauthorized senders

**Example (TryHackMe SPF Record):** Contains **3** authorized domains.

**SoftFail Intended Action:** **Flag**

---

### 3. DomainKeys Identified Mail (DKIM)

**Definition:** DKIM uses cryptographic signatures to verify that an email has not been altered and truly originates from the stated domain.

**Sample DKIM Record:**

```
v=DKIM1; k=rsa; p=<public_key>
```

* `k=rsa` → Key type
* `p=` → Public key used for signature validation

**Example Spam Header:** Shows DKIM `permerror` due to **no key for signature**.

---

### 4. Domain-Based Message Authentication, Reporting & Conformance (DMARC)

**Definition:** DMARC, an open-source standard, ties SPF and DKIM results together to enforce sender authenticity.

**Sample DMARC Record:**

```
v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com
```

* `p=` sets the policy

  * `none` → Monitor only
  * `quarantine` → Send to spam
  * `reject` → Block

**Most Protective DMARC Policy:** **p=reject**

---

### 5. Secure/Multipurpose Internet Mail Extensions (S/MIME)

S/MIME provides **digital signatures** and **encryption**.

**Digital Signatures:**

* Authentication
* Non-repudiation
* Integrity

**Encryption:**

* Ensures only intended recipients can read the message
* Maintains confidentiality

**Which component ensures confidentiality?** → **Encryption**

---

### 6. Analyzing SMTP Responses

Wireshark filter for SMTP status codes:

```
smtp.response.code
```

**Key Findings:**

* **220 Service ready:** 19 packets
* **Blocked by spamhaus:** Response code **553**
* Full message: *Requested action not taken: mailbox name not allowed (553)*
* **Response code 552:** 6 messages blocked

---

### 7. Inspecting Emails and Attachments

**Total SMTP packets:** 512

**Attachment in packet 270:** `document.zip`

**Host not responding:** `212.253.25.152`

**Email client used:** *Microsoft Outlook Express 6.00.2600.0000*

**Encoding:** `base64`

---

### 8. How Organizations Stop Phishing

**Technical Defenses:**

* Email filtering
* Secure Email Gateways (SEGs)
* Link rewriting
* Sandboxing

**User-Facing Protections:**

* Warning indicators (External sender, Suspicious link)
* Report phishing button
* Awareness training
* Phishing simulations

**Which technique safely analyzes suspicious files?** → **Sandboxing**
