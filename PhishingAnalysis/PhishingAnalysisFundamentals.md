## Phishing Analysis Fundamentals

### Introduction

Spam and phishing are common social engineering attacks. In phishing, the attack vector can be a phone call, text message, or email. This room focuses on analyzing phishing attacks delivered via email.

Phishing is a significant threat. Even with strong defenses in place, one unsuspecting user clicking a malicious link or attachment can give an attacker a foothold inside the network.

Security analysts must understand how to analyze emails, identify malicious indicators, and collect actionable information to strengthen defenses.

This room explores how emails work, what components make them up, and how we analyze email headers and bodies.

---

### The Email Address

Email was invented in the early 1970s by Ray Tomlinson, who also popularized the `@` symbol.

An email address contains:

* **User Mailbox / Username**
* **@**
* **Domain**

Example: `billy@johndoe.com`

* User mailbox: `billy`
* Domain: `johndoe.com`

**Answer:** Email dates back to the **1970s**.

---

### Email Delivery

Three main protocols are involved in email transmission:

* **SMTP** - Sends outgoing emails.
* **POP3** - Downloads emails to a single device.
* **IMAP** - Syncs emails across multiple devices.

**Key Differences:**

* POP3 stores email locally.
* IMAP stores and syncs email on the server.

**Email Flow Summary:**

1. User composes and sends email.
2. SMTP queries DNS for destination.
3. DNS returns domain info.
4. SMTP transfers the message across the Internet.
5. It reaches the destination SMTP server.
6. Email moves to local POP3/IMAP server.
7. Recipient retrieves the message.

**Secure Ports:**

* SMTP STARTTLS: **587**
* IMAP Secure: **993**
* POP3 Secure: **995**

---

### Email Headers

An email contains two parts:

* **Header** - metadata and routing info
* **Body** - actual content (text or HTML)

Common header fields:

* **From**
* **Subject**
* **Date**
* **To**

Additional important headers:

* **X-Originating-IP** - IP of sender
* **smtp.mailfrom / header.from** - sending domain (Auth-Results)
* **Reply-To** - reply destination

**Answer:** The header equivalent to Reply-To is **Return-Path**.

**Answer:** IP info can be checked on **arin.net**.

---

### Email Body

Emails can contain:

* Plain text
* HTML-formatted content
* Images
* Hyperlinks
* Attachments

Attachments have specific headers:

* **Content-Type** (e.g., application/pdf)
* **Content-Disposition** (attachment)
* **Content-Transfer-Encoding** (often base64)

Example answers:

* Blocked image URI: **[hxxps:// i.imgur.com/LSWOtDI.png]**
* PDF attachment name: **Payment-updateid.pdf**
* Extracted PDF text after decoding base64: **THM{BENIGN_PDF_ATTACHMENT}**

---

### Types of Phishing

Common malicious email categories:

* **Spam** - unsolicited bulk email
* **MalSpam** - malicious spam
* **Phishing** - impersonation to steal sensitive data
* **Spear Phishing** - targeted phishing
* **Whaling** - phishing targeting executives
* **Smishing** - phishing over SMS
* **Vishing** - phishing via voice call

**Common phishing characteristics:**

* Spoofed sender address
* Urgency in subject/body
* Lookalike branding
* Poor formatting or grammar
* Generic greetings
* Malicious links (often shortened/obfuscated)
* Malicious attachments

Use **defanging** to safely share URLs:

* Example: `http://site.com` → `hxxp[://]site[.]com`

**Email3.eml Answers:**

* Masquerading as: **Home Depot**
* Sender: **[support @teckbe. com]**
* Subject: **Order Placed : Your Order ID OD2321657089291 Placed Successfully**
* Defanged link: **hxxp[://]t[.]teckbe[.]com**

---

### Conclusion

**BEC (Business Email Compromise)** occurs when an attacker gains access to an internal corporate email account and uses it to perform fraud or manipulate employees.

Key takeaways from this room:

* Components of an email address
* How email travels across the Internet
* Viewing and analyzing email headers
* Understanding and analyzing email body content
* Identifying malicious indicators in phishing campaigns
