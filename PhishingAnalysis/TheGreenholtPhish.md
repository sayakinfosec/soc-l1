## The Greenholt Phish

### Overview

A practical SOC-style phishing investigation involving a suspicious email received by a Sales Executive at Greenholt PLC. The scenario tests real-world analysis skills such as email header inspection, attachment analysis, IP research, and validation of sender authenticity.

---

### Case Summary

The employee reported the following red flags:

* Unexpected email from a customer
* Generic greeting not typical for the sender
* Mention of a money transfer he wasn't expecting
* Unrequested attachment included in the email

The SOC team (you) must investigate the `.eml` sample.

---

### Investigation Steps

1. Load the virtual machine from the task.
2. Open `challenge.eml` using **Thunderbird** for proper header and attachment inspection.
3. Review:

   * Subject line
   * From and Reply-To addresses
   * Header fields (Received, Originating IP)
   * DNS records (SPF, DMARC)
   * Attachment details (filename, type, hash, size)

---

### Findings

### 📌 Subject

**Transfer Reference Number:** `09674321`

### 📌 Sender Details

* **From Name:** Mr. James Jackson
* **From Email:** [info@mutawamarine.com](mailto:info@mutawamarine.com)
* **Reply-To Email:** [info.mutawamarine@mail.com](mailto:info.mutawamarine@mail.com)

### 📌 Technical Header Analysis

* **Originating IP:** 192.119.71.157
* **IP Owner:** Hostwinds LLC

### 📌 DNS Records (Return-Path Domain)

* **SPF:** `v=spf1 include:spf.protection.outlook.com -all`
* **DMARC:** `v=DMARC1; p=quarantine; fo=1`

### 📌 Attachment Details

* **Attachment Name:** `SWT_#09674321____PDF__.CAB`
* **SHA256 Hash:** `2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f`
* **File Size:** `400.26 KB`
* **Actual File Extension:** RAR

---

### Conclusion

The mismatched sender details (Failed SPF), suspicious attachment type, and header anomalies confirm this is a **phishing email** with a likely malicious compressed archive disguised as a CAB/PDF file.
