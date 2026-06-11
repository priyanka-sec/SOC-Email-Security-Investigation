# 📧 Email Header Analysis

## 📌 Overview

Email header analysis is one of the most important skills for a SOC Analyst investigating phishing attacks.

Email headers contain critical forensic information that helps identify:

* Sender infrastructure
* Originating IP addresses
* Email routing path
* Mail transfer agents
* Authentication results
* Suspicious indicators
* Threat actor tooling

In this investigation, the phishing email delivered during the attack simulation was analyzed to identify Indicators of Compromise (IOCs) and reconstruct the attack path.

<br><br>

# 🎯 Investigation Objectives

The primary objectives of this analysis were:

* Identify the true sender of the email
* Determine the originating IP address
* Validate the email delivery path
* Extract Indicators of Compromise (IOCs)
* Identify attacker tooling
* Correlate findings with network and log evidence
* Support incident response activities

<br><br>

# 📨 Email Summary

| Field                | Value                                           |
| -------------------- | ----------------------------------------------- |
| Sender               | [attacker@lab.local](mailto:attacker@lab.local) |
| Recipient            | [victim@lab.local](mailto:victim@lab.local)     |
| Subject              | Password Expiry Notification                    |
| Message Type         | Phishing Email                                  |
| Delivery Method      | SMTP                                            |
| Investigation Status | Confirmed Phishing Simulation                   |

<br><br>

# 🔍 Raw Header Evidence

The email headers were extracted from the received message and reviewed manually.

Key evidence sources included:

* Received headers
* Return-Path
* Message-ID
* X-Mailer
* SMTP routing information

Evidence Screenshot:

```text id="header1"
15_Email_Raw_Header_Extraction.jpg
```

<br><br>

# 🌐 Received Header Analysis

## Purpose

The Received header is one of the most important fields during email investigations.

It records the path an email takes from sender to recipient.

SOC analysts typically read Received headers from bottom to top because each mail server appends its own entry.

<br><br>

## Evidence Observed

Example:

```text id="header2"
Received: from kali (192.168.56.10)
by mail.lab.local with SMTP;
Sun, 07 Jun 2026 19:30:15 +0530
```

<br><br>

## Findings

| Observation        | Value            |
| ------------------ | ---------------- |
| Source Hostname    | kali             |
| Source IP Address  | 192.168.56.10    |
| Destination Server | mail.lab.local   |
| Protocol           | SMTP             |
| Result             | Message Accepted |

<br><br>

## Analyst Conclusion

The email originated from the Kali Linux attacker machine and was delivered directly to the hMailServer instance running on Windows Server 2022.

This finding matches:

* SMTP traffic captured in Wireshark
* hMailServer SMTP logs
* Sysmon network connection events

<br><br>

# 🎯 Attacker IP Identification

One of the primary goals of email header analysis is identifying the originating IP address.

Evidence Screenshot:

```text id="header3"
15(a)_Attacker_IP_Identification.jpg
```

Identified IP:

```text id="header4"
192.168.56.10
```

Classification:

| IOC Type         | Value            |
| ---------------- | ---------------- |
| IP Address       | 192.168.56.10    |
| Confidence Level | High             |
| Role             | Attacker Machine |

<br><br>

# 👤 Sender Analysis

## From Header

```text id="header5"
attacker@lab.local
```

Analysis:

* Internal lab email address
* Used as phishing sender identity
* Delivered through SMTP
* Associated with attacker infrastructure

Classification:

| IOC Type         | Value                                           |
| ---------------- | ----------------------------------------------- |
| Email Address    | [attacker@lab.local](mailto:attacker@lab.local) |
| Confidence Level | High                                            |

<br><br>

# 🎯 Recipient Analysis

## To Header

```text id="header6"
victim@lab.local
```

Analysis:

* Intended target of phishing email
* Mailbox hosted on hMailServer
* Used for attack simulation

Classification:

| IOC Type         | Value                                       |
| ---------------- | ------------------------------------------- |
| Email Address    | [victim@lab.local](mailto:victim@lab.local) |
| Confidence Level | High                                        |

<br><br>

# 🔧 X-Mailer Analysis

The X-Mailer header often reveals the application used to send the message.

Observed Value:

```text id="header7"
swaks v20240103.0
```

Analysis:

* Indicates message generated using Swaks
* Common SMTP testing tool
* Frequently used during security testing and lab simulations

SOC Relevance:

* Tool fingerprinting
* Threat actor profiling
* Detection engineering opportunities

Classification:

| IOC Type         | Value             |
| ---------------- | ----------------- |
| Tool Signature   | swaks v20240103.0 |
| Confidence Level | High              |

<br><br>

# 🆔 Message-ID Analysis

The Message-ID uniquely identifies an email message.

Observed Example:

```text id="header8"
<20260607193015.12345@kali.lab.local>
```

Analysis:

* Generated by sending host
* Can assist in email correlation
* Useful during multi-email investigations

<br><br>

# ⏰ Timestamp Analysis

Observed Timestamp:

```text id="header9"
Sun, 07 Jun 2026 19:30:15 +0530
```

Analysis:

* Matches SMTP logs
* Matches Wireshark packet capture timeline
* Supports attack reconstruction

SOC Value:

* Timeline creation
* Event correlation
* Incident response documentation

<br><br>

# 📊 Extracted Indicators of Compromise (IOCs)

| IOC Type        | Value                                           | Confidence |
| --------------- | ----------------------------------------------- | ---------- |
| Source IP       | 192.168.56.10                                   | 🔴 High    |
| Destination IP  | 192.168.56.110                                  | 🔴 High    |
| Sender Email    | [attacker@lab.local](mailto:attacker@lab.local) | 🔴 High    |
| Recipient Email | [victim@lab.local](mailto:victim@lab.local)     | 🔴 High    |
| Hostname        | kali                                            | 🟠 Medium  |
| Tool Signature  | swaks v20240103.0                               | 🔴 High    |
| Subject         | Password Expiry Notification                    | 🟡 Medium  |
| URL             | http://192.168.56.10/reset                      | 🔴 High    |

<br><br>

# 🔄 Evidence Correlation

The extracted findings were validated using multiple evidence sources.

| Evidence Source  | Validation Purpose  |
| ---------------- | ------------------- |
| Email Headers    | Origin Verification |
| Wireshark PCAP   | Network Validation  |
| hMailServer Logs | SMTP Validation     |
| Sysmon Logs      | Endpoint Visibility |
| VirusTotal       | IOC Validation      |

This correlation increased confidence in the investigation findings.

<br><br>

# 🧠 SOC Analyst Assessment

Based on the header analysis:

✅ Email originated from Kali Linux

✅ Source IP identified as 192.168.56.10

✅ SMTP delivery confirmed

✅ Sender identity identified

✅ Recipient identified

✅ Swaks tool fingerprint discovered

✅ Malicious URL extracted

✅ Multiple high-confidence IOCs identified

<br><br>

# 📸 Evidence Collected

The following screenshots support this investigation.

```text id="header10"
15_Email_Raw_Header_Extraction.jpg
15(a)_Attacker_IP_Identification.jpg
22_Email_Header_Analysis_Evidence.jpg
23_Email_Investigation_Findings.jpg
24_Email_Investigation_Timeline.jpg
```

<br><br>

# 🎯 Outcome

The email header investigation successfully identified the originating attacker system, extracted multiple high-confidence Indicators of Compromise, and validated the attack path from sender to recipient.

The findings were later used for IOC enrichment, threat intelligence validation, detection engineering, MITRE ATT&CK mapping, and incident response reporting.

This analysis demonstrates a fundamental SOC Analyst skill used daily when investigating phishing emails and email-based threats.

