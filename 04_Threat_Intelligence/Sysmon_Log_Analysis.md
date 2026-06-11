# 🖥️ Sysmon Log Analysis

## 🎯 Objective

This document provides an analysis of Sysmon (System Monitor) logs collected during the phishing email investigation lab.

Sysmon was deployed on the Windows Server 2022 system to provide enhanced visibility into system activity, network connections, and process execution that would not normally be available through standard Windows Event Logs.

The purpose of this analysis was to identify evidence related to the phishing email delivery and validate attacker activity observed through other investigation sources.

<br><br>

# 📌 Why Sysmon Was Used

Microsoft Sysmon is an advanced Windows logging tool from Sysinternals that records detailed system activity.

For SOC analysts, Sysmon provides valuable telemetry for:

* 🔍 Process Creation Monitoring
* 🌐 Network Connection Tracking
* 📁 File Activity Monitoring
* 🧠 Threat Hunting
* 🚨 Detection Engineering
* 📊 Incident Investigation

During this lab, Sysmon was configured to collect network connection events that could help validate SMTP communication between the attacker and the victim mail server.

<br><br>

# 🏗️ Sysmon Deployment Details

| Configuration Item  | Value                                                         |
| ------------------- | ------------------------------------------------------------- |
| Host System         | Windows Server 2022                                           |
| Monitoring Tool     | Sysmon                                                        |
| Vendor              | Microsoft Sysinternals                                        |
| Configuration       | SwiftOnSecurity Sysmon Configuration                          |
| Log Source          | Applications and Services Logs → Microsoft → Windows → Sysmon |
| Investigation Focus | Network Connections                                           |

<br><br>

# 🔍 Investigation Goal

The primary objective was to determine whether Windows telemetry could confirm the network activity observed during:

* SMTP communication
* Email delivery
* Attacker-to-server connections

The findings would then be correlated with:

* Wireshark PCAP data
* hMailServer logs
* Email header evidence

<br><br>

# 📊 Event IDs Reviewed

## Event ID 1 — Process Creation

Records newly created processes.

### SOC Use Cases

* Malware Execution
* Script Execution
* Living-off-the-Land Activity
* Suspicious Tool Execution

### Relevance to This Investigation

No malicious process execution was observed on the Windows Server.

<br><br>

## Event ID 3 — Network Connection

Records outbound network connections initiated by processes.

### SOC Use Cases

* C2 Detection
* Data Exfiltration
* Email Delivery Tracking
* Threat Hunting

### Relevance to This Investigation

This was the most important Sysmon event analyzed during the investigation.

Network activity associated with SMTP communication was identified and correlated with the phishing attack timeline.

<br><br>

## Event ID 22 — DNS Query

Records DNS lookup activity.

### SOC Use Cases

* Domain Hunting
* Malware Investigation
* IOC Discovery

### Relevance to This Investigation

DNS activity was reviewed to validate email authentication records and DNS configuration.

<br><br>

# 🌐 Network Connection Analysis

## Event Reviewed

### Sysmon Event ID 3

This event records network connections created by processes running on the monitored system.

### Key Investigation Questions

* Did the server receive SMTP traffic?
* Was the attacker IP observed?
* Does the activity match Wireshark evidence?
* Can the timeline be validated?

<br><br>

## Observed Evidence

| Indicator        | Value               |
| ---------------- | ------------------- |
| Source Host      | Kali Linux          |
| Source IP        | 192.168.56.10       |
| Destination Host | Windows Server 2022 |
| Destination IP   | 192.168.56.110      |
| Protocol         | TCP                 |
| Service          | SMTP                |
| Port             | 25                  |

<br><br>

# 🔗 Evidence Correlation

The following sources all supported the same conclusion.

| Evidence Source   | Observation                     |
| ----------------- | ------------------------------- |
| Wireshark         | SMTP session observed           |
| hMailServer Logs  | Email successfully delivered    |
| Email Header      | Attacker IP identified          |
| Sysmon Event ID 3 | Network communication confirmed |

The correlation of multiple evidence sources significantly increased confidence in the investigation findings.

<br><br>

# 📧 SMTP Activity Validation

The SMTP communication observed during the phishing simulation matched:

* Source IP from email headers
* SMTP traffic from Wireshark
* Mail delivery records from hMailServer
* Sysmon network telemetry

This demonstrated successful end-to-end validation of the phishing attack.

<br><br>

# 🚨 Detection Opportunities

The investigation identified several opportunities for SOC monitoring.

## Detection Opportunity 1

### Suspicious SMTP Connections

Monitor systems communicating directly over SMTP (TCP/25).

### Why It Matters

Direct SMTP communication can indicate:

* Phishing campaigns
* Spam activity
* Unauthorized mail servers

<br><br>

## Detection Opportunity 2

### Unusual Internal SMTP Traffic

Alert when workstations or non-mail systems initiate SMTP connections.

### Why It Matters

Normal users rarely communicate directly over SMTP.

<br><br>

## Detection Opportunity 3

### Correlation With Email Headers

Create detections that compare:

* SMTP logs
* Sysmon network events
* Email header IP addresses

### Why It Matters

Helps identify spoofing attempts and suspicious senders.

<br><br>

# 🧠 SOC Analyst Findings

The Sysmon logs successfully provided host-based evidence supporting the phishing email investigation.

Key findings included:

✅ SMTP-related network activity observed

✅ Network connections matched attacker infrastructure

✅ Activity correlated with Wireshark packet captures

✅ Activity correlated with hMailServer delivery logs

✅ Investigation timeline successfully validated

No evidence of malware execution or post-delivery compromise was observed during the lab simulation.

<br><br>

# 📋 Conclusion

Sysmon proved to be a valuable source of host-based telemetry during the phishing investigation.

Although the attack focused on email delivery rather than malware execution, Sysmon provided additional visibility into network activity and helped validate findings collected from other evidence sources.

The combination of:

* Sysmon Logs
* Wireshark PCAP Analysis
* Email Header Analysis
* hMailServer Logs

enabled a complete reconstruction of the phishing attack lifecycle.

<br><br>

# 🏁 Final Assessment

| Category                           | Result       |
| ---------------------------------- | ------------ |
| Evidence Source                    | Sysmon Logs  |
| Critical Event Reviewed            | Event ID 3   |
| SMTP Activity Confirmed            | ✅ Yes        |
| Attacker IP Correlated             | ✅ Yes        |
| Timeline Validation                | ✅ Successful |
| Detection Opportunities Identified | ✅ Yes        |
| Investigation Confidence           | 🔴 High      |

**Analyst Verdict:** Sysmon telemetry successfully supported the phishing email investigation and provided valuable network-level evidence for attack reconstruction.

