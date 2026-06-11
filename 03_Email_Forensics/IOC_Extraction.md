# 🔎 IOC Extraction Analysis

## 📌 Overview

Indicators of Compromise (IOCs) are observable artifacts that provide evidence of malicious activity within an environment.

During this phishing email investigation, multiple IOCs were identified from:

* Email headers
* SMTP logs
* DNS records
* Wireshark packet captures
* Phishing email content

The extracted indicators were documented, classified, validated, and prioritized to support threat intelligence enrichment, detection engineering, and incident response activities.

<br><br>

# 🎯 Investigation Objective

The purpose of IOC extraction was to:

✅ Identify malicious artifacts

✅ Determine attack origin

✅ Identify attacker infrastructure

✅ Support threat intelligence activities

✅ Enable detection engineering

✅ Improve future phishing detection capabilities

<br><br>

# 🧩 What Are Indicators of Compromise (IOCs)?

Indicators of Compromise are pieces of forensic evidence that may indicate malicious activity.

Common IOC categories include:

| IOC Type      | Example                                             |
| ------------- | --------------------------------------------------- |
| IP Address    | 192.168.56.10                                       |
| URL           | http://example.com                                  |
| Domain        | malicious-domain.com                                |
| Email Address | [attacker@example.com](mailto:attacker@example.com) |
| File Hash     | SHA256                                              |
| Hostname      | kali                                                |
| User-Agent    | Custom Tool Signature                               |
| Email Subject | Phishing Lure                                       |

<br><br>

# 📧 Sources of IOC Collection

During the investigation, indicators were extracted from multiple sources.

| Source          | Purpose                     |
| --------------- | --------------------------- |
| Email Headers   | Sender tracing              |
| Email Body      | URL identification          |
| SMTP Logs       | Delivery validation         |
| Wireshark PCAP  | Network evidence            |
| DNS Records     | Authentication verification |
| X-Mailer Header | Tool fingerprinting         |

<br><br>

# 🔍 IOC Extraction Methodology

```text id="v8ghfd"
Email Collection
       │
       ▼
Header Analysis
       │
       ▼
Artifact Identification
       │
       ▼
IOC Extraction
       │
       ▼
IOC Validation
       │
       ▼
Classification
       │
       ▼
Threat Intelligence Enrichment
```

<br><br>

# 🚨 Extracted Indicators of Compromise

## IOC #1 – Attacker IP Address

### Indicator

```text id="dkndk0"
192.168.56.10
```

### Source

* Email Header
* SMTP Logs
* Wireshark Capture

### Description

Originating system used to send the phishing email.

### Confidence Level

🔴 High

### Analyst Assessment

Confirmed attacker infrastructure.

<br><br>

# 🚨 IOC #2 – Victim Mail Server

### Indicator

```text id="jl3m8d"
192.168.56.110
```

### Source

* SMTP Communication
* DNS Configuration

### Description

Target mail server receiving the phishing email.

### Confidence Level

🔴 High

### Analyst Assessment

Targeted infrastructure.

<br><br>

# 🚨 IOC #3 – Sender Email Address

### Indicator

```text id="0vmu0d"
attacker@lab.local
```

### Source

Email Header

### Description

Email address used to deliver the phishing message.

### Confidence Level

🔴 High

### Analyst Assessment

Spoofed sender account.

<br><br>

# 🚨 IOC #4 – Recipient Email Address

### Indicator

```text id="c2xz2d"
victim@lab.local
```

### Source

Email Header

### Description

Target user account.

### Confidence Level

🟢 Informational

### Analyst Assessment

Victim account identified.

<br><br>

# 🚨 IOC #5 – Malicious URL

### Indicator

```text id="w5itlb"
http://192.168.56.10/reset
```

### Source

Email Body

### Description

Credential harvesting link embedded within the phishing email.

### Confidence Level

🔴 High

### Analyst Assessment

Primary phishing payload.

<br><br>

# 🚨 IOC #6 – Hostname

### Indicator

```text id="9nifv9"
kali
```

### Source

Network Evidence

### Description

Hostname associated with the attacker machine.

### Confidence Level

🟠 Medium

### Analyst Assessment

Useful attribution artifact.

<br><br>

# 🚨 IOC #7 – Attack Tool Signature

### Indicator

```text id="3q4tvf"
swaks v20240103.0
```

### Source

X-Mailer Header

### Description

Email testing and SMTP delivery tool used by the attacker.

### Confidence Level

🔴 High

### Analyst Assessment

Strong evidence of attack tooling.

<br><br>

# 🚨 IOC #8 – Email Subject Line

### Indicator

```text id="1g92gp"
URGENT: Password Expiry Notification
```

### Source

Email Subject Header

### Description

Social engineering lure designed to create urgency.

### Confidence Level

🟠 Medium

### Analyst Assessment

Potential phishing detection indicator.

<br><br>

# 📊 IOC Classification Table

| IOC                                             | Type            | Confidence       | Category                |
| ----------------------------------------------- | --------------- | ---------------- | ----------------------- |
| 192.168.56.10                                   | IP Address      | 🔴 High          | Attacker Infrastructure |
| 192.168.56.110                                  | IP Address      | 🔴 High          | Target Infrastructure   |
| [attacker@lab.local](mailto:attacker@lab.local) | Email Address   | 🔴 High          | Malicious Sender        |
| [victim@lab.local](mailto:victim@lab.local)     | Email Address   | 🟢 Informational | Victim Account          |
| http://192.168.56.10/reset                      | URL             | 🔴 High          | Phishing Payload        |
| kali                                            | Hostname        | 🟠 Medium        | Host Artifact           |
| swaks v20240103.0                               | Tool Signature  | 🔴 High          | Attack Tool             |
| Password Expiry Notification                    | Subject Pattern | 🟠 Medium        | Social Engineering      |

<br><br>

# 📈 IOC Confidence Matrix

## 🔴 High Confidence

Evidence directly observed during investigation.

* Attacker IP
* Victim Server IP
* Sender Address
* Malicious URL
* SWAKS Signature

<br><br>

## 🟠 Medium Confidence

Indicators requiring additional context.

* Hostname
* Subject Line

<br><br>

## 🟢 Informational

Contextual information.

* Recipient Account

<br><br>

# 🛠️ Detection Opportunities

The extracted IOCs can be used within:

### SIEM Platforms

* Splunk
* Microsoft Sentinel
* QRadar
* Elastic

### Detection Content

* Correlation Rules
* Sigma Rules
* Alerting Logic
* Threat Hunting Queries

### Monitoring Opportunities

* Direct SMTP Connections
* Suspicious URLs
* Email Subject Patterns
* Unauthorized Senders
* Email Authentication Failures

<br><br>

# 🔐 IOC Preservation

All indicators were preserved within:

* Investigation Notes
* Email Evidence
* Wireshark PCAP
* SMTP Logs
* IOC Repository
* Incident Report

This ensures repeatable analysis and future threat hunting activities.

<br><br>

# 📚 Lessons Learned

* Email headers contain valuable IOC information.
* URLs often represent the primary phishing payload.
* X-Mailer fields can expose attacker tooling.
* Multiple evidence sources increase confidence levels.
* Proper IOC classification improves investigation efficiency.

<br><br>

# 🎯 SOC Analyst Findings

The IOC extraction process successfully identified:

✅ Attacker infrastructure

✅ Victim infrastructure

✅ Malicious sender identity

✅ Credential harvesting URL

✅ Attack tooling

✅ Social engineering indicators

These findings provided the foundation for threat intelligence enrichment, MITRE ATT&CK mapping, detection engineering, and incident response activities.

<br><br>

# 🏁 Conclusion

The IOC extraction phase successfully identified and documented the critical indicators associated with the phishing attack.

The extracted indicators provided actionable intelligence that enabled deeper analysis, detection development, and response planning.

IOC extraction remains one of the most important skills for SOC analysts because it transforms raw evidence into actionable security intelligence.
