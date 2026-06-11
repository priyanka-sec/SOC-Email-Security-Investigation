# 🛡️ SOC Incident Report

## Incident Information

| Field            | Value                                |
| ---------------- | ------------------------------------ |
| Incident ID      | IR-2026-EMAIL-001                    |
| Incident Type    | Phishing Email Investigation         |
| Severity         | Medium                               |
| Status           | Closed                               |
| Date Identified  | June 2026                            |
| Analyst          | Priyanka Rane                        |
| Environment      | SOC Email Security Investigation Lab |
| ATT&CK Technique | T1566.002 – Spearphishing Link       |

<br><br>

# 📌 Executive Summary

A phishing email investigation was conducted within a controlled laboratory environment to simulate a real-world Security Operations Center (SOC) workflow.

The attack originated from a Kali Linux attacker machine and targeted a mailbox hosted on a Windows Server 2022 system running hMailServer.

The phishing email was successfully delivered through SMTP and contained a malicious password-reset themed lure designed to encourage user interaction.

The investigation involved:

* Email header analysis
* SMTP log analysis
* Sysmon event analysis
* Wireshark packet analysis
* IOC extraction
* Threat intelligence validation
* MITRE ATT&CK mapping
* Detection engineering
* Incident response documentation

The attacker infrastructure, delivery method, and attack artifacts were successfully identified and documented.

No actual credential theft occurred because the attack was executed within a controlled laboratory environment.

<br><br>

# 🎯 Incident Objectives

The objectives of this investigation were:

* Simulate a phishing attack
* Investigate malicious email artifacts
* Extract Indicators of Compromise (IOCs)
* Validate findings using threat intelligence
* Map activity to MITRE ATT&CK
* Develop detection opportunities
* Produce enterprise-style incident documentation

<br><br>

# 🏗️ Environment Overview

## Attacker System

| Attribute        | Value                   |
| ---------------- | ----------------------- |
| Operating System | Kali Linux              |
| IP Address       | 192.168.56.10           |
| Tool Used        | swaks                   |
| Purpose          | Email Attack Simulation |

<br><br>

## Victim System

| Attribute        | Value                           |
| ---------------- | ------------------------------- |
| Operating System | Windows Server 2022             |
| IP Address       | 192.168.56.110                  |
| Services         | hMailServer, DNS Server, Sysmon |
| Purpose          | Mail Infrastructure             |

<br><br>

# ⚔️ Attack Summary

## Attack Type

Phishing Email

<br><br>

## Delivery Method

SMTP (Port 25)

<br><br>

## Attack Tool

swaks v20240103.0

<br><br>

## Social Engineering Theme

Password Expiry Notification

The phishing email attempted to create urgency by requesting that the recipient reset their password immediately.

<br><br>

## Attack Flow

```text
Kali Linux (192.168.56.10)
          │
          ▼
SMTP Connection (Port 25)
          │
          ▼
hMailServer (192.168.56.110)
          │
          ▼
Victim Mailbox
          │
          ▼
Email Investigation
```

<br><br>

# 🔍 Investigation Findings

## Finding 1 – Phishing Email Successfully Delivered

Evidence confirmed that the phishing email was successfully transmitted from the attacker system to the target mail server.

### Evidence Sources

* hMailServer Logs
* SMTP Traffic
* Email Message Artifact

<br><br>

## Finding 2 – Attacker IP Address Identified

Email header analysis revealed the originating attacker system.

### Identified IP

```text
192.168.56.10
```

### Source

Received Header Analysis

### Confidence

High

<br><br>

## Finding 3 – Attack Tool Identified

The email headers contained metadata identifying the delivery tool.

### Tool

```text
swaks v20240103.0
```

### Source

X-Mailer Header

### Confidence

High

<br><br>

## Finding 4 – SMTP Communication Verified

Wireshark packet analysis confirmed SMTP communication between attacker and mail server.

### Evidence

* SMTP Session
* TCP Port 25 Traffic
* Email Transfer Activity

### Confidence

High

<br><br>

## Finding 5 – Email Authentication Records Configured

DNS records were created and validated for:

* SPF
* DKIM (Simulation)
* DMARC

### Verification Method

DNS Queries

### Result

Successfully Configured

<br><br>

# 📊 Indicators of Compromise (IOCs)

| IOC Type       | Value                                           | Confidence |
| -------------- | ----------------------------------------------- | ---------- |
| IP Address     | 192.168.56.10                                   | High       |
| IP Address     | 192.168.56.110                                  | High       |
| Email Address  | [attacker@lab.local](mailto:attacker@lab.local) | High       |
| Email Address  | [victim@lab.local](mailto:victim@lab.local)     | High       |
| URL            | http://192.168.56.10/reset                      | High       |
| Hostname       | kali                                            | Medium     |
| Tool Signature | swaks v20240103.0                               | High       |
| Subject Theme  | Password Expiry Notification                    | Medium     |

<br><br>

# 🌐 Threat Intelligence Analysis

Threat intelligence validation was performed against identified artifacts.

## Validation Sources

* VirusTotal
* MITRE ATT&CK
* Internal Investigation Findings

## Results

All identified artifacts were validated and documented.

Because the attack occurred within a controlled lab environment, no external malicious infrastructure was observed.

<br><br>

# 🧠 MITRE ATT&CK Mapping

| Tactic          | Technique | Description           |
| --------------- | --------- | --------------------- |
| Initial Access  | T1566.002 | Spearphishing Link    |
| Reconnaissance  | T1598.003 | Spearphishing Link    |
| Defense Evasion | T1036.005 | Match Legitimate Name |

<br><br>

# 📈 Detection Opportunities

The investigation identified multiple detection opportunities.

## Email-Based Detections

* Suspicious sender domains
* Internal phishing indicators
* Malicious URLs
* Password-reset themed lures

<br><br>

## Network-Based Detections

* Direct SMTP connections
* Unusual SMTP sources
* SMTP traffic from non-mail systems

<br><br>

## Endpoint-Based Detections

* Suspicious email clients
* Network connections to mail infrastructure
* Event correlation using Sysmon

<br><br>

# 🔐 Security Control Assessment

| Control        | Status      |
| -------------- | ----------- |
| SPF            | Implemented |
| DKIM           | Simulated   |
| DMARC          | Implemented |
| Sysmon Logging | Implemented |
| DNS Monitoring | Implemented |
| Email Logging  | Implemented |

<br><br>

# 🚨 Root Cause Analysis

The phishing email was successfully delivered because the environment was intentionally configured to simulate a realistic attack scenario.

The purpose was to observe and investigate the full attack lifecycle before implementing additional defensive controls.

No system compromise occurred.

No credentials were exposed.

No malware execution occurred.

<br><br>

# 🛠️ Remediation Actions

The following security improvements were implemented:

### Email Security

✅ SPF Configuration

✅ DKIM Simulation

✅ DMARC Enforcement

<br><br>

### Monitoring Improvements

✅ Sysmon Logging

✅ SMTP Log Monitoring

✅ Email Header Analysis Procedures

<br><br>

### Detection Improvements

✅ Sigma Rule Development

✅ IOC Monitoring

✅ MITRE ATT&CK Mapping

<br><br>

# 📚 Lessons Learned

## Technical Lessons

* Email headers provide critical forensic evidence.
* SMTP logs are valuable during phishing investigations.
* DNS authentication records improve email security.
* Wireshark can validate email delivery activity.
* Sysmon provides useful network telemetry.

<br><br>

## SOC Lessons

* Phishing investigations require multiple evidence sources.
* IOC validation improves confidence in findings.
* MITRE ATT&CK improves attack classification.
* Detection engineering should follow every investigation.
* Documentation is a critical SOC skill.

<br><br>

# 🤖 AI-Assisted Investigation Activities

AI tools were used to support:

* IOC enrichment
* Documentation drafting
* Detection engineering
* MITRE ATT&CK mapping
* Investigation workflow development

All AI-generated content was manually reviewed and validated before inclusion in the final report.

<br><br>

# 🏁 Final Assessment

The phishing email investigation was successfully completed.

The attacker source, delivery mechanism, email artifacts, authentication controls, and detection opportunities were identified and documented.

This project demonstrates the complete lifecycle of a SOC phishing investigation, including attack simulation, forensic analysis, threat intelligence validation, detection engineering, incident response, and AI-assisted security operations.

## Final Status

✅ Investigation Completed

✅ Evidence Collected

✅ IOCs Extracted

✅ Threat Intelligence Validated

✅ MITRE ATT&CK Mapped

✅ Detection Opportunities Identified

✅ Remediation Recommendations Documented

✅ Incident Closed

