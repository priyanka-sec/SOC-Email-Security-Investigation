# ⚔️ Attack Scenario

## 📌 Overview

This project simulates a phishing attack in a controlled lab environment to demonstrate how a Security Operations Center (SOC) analyst investigates email-based threats.

The objective was to replicate a realistic phishing campaign, deliver the email through SMTP, capture the associated network traffic, analyze the email headers, and identify Indicators of Compromise (IOCs).

The attack was performed entirely inside an isolated VirtualBox lab environment for educational and defensive security purposes.

<br><br>

# 🎯 Attack Objectives

The attacker attempted to:

* Deliver a phishing email to a target user
* Create urgency using a password expiration theme
* Convince the victim to click a malicious link
* Simulate credential harvesting behavior
* Demonstrate a common Initial Access technique used by threat actors

The SOC analyst objective was to:

* Investigate the phishing email
* Identify attacker infrastructure
* Extract Indicators of Compromise (IOCs)
* Validate evidence using logs and network traffic
* Map activity to MITRE ATT&CK
* Develop detection opportunities

<br><br>

# 🏗️ Lab Environment

| Component           | Role                          | IP Address          |
| ------------------- | ----------------------------- | ------------------- |
| Kali Linux          | Attacker Machine              | 192.168.56.10       |
| Windows Server 2022 | Victim Mail Server            | 192.168.56.110      |
| hMailServer         | SMTP Service                  | 192.168.56.110      |
| DNS Server          | SPF / DKIM / DMARC Validation | 192.168.56.110      |
| Wireshark           | Network Packet Capture        | Multiple Interfaces |
| Sysmon              | Endpoint Monitoring           | Windows Server 2022 |

<br><br>

# 🎭 Social Engineering Scenario

The phishing email was designed to imitate a password expiration notification.

The goal was to create urgency and encourage the recipient to click a link without verifying its legitimacy.

Common attacker techniques used:

✅ Urgency

✅ Account Expiration Theme

✅ Credential Harvesting Lure

✅ Trusted Service Impersonation

✅ Email-Based Initial Access

<br><br>

# 📧 Phishing Email Details

| Field           | Value                                           |
| --------------- | ----------------------------------------------- |
| From            | [attacker@lab.local](mailto:attacker@lab.local) |
| To              | [victim@lab.local](mailto:victim@lab.local)     |
| Subject         | Password Expiry Notification                    |
| Delivery Method | SMTP                                            |
| Tool Used       | swaks                                           |
| Payload Type    | Malicious URL                                   |
| Objective       | Credential Harvesting                           |

<br><br>

# 🔗 Malicious Link

The phishing email contained a simulated credential harvesting URL.

```text
http://192.168.56.10/reset
```

In a real-world attack, this link would typically redirect users to a fake login page designed to steal credentials.

<br><br>

# 🚀 Attack Execution

The phishing email was delivered from the Kali Linux attacker machine using the SMTP testing tool swaks.

Example command:

```bash
swaks --to victim@lab.local \
--from attacker@lab.local \
--server 192.168.56.110 \
--header "Subject: Password Expiry Notification"
```

The command successfully established an SMTP connection with the mail server and delivered the email.

<br><br>

# 📨 Email Delivery Process

The attack followed the standard SMTP workflow.

```text
Attacker (Kali Linux)
        │
        ▼
SMTP Connection Established
        │
        ▼
hMailServer Receives Email
        │
        ▼
Email Stored in Mailbox
        │
        ▼
SOC Investigation Begins
```

<br><br>

# 🌐 Network Activity Generated

The attack generated observable network traffic.

Key protocol:

```text
SMTP (Port 25)
```

Observed Activity:

* SMTP session initiation
* SMTP commands exchanged
* Email content transmission
* Mail server acceptance
* Session termination

These activities were captured using Wireshark.

<br><br>

# 🔍 Evidence Collected

The following evidence was collected during the attack simulation.

### SMTP Connectivity Verification

```text
12_KaliLinux_SMTP_Connectivity_Test.jpg
```

### Successful Email Delivery

```text
13_KaliLinux_Phishing_Email_Sent.jpg
```

### Mail Server Logs

```text
14_hMailServer_Email_Received_Logs.jpg
```

### SMTP Traffic Capture

```text
20_Wireshark_SMTP_Email_Traffic.jpg
```

### PCAP Preservation

```text
21_Wireshark_PCAP_Saved.jpg
```

### End-to-End Validation

```text
25_End_to_End_Email_Flow_Validation.jpg
```

<br><br>

# 🧠 MITRE ATT&CK Mapping

The simulated attack maps to the following MITRE ATT&CK techniques.

| Tactic         | Technique                | ID        |
| -------------- | ------------------------ | --------- |
| Initial Access | Phishing                 | T1566     |
| Initial Access | Spearphishing Link       | T1566.002 |
| Reconnaissance | Phishing for Information | T1598     |
| Reconnaissance | Spearphishing Link       | T1598.003 |

<br><br>

# 🚨 Detection Opportunities

A SOC team could detect this activity through:

* SMTP traffic monitoring
* Email gateway analysis
* Suspicious sender detection
* Header anomaly detection
* URL reputation checks
* Mail server log monitoring
* Sysmon network connection events
* SIEM correlation rules

<br><br>

# 📊 Attack Timeline

| Time | Activity                           |
| ---- | ---------------------------------- |
| T0   | SMTP connectivity verified         |
| T1   | Phishing email crafted             |
| T2   | Email delivered via swaks          |
| T3   | hMailServer accepted message       |
| T4   | SMTP traffic captured in Wireshark |
| T5   | Email headers extracted            |
| T6   | IOC extraction completed           |
| T7   | MITRE ATT&CK mapping performed     |
| T8   | Detection opportunities documented |

<br><br>

# 🎯 Outcome

The phishing email was successfully delivered from the attacker machine to the target mail server.

The attack generated realistic email artifacts, network traffic, mail server logs, and forensic evidence that were later used throughout the SOC investigation process.

This simulation demonstrates how phishing attacks operate and how SOC analysts identify, investigate, validate, and document email-based threats using industry-standard tools and methodologies.

