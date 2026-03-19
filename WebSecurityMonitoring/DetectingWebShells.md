## Detecting Web Shells

### Introduction

Web shells are a common post-exploitation technique used by attackers to gain remote access and maintain persistence on compromised systems. For SOC Analysts and Incident Responders, detecting web shells is a critical skill.

This room covers:

* What web shells are and how they are used
* Detection techniques using logs, filesystem, and network analysis
* Tools and methods used in real-world investigations

---

### Learning Objectives

* Understand web shells and attacker use cases
* Detect web shell activity via logs, filesystem, and network data
* Learn common tools used in detection workflows

---

### Web Shell Overview

A web shell is a malicious script uploaded to a web server that allows remote command execution.

Key points:

* Used for **initial access** (via file upload vulnerabilities)
* Used for **persistence**
* Enables:

  * Reconnaissance
  * Privilege escalation
  * Lateral movement
  * Data exfiltration

Example:

* `awebshell.php` in `/uploads`
* Accessible via browser or curl
* Executes system commands remotely

#### Deployment

Attackers require:

* File upload vulnerabilities
* Misconfigurations
* Existing access

Example scenario:

* Image upload feature → attacker uploads `shell.php`

#### Real-World Examples

* **Hafnium (ProxyLogon)** → uploaded `.aspx` shells to Exchange servers
* **Conti Ransomware** → uploaded web shells and mapped internal network

#### Key Answers

* MITRE Technique: **T1505.003**
* Common extension (Exchange): **.aspx**

---

### Anatomy of a Web Shell

Web shells abuse legitimate system functions.

#### Common PHP Functions

* `shell_exec()`
* `exec()`
* `system()`
* `passthru()`

#### How It Works

* Accepts input via URL (`?cmd=whoami`)
* Executes command
* Displays output

#### Example Flow

1. Input command via URL
2. Store in variable
3. Execute using system function
4. Return output

#### Key Answers

* Current user: **www-data**
* Flag: **THM{W3b_Sh3ll_Usag3}**

---

### Log-Based Detection

Web server logs are the primary source for detecting web shells.

#### Key Indicators

##### HTTP Methods

* GET → recon / interaction
* POST → upload / interaction
* PUT → upload shell
* DELETE → cleanup
* OPTIONS / HEAD → recon

##### Suspicious Patterns

* Repeated requests to same file
* GET → POST sequence
* Frequent 404 → 200 transitions

##### User-Agent Anomalies

* Modified: `Mozilla/4.0`
* Outdated: `MSIE 6.0`
* Tools: `curl`, `wget`

##### Query Strings

* Indicators like:

  * `cmd=`
  * `exec=`
* Encoded payloads (Base64)

##### Other Indicators

* Missing referrer
* External IPs
* Odd timestamps

#### Auditd

Tracks system-level activity.

Example:

```
ausearch -k web_shell
```

Key syscall:

* **creat** → file written to disk

#### Correlation

* Web logs + audit logs = stronger detection
* Example:

  * POST request → file created → command executed

#### SIEM Benefits

* Centralized logging
* Faster querying
* Correlation across sources

#### Key Answers

* URL component: **query strings**
* Syscall: **creat**

---

### Beyond Logs

#### File System Analysis

Common directories:

* `/var/www/html/`
* `/usr/share/nginx/html/`
* `/uploads/`, `/images/`, `/admin/`
* `/tmp/`

##### Indicators

* Unusual filenames
* `.php`, `.jsp` files
* Double extensions (`image.jpg.php`)

##### Useful Commands

```
find /var/www/ -type f -name "*.php"
grep -r "eval(" .
```

#### Network Traffic Analysis

Inspect packet data for deeper visibility.

##### Indicators

* Suspicious HTTP methods
* Malicious payloads
* Encoded commands
* Abnormal ports/protocols

##### Wireshark Filters

```
http.request.method == "METHOD"
http.request.uri contains ".php"
http.user_agent
```

#### Key Answers

* Find command: **find /var/www/ -type f -name "*.php"**
* Wireshark filter: **http.request.method == "PUT"**

---

### Investigation

#### Scenario

* WordPress site compromise suspected
* Logs: `/var/log/apache2/access.log`

#### What to Look For

* Repeated `.php` requests
* Response code patterns
* Suspicious User-Agents

#### Useful Command

```
cat /var/log/apache2/access.log | grep "404"
```

#### Key Findings

* Attacker IP: **203.0.113.66**
* First directory: **/wordpress**
* Upload file: **upload_form.php**
* First command: **whoami**
* Downloaded file: **linpeas.sh**
* Flag: **THM{W3b_Sh3ll_Int3rnals}**

---

### Conclusion

Web shell detection requires a multi-layered approach:

* Web log analysis
* System-level monitoring (auditd)
* File system inspection
* Network traffic analysis

Correlating these data sources provides strong evidence of compromise and helps analysts reconstruct attacker behavior effectively.
