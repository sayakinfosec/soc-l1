## Network Miner - Network Forensics Tool

NetworkMiner is an open-source Network Forensic Analysis Tool (NFAT) developed by Netresec. It supports passive traffic analysis and offline PCAP investigation to identify hosts, sessions, credentials, files, and anomalies without injecting traffic into the network. Widely used by incident response teams and law enforcement, it excels at quickly extracting forensic artifacts from network captures.

---

### NetworkMiner in Forensics
Network forensics focuses on identifying malicious activity, breaches, and anomalies using network data. NetworkMiner accelerates this process by providing:
- Host context (IP, MAC, hostname, OS)
- High-level attack indicators (scans, spikes, anomalies)
- Identification of attacker tools (e.g., Nmap)
It is best suited for initial triage and evidence extraction rather than deep packet analysis.

---

### Supported Data Types
NetworkMiner can analyze:
- Live traffic
- PCAP traffic captures
- Log files  
This lab focuses on live and captured traffic analysis.

---

### What is NetworkMiner?
NetworkMiner provides:
- Traffic sniffing (limited, Windows only)
- PCAP parsing and session reconstruction
- Protocol identification
- OS fingerprinting (via p0f and Satori)
- File extraction (images, HTML, emails)
- Credential extraction
- Cleartext keyword discovery  
The free edition is sufficient for forensic triage, while the professional version adds OSINT and advanced features.

---

### Operating Modes
- **Sniffer Mode**: Passive capture; not recommended as a primary sniffer
- **Packet Parsing/Processing**: Preferred mode for extracting low-hanging forensic artifacts from PCAPs

---

### Pros and Cons
**Pros**
- OS fingerprinting
- Easy file and credential extraction
- Cleartext keyword parsing
- Fast traffic overview

**Cons**
- Weak for live sniffing
- Inefficient for very large PCAPs
- Limited filtering
- Not designed for manual packet-level analysis

---

### NetworkMiner vs Wireshark
NetworkMiner is optimized for rapid overview and extraction, while Wireshark is built for deep protocol and packet analysis. Best practice is to triage with NetworkMiner and investigate further using Wireshark.

---

### Tool Overview - Part 1
Key interface components:
- **Landing Page**: Initial dashboard
- **File Menu**: Load PCAPs or receive PCAP over IP
- **Tools Menu**: Clear dashboards and cases
- **Help Menu**: Version and update info
- **Case Panel**: Manage loaded PCAP files and metadata

### Hosts
Displays identified hosts with:
- IP and MAC addresses
- OS fingerprint
- Open ports
- Packet and session counts  
Supports sorting, coloring, and quick copying of values.

### Sessions
Shows detected sessions including:
- Client/server IPs
- Ports
- Protocol
- Frame number and start time  
Supports keyword filtering using exact phrases, regex, or word matching.

### DNS
Displays DNS queries and responses with:
- Query/answer details
- TTL, transaction ID, timestamps
- Client/server info  
Useful for spotting suspicious or anomalous domains.

### Credentials
Extracts credentials and hashes such as:
- NTLM and Kerberos hashes
- HTTP, FTP, SMTP, IMAP credentials
- RDP cookies  
Hashes can be exported for cracking with Hashcat or John the Ripper.

---

### Exercise: mx-3.pcap
- Total frames: **460**
- IPs sharing MAC with 145.253.2.203: **2**
- Packets sent from 65.208.228.223: **72**
- Webserver banner: **Apache**

---

### Exercise: mx-4.pcap
- Extracted username: **#B\\Administrator**
- Extracted NTLMv2 hash:
  `$NETNTLMv2$#B$136B077D942D9A63$FBFF3C253926907AAAAD670A9037F2A5$01010000000000000094D71AE38CD60170A8D571127AE49E00000000020004003300420001001E003000310035003600360053002D00570049004E00310036002D004900520004001E0074006800720065006500620065006500730063006F002E0063006F006D0003003E003000310035003600360073002D00770069006E00310036002D00690072002E0074006800720065006500620065006500730063006F002E0063006F006D0005001E0074006800720065006500620065006500730063006F002E0063006F006D00070008000094D71AE38CD601060004000200000008003000300000000000000000000000003000009050B30CECBEBD73F501D6A2B88286851A6E84DDFAE1211D512A6A5A72594D340A001000000000000000000000000000000000000900220063006900660073002F003100370032002E00310036002E00360036002E0033003600000000000000000000000000`

---

### Tool Overview - Part 2
Additional analysis tabs include:
- **Files**: Extracted files with metadata
- **Images**: Reconstructed images with source details
- **Parameters**: Extracted request parameters
- **Keywords**: Indexed cleartext keywords
- **Messages**: Emails, chats, attachments
- **Anomalies**: Basic exploit and spoofing detections

---

### Exercise: mx-7.pcap
- Linux distro (frame 63075): **CentOS**
- Page header (frame 75942): **Password-Ned AB**
- Image source IP: **80.239.178.187**
- TLS anomaly frame: **36255**

---

### Exercise: mx-9.pcap
- Email platform: **Facebook**
- Email address: **branson@sandsite.org**

---

### Version Differences
- Duplicate MAC detection: **v2.7**
- Frame handling: **v1.6**
- Detailed packet inspection: **v1.6**
Newer versions improve correlation and parameter handling, while older versions expose more raw packet detail.

---

### Exercises - Case Files
**case1.pcap**
- OS of 131.151.37.122: **Windows NT 4**
- Bytes received via port 1065: **192**
- Bytes received via port 143: **20769**
- Frame 9 sequence number: **2AD77400**
- Detected content types: **2**

**case2.pcap**
- USB brand: **ASIX**
- Phone model: **Lumia 535**
- Image source IP: **50.22.95.9**
- Email password: **spring2015**
- DNS query (frame 62001): **pop.gmx.com**

---

### Conclusion
NetworkMiner should not be used as a primary packet sniffer. It is best leveraged for rapid forensic triage, credential and file extraction, and host identification before transitioning to Wireshark or tcpdump for deep packet-level analysis.
