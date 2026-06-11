# 📅 Investigation Timeline

## 🎯 Objective

This document provides a chronological reconstruction of the phishing email attack performed during the SOC Email Security Investigation Lab.

The timeline was created using evidence collected from:

- 📧 Email Headers
- 📨 hMailServer Logs
- 🌐 Wireshark PCAP Analysis
- 🖥️ Sysmon Event Logs
- 🔍 IOC Investigation
- 🧠 Analyst Findings

The purpose of this timeline is to demonstrate how a SOC Analyst reconstructs attack activity from multiple data sources and builds an incident narrative.

<br><br>

# 📌 Executive Summary

A phishing email was successfully delivered from a Kali Linux attacker machine to a Windows Server 2022 mail server running hMailServer.

The attack was performed using the SWAKS SMTP testing tool and contained a malicious password reset lure designed to simulate credential harvesting activity.

The investigation identified:

- Source IP Address
- Destination Mail Server
- Email Authentication Status
- Attack Tool Used
- SMTP Communication Flow
- Indicators of Compromise (IOCs)
- MITRE ATT&CK Mapping

<br><br>

# 🕒 Chronological Timeline

| Time | Event | Evidence Source |
|--------|--------|--------|
| T+00 | Virtual lab environment prepared | VirtualBox |
| T+05 | Network connectivity verified between Kali and Windows Server | Ping Validation |
| T+10 | Sysmon installed and configured | Sysmon Logs |
| T+15 | hMailServer configured and operational | hMailServer Configuration |
| T+20 | SMTP port 25 confirmed listening | Netstat Verification |
| T+25 | DNS records configured for SPF, DKIM, and DMARC simulation | Windows DNS |
| T+30 | Attacker prepared phishing email | Kali Linux |
| T+31 | SWAKS command executed | Kali Terminal |
| T+32 | SMTP connection established to Windows Server | Wireshark |
| T+33 | Email transmitted successfully | Wireshark PCAP |
| T+34 | Email accepted by hMailServer | SMTP Logs |
| T+35 | Email stored in recipient mailbox | hMailServer Logs |
| T+40 | Raw email headers extracted | Email Client |
| T+45 | Received headers analysed | Email Forensics |
| T+50 | Attacker IP identified | Header Analysis |
| T+55 | X-Mailer field identified as SWAKS | Header Analysis |
| T+60 | IOC extraction completed | Investigation Notes |
| T+65 | VirusTotal validation performed | Threat Intelligence |
| T+70 | MITRE ATT&CK mapping completed | ATT&CK Navigator |
| T+75 | Detection opportunities identified | SOC Analysis |
| T+80 | Sigma rules drafted | Detection Engineering |
| T+85 | Investigation findings documented | Incident Report |
| T+90 | Remediation recommendations produced | Incident Response |
| T+95 | Investigation closed | SOC Analyst |

<br><br>

# 📧 Email Delivery Timeline

## Step 1 — Attacker Preparation

The attacker prepared a phishing email using the SWAKS SMTP testing tool from the Kali Linux system.

### Evidence

- Host: Kali Linux
- IP Address: 192.168.56.10
- Tool: SWAKS

<br><br>

## Step 2 — SMTP Connection

A direct SMTP connection was established from the attacker machine to the Windows Server mail server.

### Evidence

| Source | Destination | Protocol | Port |
|----------|----------|----------|----------|
| 192.168.56.10 | 192.168.56.110 | SMTP | 25 |

### Validation

- Wireshark Packet Capture
- SMTP Session Logs

<br><br>

## Step 3 — Email Transmission

The phishing email was transmitted through SMTP.

### Indicators Observed

- MAIL FROM command
- RCPT TO command
- DATA command
- SMTP Success Response

### Evidence Sources

- Wireshark
- hMailServer Logs

<br><br>

## Step 4 — Email Delivery

The email server successfully accepted and processed the message.

### Evidence

- SMTP 250 Success Response
- Mail Delivery Logs
- Mailbox Verification

<br><br>

## Step 5 — Email Header Analysis

The received email was examined for forensic indicators.

### Findings

| Field | Result |
|---------|---------|
| Source IP | 192.168.56.10 |
| Sender | attacker@lab.local |
| Recipient | victim@lab.local |
| X-Mailer | SWAKS |
| Authentication | Simulated Lab Environment |

<br><br>

## Step 6 — IOC Extraction

Indicators of Compromise were extracted from available evidence.

### IOCs Identified

- Attacker IP Address
- Mail Server IP Address
- Email Addresses
- Hostnames
- URL Indicators
- Tool Fingerprints

<br><br>

## Step 7 — Threat Intelligence Validation

Extracted indicators were validated through threat intelligence processes.

### Activities Performed

- IP Reputation Review
- URL Review
- MITRE Mapping
- IOC Classification

<br><br>

## Step 8 — Detection Engineering

Detection opportunities were identified for future monitoring.

### Created

- Sigma Rules
- Detection Logic
- SIEM Use Cases
- Alert Recommendations

<br><br>

## Step 9 — Incident Response

Investigation findings were documented and remediation actions proposed.

### Recommendations

- Enforce SPF
- Enforce DKIM
- Enforce DMARC
- Monitor SMTP Activity
- Create Email Security Alerts
- Monitor Suspicious Senders

<br><br>

# 🔍 Evidence Used During Investigation

| Evidence Type | Purpose |
|---------------|----------|
| Email Headers | Identify sender and route |
| SMTP Logs | Validate delivery |
| Wireshark PCAP | Network-level visibility |
| Sysmon Logs | Endpoint visibility |
| DNS Records | Email authentication validation |
| Threat Intelligence | IOC enrichment |
| MITRE ATT&CK | Adversary behavior mapping |

<br><br>

# 🧠 SOC Analyst Conclusion

The phishing email attack was successfully reconstructed from initial delivery through final investigation.

The timeline confirmed that:

✅ The attacker originated from 192.168.56.10

✅ The phishing email was delivered through SMTP

✅ hMailServer successfully processed the message

✅ SWAKS was identified as the email generation tool

✅ Multiple forensic artifacts were collected and validated

✅ Detection opportunities were identified and documented

✅ SPF, DKIM, and DMARC controls were implemented and validated

The investigation demonstrates a complete SOC workflow covering email forensics, network analysis, threat intelligence, detection engineering, and incident response.

<br><br>

## 🏁 Final Status

**Investigation Status:** Closed

**Severity:** Medium

**Attack Type:** Phishing

**MITRE ATT&CK Technique:** T1566.002 – Spearphishing Link

**Analyst Verdict:** Successfully Investigated and Documented
