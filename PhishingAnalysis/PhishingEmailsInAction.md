
## Phishing Emails in Action

### Introduction

Now that the fundamentals of email structure and phishing concepts are covered, we are moving into real-world phishing email samples. Each sample highlights specific tactics used by attackers to make emails appear legitimate. The more convincing the email, the more likely a user is to click a malicious link, open a dangerous attachment, or fall for social engineering.

These samples are taken from real spam and phishing campaigns. Interact with them cautiously.

---

### Cancel Your PayPal Order

**Techniques shown:**

* Spoofed email address
* URL shortening services
* HTML impersonation of a brand

### Observations

* Recipient email is unusual and not related to the actual Yahoo account.
* Sender details appear as `service@paypal.com`, but the real sender address is `gibberish@sultanbogor.com`.
* Subject creates urgency by suggesting a transaction the victim doesn't recognize.

### Body Analysis

* Email is designed to look like a legitimate PayPal notification.
* No attachments present.
* Only actionable item is the **Cancel the order** button.

### Hyperlink Review

* Link is shortened using a URL shortener.
* Expansion reveals redirect to `google.com`.

**Answer:** The gibberish sender email starts with: `noreply`.

---

### Track Your Package

**Techniques shown:**

* Spoofed email address
* Pixel tracking
* Link manipulation

### Observations

* Email pretends to be from a mail distribution center.
* Subject line contains a fake tracking number.
* Images are blocked by Yahoo to prevent tracking pixel activation.

### Pixel Tracking

* The source reveals an embedded image named `Tracking.png`.
* Tracking pixels inform the attacker that the email was opened.

### Hyperlink

* Link points to a suspicious domain.

**Answer:** Root domain (defanged): `devret[.]xyz`

---

### Select Your Email Provider to View Document

**Techniques shown:**

* Urgency
* HTML brand impersonation
* Link manipulation
* Credential harvesting
* Poor grammar and typos

### Observations

* Sent on July 15, 2021.
* Introduces urgency: link expires the same day.
* Victim is redirected to a fake OneDrive page.
* Multiple login options designed to harvest credentials.
* Further redirection leads to a fake Adobe-themed page with typos.

**Answer:** Another company name used in the phishing email: **Citrix**.

---

### Please Update Your Payment Details

**Techniques shown:**

* Spoofed email address
* Urgency
* HTML brand impersonation
* Poor grammar / typos
* Attachments

### Observations

* Email appears from "Netflix Billing" but sender is `z99@musacombi.online`.
* Repeated urgency: account suspended.
* Misspellings of "Netflix" appear in multiple places.
* Attachment contains a PDF with a malicious link.
* Phone number shown is unusual for a US-based victim.

**Answer:** Users should forward suspicious Netflix messages to: **[phishing@ netflix.com]**.

---

### Your Recent Purchase

**Techniques shown:**

* Spoofed email address
* BCCed recipients
* Urgency
* Poor grammar / typos
* Attachments

### Observations

* Email appears to be from Apple Support, but sender is `gibberish@sumpremed.com`.
* Recipient was BCCed — indicating mass delivery.
* Several typos: `donoreply`, `payament`.
* No email body — only an attached `.DOT` file.
* Attachment displays an App Store–themed fake receipt.

**Answer:**

* BCC stands for **Blind Carbon Copy**.
* Technique used to persuade the victim: **Urgency**.

---

### DHL Express Courier Shipping Notice

**Techniques shown:**

* Spoofed sender
* HTML impersonation of brand
* Attachments

### Observations

* Sender domain does not match DHL.
* Subject implies a package shipment.
* Email body uses DHL-themed HTML.
* Attachment is an Excel file.
* Opening it triggers a payload and throws an error.

**Answer:** The executable attempted to run is: **regasms.exe**.

---

### Conclusion

This room demonstrated real phishing email examples, highlighting:

* Spoofing
* Urgency tactics
* Tracking mechanisms
* Links disguised via HTML or shortened URLs
* Credential harvesting workflows
* Malicious attachments and payload delivery

These practical examples reinforce how attackers craft convincing emails and what indicators analysts must identify.
