## Network Traffic Basics

### Introduction

Network Traffic Analysis (NTA) involves capturing, inspecting, and analyzing data as it flows through a network. Its goal is complete visibility of internal and external communication. NTA is not limited to Wireshark-it includes correlating logs, deep packet inspection, and network flow statistics.

Understanding network traffic is essential for SOC analysts and other security roles. It allows identifying normal behavior and spotting deviations.

---

### Purpose of Network Traffic Analysis

Network traffic analysis helps:

* Monitor network performance.
* Detect abnormalities (performance peaks, slowness).
* Inspect suspicious internal and external communication (exfiltration, malicious downloads, lateral movement).
* Detect malicious activity.
* Reconstruct attacks in incident response.
* Validate alerts.

#### Example: DNS Tunneling & Beaconing

Unusual DNS queries can indicate command-and-control activity. DNS logs reveal:

* Query and query type
* Subdomain and TLD (can be checked in reputation tools)
* Host IP (source of DNS traffic)
* Destination IP
* Timestamp (timeline creation)

Logs alone cannot reveal the full content of DNS queries-packet inspection is required to detect encoded C2 commands.

**Technique used to smuggle C2 commands via DNS:** DNS tunneling

---

### What Network Traffic Can We Observe?

Network traffic visibility aligns with the TCP/IP stack. Each layer adds headers that contain valuable information.

#### Layer Breakdown

```
                                             Application Header + Data       <-- Application
                          Transport Header | Application Header + Data       <-- Transport
              IP Header | Transport Header | Application Header + Data       <-- Internet
Link Header | IP Header | Transport Header | Application Header + Data       <-- Data Link
```

#### Application Layer

Example: HTTP GET request and server response. Logs show headers but not payloads (e.g., ZIP file contents).

**ZIP attachment size in the HTTP example:** 10485760 bytes

#### Transport Layer

Firewall logs commonly show ports and flags but not sequence numbers needed to detect session hijacking.

**Field used to detect session hijacking:** Sequence number

#### Internet Layer

Fragmentation attacks (evasion technique) can only be detected by inspecting fragment offsets.

**Attack used to evade IDS:** Fragmentation

#### Link Layer

ARP spoofing/poisoning requires full packet context (MAC address anomalies).

---

### Network Traffic Sources and Flows

Network traffic sources fall under two categories:

* **Intermediary:** firewalls, switches, web proxies, routers, IDS/IPS
* **Endpoint:** servers, hosts, IoT, VMs, mobile devices

**Category generating the most traffic:** Endpoint

#### Traffic Flow Types

* **North-South:** LAN ↔ WAN traffic (HTTPS, DNS, VPN, SMTP)
* **East-West:** internal LAN traffic (AD, SMB, infrastructure services)

#### SMB Flow

Before establishing an SMB session, Kerberos authentication occurs.

**Service contacted first:** Kerberos

#### HTTPS Flow

TLS inspection introduces dual sessions-client → proxy and proxy → server.

**TLS stands for:** Transport Layer Security

---

### How Can We Observe Network Traffic?

Observation methods include:

* Logs
* Full packet capture
* Network statistics

#### Logs

Useful but incomplete-vendors choose what to log.

#### Full Packet Capture

Methods:

* **Network TAP:** Hardware placed inline; duplicates traffic with no performance loss.
* **Port Mirroring (SPAN):** Software duplication of packets to a monitoring port.

Key considerations:

* Placement
* Storage requirements
* TAP vs mirroring performance

#### Tools

* Wireshark
* TCPdump
* IDS/IPS (Snort, Suricata, Zeek)

#### Network Statistics

Protocols:

* **NetFlow:** Cisco-developed metadata export protocol.
* **IPFIX:** Vendor-neutral successor with flexible field configuration.

These reveal flow-level anomalies (C2 activity, exfiltration, lateral movement).
