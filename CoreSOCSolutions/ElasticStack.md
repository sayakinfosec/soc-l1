## Elastic Stack - The Basics

### 1. Introduction
Elastic Stack (ELK) can be used for log analysis and investigations.  
Although not a traditional SIEM, SOC teams widely use it due to its strong search and visualization capabilities.  
This room explores ELK components, log analysis, visualizations, and dashboards.

---

### 2. Learning Objectives

#### 2.1 Understand ELK Components & SOC Usage  
#### 2.2 Explore ELK Features  
#### 2.3 Search & Filter Data in ELK  
#### 2.4 Investigate VPN Logs for Anomalies  
#### 2.5 Create Visualizations & Dashboards  

---

### 3. Elastic Stack Overview
Elastic Stack (ELK) was originally designed for storing, searching, and visualizing large datasets.  
Today, it is widely used in SOC operations for log analysis.

ELK components work together to collect, normalize, index, and visualize logs from any source.

---

### 4. ELK Components 🔥

#### 4.1 Beats  (Data Collection Agents)
Lightweight agents (data shippers) that send log data from endpoints to Elasticsearch.  
Examples: Winlogbeat, Filebeat, Packetbeat, Metricbeat, etc.

#### 4.2 Logstash  (Data Input/ Filter/ Process & Output)
A data processing engine. Configuration consists of:

- **Input** - Log source  
- **Filter** - Parsing/normalization  
- **Output** - Send processed data to Elasticsearch, Kibana, ports, or files  

#### 4.3 Elasticsearch  (Index & Store Data)
A full-text search & analytics engine storing JSON documents.  
Supports RESTful API interactions.

#### 4.4 Kibana  (Analysis & Visualization)
A web-based interface for analysis, investigation, dashboards, and visualization.

#### 4.5 How ELK Works Together

1. Beats collect logs from endpoints.  
2. Logstash ingests, parses, and normalizes logs.  
3. Elasticsearch stores and indexes the processed data.  
4. Kibana displays, searches, filters, and visualizes the data.

---

### 5. Questions & Answers (Section 1)

**Q:** Logstash is used to visualize the data (yay/nay)  
**A:** nay  

**Q:** Elastic Stack supports all data formats apart from JSON (yay/nay)  
**A:** nay  

---

### 6. Discover Tab

The Discover tab is where SOC analysts spend most of their time.  
It provides raw logs, fields, filters, queries, and time-based views.

#### 6.1 Key Elements of Discover

- **Logs** - Each row = a single log event  
- **Fields Pane** - Left panel listing normalized fields  
- **Index Pattern** - Determines which dataset is being analyzed  
- **Search Bar** - Free text or KQL queries  
- **Time Filter** - Filter logs by date/time  
- **Time Interval (Histogram)** - Shows event spikes  
- **Top Bar** - Save, share, load searches  
- **Add Filter** - Add logic-based filters without writing queries  

#### 6.2 Index Pattern  
Defines which indices Kibana should query.  
Each log source creates its own index pattern.

Example used in lab: **vpn_connections**

#### 6.3 Fields Pane  
Displays all normalized fields.  
Clicking a field shows top values and allows quick filtering (+ / -).

#### 6.4 Time Filter  
Filter logs by predefined or custom date ranges.

#### 6.5 Timeline  
Histogram showing event volumes over time.  
Useful for spotting spikes (e.g., 11 Jan 2022).

#### 6.6 Create Table  
Select fields to build cleaner, noise-free table views.  
Tables can be saved for future sessions.

---

### 7. Questions & Answers (Discover Tab)

**Hits returned between 31 Dec 2021 - 2 Feb 2022:** **2861**  
**IP with maximum connections:** **238.163.231.224**  
**User with maximum traffic:** **James**  
**For User Emanda → SourceIP with max hits:** **107.14.1.247**  
**IP causing spike on 11 Jan:** **172.201.60.191**  
**Connections from 238.163.231.224 excluding New York:** **48**  
**Create Table:** No answer required  

---

### 8. KQL Overview

KQL (Kibana Query Language) allows searching through:

#### 8.1 Free Text Search  
Searches for whole terms unless wildcard (`*`) is used.

Examples:
- `United States` → Matches full term  
- `United` → No results  
- `United*` → Matches United States, United Kingdom, etc.

#### 8.2 Logical Operators  
- `AND`  
- `OR`  
- `NOT`

Examples:
- `"United States" AND "Virginia"`  
- `"United States" OR "England"`  
- `"United States" AND NOT ("Florida")`  

#### 8.3 Field-Based Search  
Syntax: `Field : Value`

Example:  
`Source_ip: 238.163.231.224 AND UserName: Suleman`

---

### 9. Questions & Answers (KQL)

**Records where Source_Country = United States AND (User = James OR Albert):** **161**  
**VPN connections by terminated user Johny Brown after 1 Jan 2022:** **1**  

---

### 10. Creating Visualizations

Kibana allows visualizations such as:

- Tables  
- Pie Charts  
- Bar Charts  
- Correlations  

#### 10.1 Visualization Workflow

1. Select fields  
2. Choose visualization type  
3. Adjust correlations (optional)  
4. Save visualization → Add to library  

#### 10.2 Examples Covered

- Correlation between Source_IP & Source_Country  
- Pie chart of TOP 5 Source Countries  
- Table visualizations  

---

### 11. Questions & Answers (Visualizations)

**User with most failed attempts:** **Simon**  
**Failed VPN connection attempts in January:** **274**  

---

### 12. Creating Dashboards

Dashboards help visualize multiple saved searches and visualizations together.

#### Steps

1. Go to Dashboard tab  
2. Click **Create Dashboard**  
3. **Add from Library**  
4. Arrange items  
5. Save the dashboard  

