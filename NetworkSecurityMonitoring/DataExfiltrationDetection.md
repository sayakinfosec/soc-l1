## DataExfiltrationDetection

Data exfiltration is the unauthorized transfer of sensitive data from an internal system to an external destination controlled by an adversary. It is often the primary objective once attackers gain access. SOC analysts must detect these activities early to prevent data breaches and impact.

---

### Data Exfiltration: Overview

Data exfiltration occurs when sensitive information is removed from an organization without authorization. This can be carried out by external attackers, malware, or insiders using legitimate tools and protocols.

---

### Why Adversaries Perform Data Exfiltration

Attackers exfiltrate data for several reasons:

* Financial gain through resale or fraud
* Espionage and intellectual property theft
* Ransomware-driven extortion
* Operational disruption and reputational damage
* Reconnaissance for future attacks

---

### Threat Actors and Exfiltration Techniques

Real-world campaigns show that attackers prefer stealthy, trusted channels:

* APT29 using HTTPS over legitimate domains
* FIN7 embedding data in HTTP POST requests
* Lunar Spider staging encrypted exfiltration
* DarkSide performing dual extortion
* APT10 abusing cloud APIs for cloud-to-cloud exfiltration

---

### Common Phases of Data Exfiltration

* Discovery and collection of sensitive data
* Staging through compression, encryption, or encoding
* Exfiltration via network, cloud, or removable media
* Command and Control coordination

---

### Techniques and Indicators of Data Exfiltration

Detection requires correlating multiple telemetry sources:

* Proxy, firewall, and NetFlow logs
* DNS query patterns
* Endpoint process and file activity
* Cloud audit and access logs

SOC triage focuses on source host, destination, data volume, process identity, and timeline correlation.

---

### Detection: Data Exfiltration via DNS Tunneling

DNS tunneling abuses DNS queries and responses to encode and transfer data. Since DNS traffic is common and usually allowed outbound, it is an effective covert channel.

DNS tunneling indicators include:

* Excessive DNS queries to a single external domain
* Very long query names or subdomains
* High-entropy or Base32/Base64-like strings
* Frequent NXDOMAIN responses
* Unusual record types such as TXT
* Regular beaconing intervals

Wireshark analysis using filters such as:

* `dns`
* `dns.flags.response == 0`
* `dns && frame.len > 70`

revealed long encoded DNS queries targeting a single suspicious domain.

Splunk analysis showed:

* Abnormally high query counts
* Long encoded query names
* Multiple compromised internal hosts
* One external domain receiving the data

Findings:

* Suspicious domain: `tunnelcorp.net`
* Suspicious DNS logs observed: `315`
* Most active internal IP: `192.168.1.103`

---

### Detection: Data Exfiltration via FTP

FTP is frequently abused due to clear-text authentication and simple file transfer mechanisms. Attackers may use compromised or weak credentials to exfiltrate large volumes of data.

Indicators include:

* USER and PASS commands in clear text
* Repeated STOR upload commands
* Large payload transfers to external IPs
* Suspicious file names and extensions
* Use of guest or service accounts

Wireshark analysis using:

* `ftp || ftp-data`
* `ftp.request.command == "USER" || ftp.request.command == "PASS"`
* `ftp contains "STOR"`
* `ftp contains "csv"`

revealed sensitive files being uploaded to an external IP.

Following TCP streams exposed customer-related data and hidden flags inside transferred files.

Findings:

* Guest account connections: `5`
* Exfiltrated file: `customer_data.xlsx`
* Internal IP with largest payload: `192.168.1.105`
* Hidden flag: `THM{ftp_exfil_hidden_flag}`

---

### Detection: Data Exfiltration via HTTP

HTTP is commonly abused because it blends with legitimate web traffic and easily traverses firewalls and proxies. Attackers often use POST requests or encoded payloads.

Indicators include:

* Large HTTP POST requests to unusual domains
* High outbound byte counts
* Chunked or multipart uploads
* Beaconing followed by large transfers

Splunk analysis filtered POST requests and highlighted abnormal payload sizes and suspicious domains.

Wireshark analysis using:

* `http`
* `http.request.method == "POST"`
* `frame.len > 750`

confirmed a single large POST request containing exfiltrated sensitive data.

Findings:

* Compromised internal host: `192.168.1.103`
* Hidden flag: `THM{http_raw_3xf1ltr4t10n_succ3ss}`

---

### Detection: Data Exfiltration via ICMP

ICMP is often allowed and lightly inspected. Attackers encode data into ICMP echo requests and replies to exfiltrate information covertly.

Indicators include:

* High volumes of ICMP traffic to external IPs
* ICMP packets with unusually large payloads
* Regular, periodic ICMP traffic
* High-entropy encoded payloads

Wireshark analysis using:

* `icmp`
* `icmp.type == 8`
* `icmp.type == 8 && frame.len > 100`

revealed large ICMP echo requests carrying encoded data.

Findings:

* Hidden flag: `THM{1cmp_3ch0_3xf1ltr4t10n_succ3ss}`

---

### SOC Analyst Key Takeaways

Data exfiltration detection depends on correlation, not single alerts. Effective SOC analysis focuses on abnormal outbound behavior, staging techniques, and correlating host, network, and log evidence to stop attackers before sensitive data leaves the organization.

