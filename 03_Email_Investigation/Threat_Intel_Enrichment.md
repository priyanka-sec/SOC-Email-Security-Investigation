# 🌍 Threat Intelligence Enrichment

## 📌 Overview

Threat Intelligence Enrichment is the process of collecting additional context about Indicators of Compromise (IOCs) identified during a security investigation.

During this phishing investigation, multiple IOCs were extracted from email headers, SMTP logs, DNS records, and network traffic. These indicators were then validated and enriched using publicly available threat intelligence sources.

The goal was to determine:

* Whether the indicators were malicious
* Whether they were associated with known threats
* Their potential impact on the environment
* Appropriate response actions

<br><br>

# 🎯 Investigation Objective

The primary objectives of this threat intelligence analysis were:

✅ Validate extracted IOCs

✅ Determine reputation of IP addresses and URLs

✅ Identify potential phishing infrastructure

✅ Assess attacker behavior

✅ Support incident response decisions

<br><br>

# 🔍 Extracted Indicators of Compromise (IOCs)

The following indicators were identified during the phishing investigation.

| IOC Type              | Value                                           |
| --------------------- | ----------------------------------------------- |
| Attacker IP Address   | 192.168.56.10                                   |
| Victim Mail Server IP | 192.168.56.110                                  |
| Sender Email          | [attacker@lab.local](mailto:attacker@lab.local) |
| Recipient Email       | [victim@lab.local](mailto:victim@lab.local)     |
| Malicious URL         | http://192.168.56.10/reset                      |
| Hostname              | kali                                            |
| X-Mailer Signature    | swaks v20240103.0                               |

<br><br>

# 🛠️ Threat Intelligence Sources Used

The following intelligence sources were utilized for enrichment activities.

| Source                | Purpose                     |
| --------------------- | --------------------------- |
| VirusTotal            | Reputation analysis         |
| MITRE ATT&CK          | Adversary technique mapping |
| Email Header Analysis | IOC extraction              |
| DNS Records           | Domain validation           |
| SMTP Logs             | Attack verification         |
| Wireshark PCAP        | Network validation          |

<br><br>

# 🌐 IOC Enrichment Process

```text
IOC Extraction
       │
       ▼
IOC Validation
       │
       ▼
Threat Intelligence Lookup
       │
       ▼
Reputation Analysis
       │
       ▼
MITRE Mapping
       │
       ▼
Risk Assessment
       │
       ▼
Response Recommendation
```

<br><br>

# 🔴 Attacker IP Analysis

## Indicator

```text
192.168.56.10
```

<br><br>

## Source of Discovery

The IP address was identified from:

* Email headers
* SMTP logs
* Wireshark packet captures

<br><br>

## Validation Evidence

The IP address appeared within the SMTP communication chain and was confirmed as the originating host responsible for sending the phishing email.

<br><br>

## Threat Intelligence Result

| Attribute      | Value                     |
| -------------- | ------------------------- |
| Indicator Type | IP Address                |
| Role           | Attacker Host             |
| Source         | Kali Linux                |
| Reputation     | Lab Simulated Environment |
| Confidence     | High                      |

<br><br>

## Analyst Assessment

The IP address was directly observed sending the phishing email and is therefore considered a confirmed malicious source within the lab environment.

### Risk Rating

🔴 High

<br><br>

# 🔗 Malicious URL Analysis

## Indicator

```text
http://192.168.56.10/reset
```

<br><br>

## Source of Discovery

The URL was embedded within the phishing email body.

The message attempted to convince the recipient to reset their password using a fraudulent webpage.

<br><br>

## Threat Intelligence Result

| Attribute      | Value                 |
| -------------- | --------------------- |
| Indicator Type | URL                   |
| Purpose        | Credential Harvesting |
| Location       | Email Body            |
| Confidence     | High                  |

<br><br>

## Analyst Assessment

The URL was used as the phishing payload and represents the primary social engineering component of the attack.

If deployed in a real environment, this link could be used to:

* Steal credentials
* Redirect victims
* Deliver malware
* Collect sensitive information

### Risk Rating

🔴 High

<br><br>

# 📧 Email Address Analysis

## Sender Address

```text
attacker@lab.local
```

### Assessment

The sender address was intentionally crafted to simulate a phishing campaign.

No legitimate business purpose was identified.

### Risk Rating

🔴 High

<br><br>

## Recipient Address

```text
victim@lab.local
```

### Assessment

Targeted user account used to receive the phishing message.

### Risk Rating

🟢 Informational

<br><br>

# 🖥️ Hostname Analysis

## Indicator

```text
kali
```

<br><br>

## Source

Email headers and network communications.

<br><br>

## Assessment

The hostname identifies the originating attack system.

Hostnames can provide useful attribution clues during investigations.

### Risk Rating

🟠 Medium

<br><br>

# 🛠️ Attack Tool Identification

## Indicator

```text
swaks v20240103.0
```

<br><br>

## Source

X-Mailer Header

<br><br>

## Description

SWAKS (Swiss Army Knife SMTP) is a legitimate SMTP testing utility frequently used by:

* Security researchers
* Red team operators
* Penetration testers
* Email administrators

<br><br>

## SOC Relevance

The presence of SWAKS within email headers can indicate:

* Security testing
* Phishing simulation
* Adversary testing
* Unauthorized email delivery attempts

### Risk Rating

🔴 High

<br><br>

# 🧠 MITRE ATT&CK Mapping

The observed attack behavior aligns with the following ATT&CK techniques.

| Tactic          | Technique                | ID        |
| --------------- | ------------------------ | --------- |
| Initial Access  | Spearphishing Link       | T1566.002 |
| Reconnaissance  | Phishing for Information | T1598     |
| Defense Evasion | Masquerading             | T1036     |

<br><br>

# 📊 IOC Confidence Assessment

| IOC             | Confidence       |
| --------------- | ---------------- |
| Attacker IP     | 🔴 High          |
| Malicious URL   | 🔴 High          |
| Sender Email    | 🔴 High          |
| Recipient Email | 🟢 Informational |
| Hostname        | 🟠 Medium        |
| SWAKS Signature | 🔴 High          |

<br><br>

# 🚨 Risk Assessment Summary

| Category                | Risk Level |
| ----------------------- | ---------- |
| Phishing Infrastructure | 🔴 High    |
| Credential Theft Risk   | 🔴 High    |
| Email Spoofing Risk     | 🟠 Medium  |
| Domain Abuse Risk       | 🟠 Medium  |
| Network Impact          | 🟡 Low     |
| Malware Delivery Risk   | 🟠 Medium  |

<br><br>

# 🛡️ Recommended Detection Opportunities

SOC teams should monitor for:

* Direct SMTP connections
* Unusual sender domains
* Suspicious URLs inside email bodies
* X-Mailer values associated with testing tools
* Authentication failures (SPF/DKIM/DMARC)
* Phishing-themed subject lines

<br><br>

# 🎯 SOC Analyst Findings

The threat intelligence enrichment process successfully validated the indicators extracted from the phishing investigation.

Key findings include:

✅ Attacker infrastructure identified

✅ Phishing payload confirmed

✅ Malicious sender validated

✅ Attack tooling identified

✅ MITRE ATT&CK techniques mapped

✅ IOC confidence levels assigned

<br><br>

# 📚 Lessons Learned

* Raw IOCs provide limited value without context.
* Threat intelligence enrichment improves detection accuracy.
* Multiple evidence sources increase analyst confidence.
* MITRE ATT&CK mapping provides operational context.
* IOC validation supports faster incident response decisions.

<br><br>

# 🏁 Conclusion

Threat intelligence enrichment transformed basic investigation artifacts into actionable security intelligence.

The enrichment process confirmed the phishing attack source, validated the malicious payload, identified the attack tooling, and provided additional context required for detection engineering and incident response activities.

This exercise demonstrates a critical SOC analyst capability: converting raw indicators into meaningful intelligence that supports security operations and threat detection.
