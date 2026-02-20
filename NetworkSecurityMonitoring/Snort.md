
## 🐷 Snort - Network Intrusion Detection & Prevention

**Snort** is an open-source Network Intrusion Detection System (NIDS) and Intrusion Prevention System (NIPS) that performs real-time traffic analysis and packet logging.

It detects attacks based on **rules (signatures)** and can run in sniffing, packet logging, or intrusion detection mode.

---

### 📌 What Snort Does

* Monitors network traffic in real time
* Detects malicious patterns using rules
* Generates alerts for suspicious activity
* Can drop/block traffic (IPS mode)
* Supports packet capture (pcap analysis)

---

### ⚙️ Installation (Ubuntu Example)

```bash
sudo apt update
sudo apt install snort -y
```

Verify installation:

```bash
snort -V
```

---

### 🧠 Snort Operating Modes

1. **Sniffer Mode** - Reads packets and displays them

   ```bash
   snort -v
   ```

2. **Packet Logger Mode** - Logs packets to disk

   ```bash
   snort -dev -l ./log
   ```

3. **IDS Mode** - Detects traffic based on rules

   ```bash
   snort -c /etc/snort/snort.conf -i eth0
   ```

4. **Read from PCAP File**

   ```bash
   snort -r capture.pcap
   ```

---

### 📂 Important Files & Directories

| Path                           | Purpose                            |
| ------------------------------ | ---------------------------------- |
| `/etc/snort/snort.conf`        | Main configuration file            |
| `/etc/snort/rules/`            | Rule files                         |
| `/var/log/snort/`              | Alert & log output                 |
| `/etc/snort/snort.debian.conf` | Interface settings (Debian/Ubuntu) |

---

### 📝 Basic Rule Structure

```
action protocol src_ip src_port -> dest_ip dest_port (options)
```

Example:

```
alert icmp any any -> any any (msg:"ICMP Detected"; sid:1000001; rev:1;)
```

#### Rule Components:

* **action** → alert, log, drop
* **protocol** → tcp, udp, icmp
* **IP/Port** → source and destination
* **msg** → alert message
* **sid** → unique rule ID
* **rev** → revision number

---

### 🔎 Common Commands for Beginners

Test configuration:

```bash
snort -T -c /etc/snort/snort.conf
```

Run with console alerts:

```bash
snort -A console -q -c /etc/snort/snort.conf -i eth0
```

---

### 📊 Alert Output Example

```
[**] [1:1000001:1] ICMP Detected [**]
[Priority: 0]
03/10-12:33:44.123456 192.168.1.5 -> 8.8.8.8
```

---

### 🚀 Beginner Workflow

1. Install Snort
2. Identify network interface (`ip a`)
3. Test config (`-T`)
4. Add a custom rule
5. Run in IDS mode
6. Generate test traffic (e.g., ping)
7. Observe alerts

---

### 🛡️ When to Use Snort

* Learning IDS fundamentals
* SOC lab simulations
* Packet-level threat detection
* Signature-based detection experiments

---

### 📚 Key Concepts to Remember

* Snort is **signature-based detection**
* Rules drive detection logic
* Needs proper network interface configuration
* Works best with packet capture understanding
* Can integrate with SIEM tools

---

### 🔥 Quick Tip for Labs

* Use a NAT + Internal Network lab setup
* Generate traffic from attacker VM
* Monitor from Snort machine
* Keep rules minimal while learning

---

### 📎 Resources

* Official Documentation: [https://www.snort.org/documents](https://www.snort.org/documents)
* Rule Writing Guide: [https://docs.snort.org](https://docs.snort.org)

