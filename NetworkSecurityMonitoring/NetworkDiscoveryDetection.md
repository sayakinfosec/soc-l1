## Network Discovery Detection

### Network Discovery

Attackers and Network Discovery  
Attackers begin by identifying an organisation’s publicly exposed attack surface. During this phase, they attempt to gather information such as accessible assets, IP addresses, open ports, operating systems, running services, and service versions. The goal is to find weaknesses that can be exploited to gain initial access.

Defenders and Network Discovery  
Defenders also perform network discovery to maintain visibility of their environment. Their objectives include maintaining an accurate asset inventory, ensuring only required services and ports are exposed, and confirming that vulnerabilities are patched. The overall aim is to minimise the attack surface.

The Challenge in Detecting Network Discovery  
Both benign and malicious entities perform discovery actions. SOC teams must differentiate between legitimate scanning and hostile reconnaissance. Common approaches include allowlisting trusted scanners, integrating threat intelligence to identify known malicious sources, and using behavioural detection to flag suspicious scanning patterns.
```
Question: What do attackers scan, other than IP addresses, ports, and OS version, to identify vulnerabilities in a network? 
Answer: Services
```
---

### External vs Internal Scanning

External Scanning Activity  
External scanning originates outside the organisation and targets public-facing assets. This activity represents the reconnaissance phase of an attack and is typically low severity, as the attacker does not yet have an internal foothold.

Internal Scanning Activity  
Internal scanning occurs when a compromised internal host scans other internal assets. This indicates progression into the discovery phase and is high severity, requiring escalation and incident response.

Identifying Internal and External Scanning  
Firewall logs can be analysed to distinguish scanning activity based on source and destination IP addresses.

```
Question: Which file contains logs that showcase internal scanning activity? 
Answer: log-session-2.csv  

Question: How many log entries are present for the internal IP performing internal scanning activity? 
Answer: 2276  

Question: What is the external IP address performing external scanning activity? 
Answer: 203.0.113.25
```
---

### Horizontal vs Vertical Scanning

Horizontal Scanning  
A horizontal scan targets the same port across multiple hosts to identify systems exposing a specific service.

Vertical Scanning  
A vertical scan targets multiple ports on a single host to identify exposed services and potential vulnerabilities.

Detection Logic  
Horizontal scans show one source IP, one destination port, and multiple destination IPs.  
Vertical scans show one source IP, one destination IP, and multiple destination ports.

```
Question: Which IP range was scanned horizontally? 
Answer: 203.0.113.0/24  

Question: Which IP address was vertically scanned? 
Answer: 192.168.230.145  

Question: Which ports were scanned on one of the IP addresses? 
Answer: 80, 445, 3389
```
---

### The Mechanics of Scanning

Ping Sweep  
Uses ICMP to identify live hosts and is often blocked by modern security controls.

TCP SYN Scan  
Uses partial TCP handshakes to identify open ports and active hosts in a stealthy manner.

UDP Scan  
Relies on ICMP responses or timeouts to infer port states, making it slow and unreliable.

Identifying Scan Types  
Firewall and Zeek logs analysed in Kibana can reveal scan techniques based on protocol behaviour and connection states.

```
Question: Which source IP performs a ping sweep across a whole subnet? 
Answer: 192.168.230.127  

Question: What type of scan is performed by 203.0.113.25 against 192.168.230.145? 
Answer: TCP SYN Scan  

Question: Is there any UDP scanning attempt in the logs? 
Answer: N
```
---

### Conclusion

Network discovery is a critical phase of the attack lifecycle and is performed by both attackers and defenders. Effective detection relies on understanding scanning techniques, distinguishing internal and external activity, and correlating log behaviour to identify malicious intent while reducing false positives.
