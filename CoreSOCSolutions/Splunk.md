## Splunk - The Basics

### 1. Introduction
Splunk is one of the leading SIEM solutions in the market. It allows users to collect, analyze, and correlate network and machine logs in real time.  
This room explores Splunk’s basic functionalities, visibility benefits, and how it speeds up detection.

---

### 2. Learning Objectives
This room covers the following:

#### Understand Splunk Components  
#### Explore Available Options in Splunk  
#### Learn Log Ingestion Workflow  
#### Ingest & Analyze Logs Practically  

---

### 3. Splunk Components
Splunk consists of three core components that work together to collect, store, and search logs.

#### 3.1 Forwarder
A lightweight agent installed on endpoints to collect and send logs to the Splunk instance.  
Typical data sources include:

- Web server traffic  
- Windows Event Logs, PowerShell, Sysmon  
- Linux host logs  
- Database connection events  

**Answer:** The component used to collect and send data → **Forwarder**

#### 3.2 Indexer
Receives logs from forwarders, parses, normalizes, and stores them as searchable events (field-value pairs).

#### 3.3 Search Head
User interface for querying data using SPL (Search Processing Language).  
Allows transformation into tables and visualizations (bar, pie, column charts).

---

### 4. Navigating Splunk

#### 4.1 Splunk Bar
Top navigation bar with:

- Messages  
- Settings  
- Activity  
- Help  
- Find  

Also used to switch between installed apps.

#### 4.2 Apps Panel
Displays all installed apps.  
Default app: **Search & Reporting**

#### 4.3 Explore Splunk
Provides quick access to:

- Add Data  
- Add Apps  
- Documentation  

#### 4.4 Splunk Dashboard
Default is empty.  
Dashboards can be selected from the list or created by the user.  
User-created dashboards appear under "Yours".

**Answer:** In Add Data → option for collecting data from files & ports → **Monitor**

---

### 5. Adding Data

Splunk can ingest any machine data and convert it into searchable events.  
Data sources include logs from OS, network devices, security solutions, web servers, and more.

In this task, we focus on **VPN logs** uploaded via the **Upload** option.

---

### 6. Practical: Ingesting VPN Logs

#### Upload Steps:
1. **Select Source** - Choose log file  
2. **Select Source Type** - e.g., syslog, JSON  
3. **Input Settings** - Choose index & hostname  
4. **Review** - Confirm configuration  
5. **Done** - Upload completes  

---

### 7. Practical Answers

#### 7.1 Number of events in the VPN log file  
**2862**

#### 7.2 Number of log events by user “Maleena”  
**60**

#### 7.3 Username associated with IP `107.14.182.38`  
**Smith**

#### 7.4 Number of events from all countries except France  
**2814**

#### 7.5 Number of VPN events associated with IP `107.3.206.58`  
**14**
