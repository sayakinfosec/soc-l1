### Introduction

Wireshark fundamentals for packet-level analysis to investigate events of interest.

### Learning Objectives

* Investigate network traffic captures
* Use statistical views effectively
* Apply packet and protocol filters
* Perform advanced filtering

---

### Statistics | Summary

### Overview

Use **Statistics** to understand traffic scope, protocols, endpoints, and conversations.

### Key Menus

* **Statistics → Summary**: High-level capture overview
* **Statistics → Resolved Addresses**: IP ↔ hostname mapping via DNS
* **Statistics → Protocol Hierarchy**: Protocol usage tree
* **Statistics → Conversations**: Traffic between endpoints
* **Statistics → Endpoints**: Unique endpoints (MAC/IP/Ports)

### Name Resolution & GeoIP

* Enable: `Edit → Preferences → Name Resolution`
* GeoIP: Requires MaxMind DB (`Edit → Preferences → Name Resolution → MaxMind`)

### Questions & Answers

* **IP of hostname starting with "bbc"**
  `Statistics → Resolved Addresses`
  **Answer:** 199.232.24.81

* **Number of IPv4 conversations**
  `Statistics → Conversations → IPv4`
  **Answer:** 435

* **Bytes (k) from "Micro-St" MAC**
  `Statistics → Endpoints → Ethernet`
  **Answer:** 7474

* **IP addresses linked with "Kansas City"**
  `Statistics → Endpoints → IPv4 (GeoIP enabled)`
  **Answer:** 4

* **IP linked with "Blicnet" AS Organisation**
  `Statistics → Endpoints → IPv4 (GeoIP/ASN)`
  **Answer:** 188.246.82.7

---

### Statistics | Protocol Details

### IPv4 / IPv6

* Menu: `Statistics → IPvX Statistics`

### DNS

* Menu: `Statistics → DNS`

### HTTP

* Menu: `Statistics → HTTP`

### Questions & Answers

* **Most used IPv4 destination**
  `Statistics → IPv4 Statistics`
  **Answer:** 10.100.1.33

* **Max DNS request-response time**
  `Statistics → DNS → Service Response Time`
  **Answer:** 0.467897

* **HTTP requests to rad[.]msn[.]com**
  `Statistics → HTTP → Requests`
  **Answer:** 39

---

### Packet Filtering | Principles

### Filter Types

* **Capture Filters**: Applied before capture (BPF syntax)
* **Display Filters**: Applied during analysis (Wireshark syntax)

### Sample Syntax

* Capture: `tcp port 80`
* Display: `tcp.port == 80`

### Comparison Operators

* `==` equal | `!=` not equal | `>` `<` `>=` `<=`

### Logical Operators

* `and` / `or` / `not`

### Tips

* Filters are lowercase
* Green = valid, Red = invalid, Yellow = warning

---

### Packet Filtering | Protocol Filters

### IP Filters

* All IP: `ip`
* Specific IP: `ip.addr == 10.10.10.111`
* Source IP: `ip.src == 10.10.10.111`
* Destination IP: `ip.dst == 10.10.10.111`

### TCP / UDP Filters

* TCP port: `tcp.port == 80`
* UDP port: `udp.port == 53`
* TCP dst port: `tcp.dstport == 80`

### HTTP / DNS Filters

* HTTP only: `http`
* DNS only: `dns`
* HTTP GET: `http.request.method == "GET"`
* DNS A record: `dns.qry.type == 1`

### Questions & Answers

* **Number of IP packets**
  `ip`
  **Answer:** 81420

* **Packets with TTL < 10**
  `ip.ttl < 10`
  **Answer:** 66

* **Packets using TCP port 4444**
  `tcp.port == 4444`
  **Answer:** 632

* **HTTP GET requests to port 80**
  `http.request.method == "GET" && tcp.dstport == 80`
  **Answer:** 527

* **Type A DNS queries**
  `dns.qry.type == 1 && dns.flags.response == 0`
  **Answer:** 51

---

### Advanced Filtering

### Advanced Operators

* **contains**: `http.server contains "Apache"`
* **matches (regex)**: `http.host matches "\\.(php|html)"`
* **in**: `tcp.port in {80 443 8080}`
* **upper()**: `upper(http.server) contains "APACHE"`
* **lower()**: `lower(http.server) contains "apache"`
* **string()**: `string(frame.number) matches "[13579]$"`

### Profiles & Reuse

* Bookmarks & buttons save filters
* Profiles: `Edit → Configuration Profiles`

### Questions & Answers

* **Microsoft IIS packets not from port 80**
  `http.server contains "Microsoft-IIS" && tcp.srcport != 80`
  **Answer:** 21

* **Microsoft IIS version 7.5 packets**
  `http.server contains "Microsoft-IIS/7.5"`
  **Answer:** 71

* **Packets using ports 3333, 4444, 9999**
  `tcp.port in {3333 4444 9999}`
  **Answer:** 2235

* **Packets with even TTL values**
  `ip.ttl % 2 == 0`
  **Answer:** 77289

* **Bad TCP checksum packets (Checksum Control profile)**
  `tcp.checksum_bad == 1`
  **Answer:** 34185

* **Displayed packets using existing filter button**
  *(Predefined button filter)*
  **Answer:** 261
