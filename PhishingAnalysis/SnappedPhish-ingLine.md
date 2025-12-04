## Snapped Phish-ing Line

### Overview

A multi-stage phishing investigation involving compromised employees, malicious URLs, phishing kits, and CTI (Cyber Threat Intelligence) enrichment. This scenario simulates a real-world incident affecting SwiftSpend Financial.

---

### Scenario Summary

Multiple employees reported a suspicious email, and some already entered credentials on a phishing page. As part of IT/SOC, your tasks included:

* Reviewing phishing emails in the VM
* Visiting phishing URLs in a contained environment
* Retrieving the phishing kit from the adversary's server
* Using CTI tools to analyse the kit and adversary
* Extracting indicators such as hashes, URLs, emails, and timestamps

---

### Findings

#### 📌 Email Investigation

* **Employee who received a PDF attachment:** William McClean
* **Adversary's sending email address:** [Accounts.Payable@groupmarketingonline.icu](mailto:Accounts.Payable@groupmarketingonline.icu)

#### 📌 Phishing URL Analysis

* **Redirection URL for Zoe Duncan (defanged):**
  `hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error`

#### 📌 Phishing Kit Retrieval

* **ZIP archive URL (defanged):**
  `hxxp[://]kennaroads[.]buzz/data/Update365[.]zip`
* **SHA256 hash of phishing kit:**
  `ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686`
* **First submission timestamp:** `2020-04-08 21:55:50 UTC`
* **SSL certificate log date:** `2020-06-25`

---

### Compromised Credentials & Exfiltration

* **Employee who submitted password twice:**
  `michael.ascot@swiftspend.finance`
* **Collector email used by adversary:**
  `m3npat@yandex.com`
* **Additional email found in phishing kit (Gmail):**
  `jamestanner2299@gmail.com`

---

### Hidden Flag

**`THM{pL4y_w1Th_tH3_URL}`**

---

### Conclusion

The phishing campaign used:

* A malicious domain hosting spoofed Office365 login pages
* Multiple exfiltration email accounts
* A distributed phishing kit with traceable indicators (zip archive, SSL logs)

This investigation demonstrates practical SOC workflows: email analysis, URL investigation, phishing kit teardown, and CTI correlation.
