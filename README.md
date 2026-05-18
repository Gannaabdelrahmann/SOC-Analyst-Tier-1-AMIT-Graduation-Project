# 🛡️ SOC Analyst Tier 1 — Graduation Project

> A hands-on graduation project simulating real-world SOC operations using **Splunk Enterprise** and **LetsDefend** labs — covering SIEM architecture, log management, threat detection, and security monitoring workflows.

**Author:** Ganna Mohamed Abdelrahman  
**Program:** SOC Analyst Tier 1  
**Platform:** LetsDefend

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Reports](#project-reports)
- [Key Implementations](#key-implementations)
- [Skills Demonstrated](#skills-demonstrated)
- [Tools & Technologies](#tools--technologies)
- [Learning Outcomes](#learning-outcomes)
- [Repository Structure](#repository-structure)

---

## Overview

This repository documents a comprehensive SOC Analyst Tier 1 graduation project. The work covers both the theoretical foundations of SIEM platforms and practical, hands-on implementation using Splunk Enterprise — from installation and configuration to active threat monitoring and incident investigation.

All labs were completed on real systems (Windows 11 and Ubuntu Linux) using industry-standard tools, replicating the daily workflow of a Tier 1 SOC analyst.

---

## 📁 Project Reports

### 1. 📘 SIEM Introduction Report

Covers the theoretical and operational foundations of SIEM platforms, including:

| Topic | Details |
|---|---|
| SIEM Architecture | Components, data flow, deployment models |
| Log Collection | Agents, agentless methods, Syslog |
| Log Aggregation & Parsing | Normalization, field extraction |
| EPS (Events Per Second) | Capacity planning fundamentals |
| Storage & Indexing | Hot/Warm/Cold/Archived buckets |
| Alerting Strategies | Threshold-based and correlation rules |
| Analysis Techniques | Blacklisting, whitelisting, long-tail analysis |

📄 [`reports/SIEM 101 Report.pdf`](reports/SIEM%20101%20Report.pdf)

---

### 2. 📗 Splunk Room Report

A complete, step-by-step walkthrough of deploying and operating Splunk Enterprise in a SOC environment, based on the LetsDefend Splunk Room.

| Topic | Details |
|---|---|
| Sizing & Storage Planning | Used the Splunk Storage Sizing tool; calculated 4.7 TB for 200 GB/day over 90 days |
| Installation (Windows) | Installed Splunk Enterprise 9.0.0.10 on Windows 11 |
| Installation (Linux) | Installed via CLI (`wget`) on Ubuntu 24.04 LTS; configured boot-start |
| Universal Forwarder | Configured Windows forwarder to send event logs to the Splunk indexer |
| Data Ingestion | Ingested live Windows event logs and uploaded log archives manually |
| SPL Searching | Wrote and tested queries using wildcards, AND/OR/NOT operators, and field filters |
| Reports & Alerts | Created scheduled reports and real-time/scheduled alerts |
| Dashboards | Built multi-panel dashboards for SOC visibility |
| Health Monitoring | Used the Splunk Health Status dashboard to verify server components |
| User & Role Management | Configured roles, created users, and enforced password policies |

📄 [`reports/Splunk Report.pdf`](reports/Splunk%20Report.pdf)

---

## ⚙️ Key Implementations

### Splunk Deployment

Installed and configured Splunk Enterprise on both Windows and Linux, with the following ports verified and opened:

| Port | Purpose |
|---|---|
| `9997` | Universal Forwarder → Indexer |
| `8000` | Splunk Web Interface |
| `8089` | Management / Deployment Server |

---

### Universal Forwarder Setup

Configured the Splunk Universal Forwarder on Windows 11 to forward Windows Event Logs to the Splunk indexer. Verified connectivity using PowerShell:

```powershell
Test-NetConnection -ComputerName <IndexerIP> -Port 9997
# Expected: TcpTestSucceeded : True
```

---

### Data Ingestion

- Forwarded live **Windows Event Logs** from a Universal Forwarder
- Uploaded **log archives** (`.zip`) directly into Splunk
- Created a custom index `windows_events` to store ingested data

---

### SPL Queries

**Detect failed login attempts targeting admin accounts:**

```spl
source="WinEventLog:*" index="windows_events" EventCode=4625 AND accountname=Admin
```

**Detect successful logins:**

```spl
source="WinEventLog:*" index="windows_events" EventCode=4624
```

**Filter by specific host:**

```spl
eventid=4624 AND computername=computer1
```

---

### Alerts & Reports

- Created a **scheduled report** (daily at 8:00 AM) tracking failed admin login attempts
- Configured a **Splunk alert** triggered when internal index error count exceeded threshold
- Verified alert firing under `Activity > Triggered Alerts`

---

### Dashboards

Built a **Security Analyst Dashboard** with panels for:
- Total events over time
- Failed login attempts
- Events by source type and severity
- Top users by event count
- Recent security alerts

---

## 🧠 Skills Demonstrated

```
SIEM Fundamentals          SOC Tier 1 Operations       Splunk Enterprise
SPL (Search Processing Language)                        Log Collection & Parsing
Windows Event Log Analysis  Linux CLI Administration    Alert Engineering
Threat Detection            Dashboard Creation          Incident Investigation
User & Role Management      Security Monitoring         Capacity Planning
```

---

## 🛠️ Tools & Technologies

| Category | Tools |
|---|---|
| SIEM Platform | Splunk Enterprise 9.0.10 / 10.2.2 |
| Log Forwarding | Splunk Universal Forwarder |
| Operating Systems | Windows 11, Ubuntu 24.04 LTS |
| Virtualization | VMware Workstation Pro 17 |
| Scripting | PowerShell, Bash |
| Protocol | Syslog |
| Lab Platform | LetsDefend SOC Analyst Path |

---

## 📈 Learning Outcomes

Through this project, the following competencies were developed:

- ✅ Understanding end-to-end SIEM data flow (collection → parsing → indexing → alerting)
- ✅ Deploying and administering Splunk in a multi-OS environment
- ✅ Writing SPL queries for real-world threat detection scenarios
- ✅ Building SOC-ready dashboards and scheduled reports
- ✅ Configuring role-based access control in Splunk
- ✅ Simulating and investigating security events (failed logins, privilege escalation indicators)
- ✅ Applying SOC Tier 1 analyst workflows in a hands-on lab environment

**Ganna Mohamed Abdelrahman**  
SOC Analyst Tier 1 — Graduation Project  
*LetsDefend · 2026*

</div>
