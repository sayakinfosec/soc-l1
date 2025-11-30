## Phishing Analysis Tools

### Introduction

Earlier we learned how to manually sift through raw email source code to extract header information, sender details, URLs, and attachments. In this room, we explore tools that streamline and enhance phishing email analysis.

We will cover tools that help us:

* Examine and interpret email headers
* Extract and expand URLs (including shortened URLs)
* Analyze potentially malicious links safely
* Retrieve attachments and analyze them through malware sandboxes

---

### What Information Should We Collect?

When analyzing a suspicious email, analysts must gather key information from both the header and the body.

### Email Header Checklist

* Sender email address
* Sender IP address
* Reverse lookup for the sender IP
* Email subject
* Recipient email (may also appear in CC/BCC)
* Reply-To address (if any)
* Date and time

### Email Body Checklist

* URL links (expand if shortened)
* Attachment name(s)
* SHA256 or MD5 hash of attachments

⚠️ Avoid clicking links or opening attachments directly.

---

### Email Header Analysis

Some header data can be viewed directly in your email client, but sender IPs, Reply-To fields, and intricate routing details require full header access. The following tools automate header parsing.

### **1. Google Admin Toolbox - Messageheader**

* Analyzes SMTP headers to reveal routing issues, delays, and misconfigured servers.
* Usage: paste the entire header and analyze.

### **2. Message Header Analyzer**

* Simple visual representation of header routing.

### **3. Mailheader.org**

* Another alternative for parsing metadata.

### Additional Reading

* **MTA (Message Transfer Agent):** Software responsible for transferring emails.
* **MUA (Mail User Agent):** Software like Gmail, Outlook, Thunderbird used to read/send email.

### IP & Domain Investigation Tools

* **IPinfo.io:** Provides geolocation and context for IP addresses.
* **URLScan.io:** Navigates URL automatically, takes screenshot, logs requests.
* **Talos Reputation Center:** Cisco’s threat intelligence for domain/IP reputation.

**Answer:** The official site capital-one.com tried to mimic is **capitalone.com**.

---

### Email Body Analysis

The email body often contains the malicious component: a link or an attachment.

### Extracting Links

You can manually extract links by right-clicking and selecting:
**Copy Link Location**

Or use tools:

* **URL Extractor**
* **CyberChef - Extract URLs recipe**

Always note the **root domain** for reputation checks.

### Attachment Handling

If attachments exist:

1. Save them safely (e.g., via Thunderbird’s *Save* button)
2. Obtain the hash:

```
sha256sum FileName.ext
```

Example:

```
c650f397...af4ee83  Double Jackpot Slots Las Vegas.dot
```

### File Reputation Tools

* **Talos File Reputation**
* **VirusTotal**
* **ReversingLabs** (additional option)

**Answer:** Manually obtain a hyperlink via **Copy Link Location**.

---

### Malware Sandboxes

You do not need reverse-engineering skills to understand malware behavior. Malware sandboxes analyze malicious files safely.

### Common Sandboxes

* **Any.Run** - Interactive, real-time analysis
* **Hybrid Analysis** - Cloud-based analysis engine
* **Joe Sandbox** - Rich feature set, MITRE mapping, Yara/Sigma support

Sandboxes reveal:

* Network communication
* Additional payload downloads
* Registry modifications
* IOCs (Indicators of Compromise)

---

### PhishTool

PhishTool streamlines phishing casework by integrating:

* Email metadata extraction
* OSINT enrichment
* Auto-analysis pathways
* Attachment and URL analysis
* Integration with VirusTotal

Features include:

* Sender/recipient info
* Timestamp and originating IP
* SMTP relay chain
* Reply-To detection
* Email text and HTML source views
* Attachment extraction + hash generation
* VT integration (with API key)

PhishTool also allows SOC-style workflows:

* Marking email as malicious
* Adding classification codes (e.g., Whaling)
* Documenting resolution notes

**Answer:** The EXE filename visible in Strings output is **#454326_PDF.exe**.

---

### Conclusion

In this room, we learned how to:

* Use specialized tools to extract and analyze email headers
* Expand and inspect URLs safely
* Retrieve, hash, and reputation-check attachments
* Use sandboxes for behavioral malware analysis
* Automate phishing triage using PhishTool

These tools form the foundational toolkit for SOC analysts and incident responders dealing with phishing threats.
