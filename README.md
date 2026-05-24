<div align="center">

# 🛡️ SOC Email Security Investigation
### Phishing Attack Simulation · Email Forensics · MITRE ATT&CK T1566 · Incident Response

[![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=flat-square&logo=virtualbox)](https://www.virtualbox.org/)
[![Attacker OS](https://img.shields.io/badge/Attacker-Kali%20Linux-red?style=flat-square&logo=kalilinux)](https://www.kali.org/)
[![Victim OS](https://img.shields.io/badge/Victim-Windows%20Server%202022-0078D4?style=flat-square&logo=windows)](https://www.microsoft.com/)
[![Mail Server](https://img.shields.io/badge/Mail%20Server-hMailServer-grey?style=flat-square)](https://www.hmailserver.com/)
[![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-T1566%20Phishing-orange?style=flat-square)](https://attack.mitre.org/techniques/T1566/)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)]()

</div>

<br><br>

## 📌 Project Overview

This project simulates a realistic SOC phishing investigation workflow commonly performed in enterprise Security Operations Centres.

The project demonstrates the complete investigation lifecycle of a phishing email incident, including attack simulation, email header forensics, IOC extraction, threat intelligence validation, MITRE ATT&CK mapping, and incident reporting:

- Building an isolated lab environment with a live mail server
- Executing a phishing attack using professional attack tooling (`swaks`)
- Performing raw email header forensics to identify the attacker's true IP
- Extracting and validating all Indicators of Compromise (IOCs)
- Mapping the attack to MITRE ATT&CK framework (T1566.002)
- Producing a formal SOC Incident Report

> **Target Role Alignment:** SOC Analyst L1/L2 · Threat Detection · Email Security · Incident Response

<br><br>

## 📁 Repository Structure

```
SOC-Email-Security-Investigation/
│
├── 01_Lab_Setup/
│   ├── Lab_Setup_Guide.md               # VM config, network, hMailServer setup
│   ├── Network_Topology_Diagram.png     # Visual lab architecture
│   └── hMailServer_Config.md            # Mail server configuration steps
│
├── 02_Attack_Simulation/
│   ├── Attack_Scenario.md               # swaks command, spoofing technique
│   └── phishing_email_sample.eml        # Sanitized raw phishing email file
│
├── 03_Email_Forensics/
│   ├── Email_Header_Analysis.md         # Full annotated header breakdown
│   ├── Header_Screenshot.png            # Screenshot of raw .eml in Notepad
│   └── SPF_DKIM_DMARC_Analysis.md       # Email auth failure analysis
│
├── 04_IOC_Extraction/
│   ├── IOC_Table.md                     # IOC table with confidence & disposition
│   └── VirusTotal_Results/              # Screenshots of VT lookups
│
├── 05_Threat_Intelligence/
│   ├── Threat_Intel_Summary.md          # TI platform findings
│   └── IOC_Validation_Process.md        # Step-by-step IOC validation
│
├── 06_MITRE_ATT&CK/
│   ├── MITRE_Mapping.md                 # Full T1566 mapping with detection logic
│   └── ATT&CK_Navigator_Export.json     # Navigator layer export
│
├── 07_Incident_Report/
│   ├── SOC_Incident_Report.md           # Markdown IR report
│   └── SOC_Incident_Report.pdf          # PDF version for download
│
├── 08_Lessons_Learned/
│   └── Lessons_Learned.md               # Analyst reflection & SIEM rule ideas
│
└── Screenshots/
    └── INDEX.md                         # Captioned index of all screenshots
```

<br><br>

## 🎯 Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Build an isolated virtual lab with a live SMTP mail server | ✅ Complete |
| 2 | Simulate a phishing email attack using `swaks` from Kali Linux | ✅ Complete |
| 3 | Forensically analyse raw email headers to extract attacker IP | ✅ Complete |
| 4 | Extract all IOCs from email header and body | ✅ Complete |
| 5 | Validate IOCs using VirusTotal threat intelligence | ✅ Complete |
| 6 | Analyse SPF/DKIM/DMARC failures as attack enablers | ✅ Complete |
| 7 | Map the attack to MITRE ATT&CK T1566.002 — Spearphishing Link | ✅ Complete |
| 8 | Produce a professional enterprise-grade SOC Incident Report | ✅ Complete |

<br><br>

## 🧰 Tools & Technologies

| Category | Tool | Purpose |
|----------|------|---------|
| Virtualisation | Oracle VM VirtualBox | Isolated lab environment |
| Attacker Machine | Kali Linux | Attack simulation platform |
| Victim Machine | Windows Server 2022 | Target mail server host |
| Mail Server | hMailServer | SMTP/POP3/IMAP mail server |
| Attack Tool | swaks v20240103.0 | Phishing email delivery via SMTP |
| Firewall | Windows Defender Firewall | Port 25 inbound rule configuration |
| Forensics | Text-Based Email Header Analysis | Email header extraction |
| Threat Intel | VirusTotal | IOC reputation validation |
| Framework | MITRE ATT&CK Navigator | Technique mapping & visualisation |

<br><br>

## 🗺️ Lab Network Topology

```
┌──────────────────────────┐              ┌──────────────────────────────┐
│       Kali Linux         │              │    Windows Server 2022       │
│    Attacker Machine      │              │    Victim Mail Server        │
│                          │              │                              │
│  NAT IP : 10.0.3.15      │──SMTP:25────▶│  NAT IP  : 10.0.3.14        │
│  H-Only : 192.168.56.10  │              │  H-Only  : 192.168.56.110    │
│                          │              │  hMailServer (running)       │
└──────────────────────────┘              └──────────────────────────────┘
     Adapter 1: NAT                              Adapter 1: NAT
     Adapter 2: Host-Only                        Adapter 2: Host-Only
```

<br><br>

## ⚔️ Attack Scenario

**Technique:** MITRE ATT&CK T1566.002 — Spearphishing Link  
**Tool Used:** `swaks` (Swiss Army Knife for SMTP)

The attacker on Kali Linux crafted and delivered a spoofed phishing email to a victim mailbox on Windows Server 2022, simulating a **credential harvesting phishing campaign**:

- **Spoofed sender:** `attacker@lab.local` (fake trusted identity)
- **Subject line:** `Urgent: Reset Your Password Immediately` (social engineering via urgency)
- **Payload:** Embedded fake password reset URL — `http://192.168.56.10/reset`
- **Delivery:** Direct SMTP connection to port 25 on the victim mail server

<br><br>

## 🔍 Investigation Workflow

```
Step 1 — Lab Setup           →  Configure VMs, network, hMailServer, firewall rule
Step 2 — Attack Simulation   →  Send phishing email via swaks from Kali Linux
Step 3 — Email Discovery     →  Locate .eml file in hMailServer mailbox directory
Step 4 — Header Forensics    →  Extract true attacker IP from Received field
Step 5 — IOC Extraction      →  Identify all indicators from header + body
Step 6 — Auth Analysis       →  Confirm SPF/DKIM/DMARC absence as attack enabler
Step 7 — Threat Intel        →  Validate IOCs on VirusTotal
Step 8 — MITRE Mapping       →  Map to T1566.002 — Spearphishing Link
Step 9 — Incident Report     →  Document full investigation professionally
```

<br><br>

## 📊 IOC Summary

| IOC Type | Value | Source | Confidence | Disposition |
|----------|-------|--------|------------|-------------|
| IP Address | `192.168.56.10` | Email `Received` header | High | Attacker Machine |
| Email Address | `attacker@lab.local` | `Return-Path` / `From` header | High | Spoofed Sender |
| Email Address | `victim@lab.local` | `To` header | High | Victim / Target |
| URL | `http://192.168.56.10/reset` | Email body | High | Fake Credential Page |
| Tool Signature | `swaks v20240103.0` | `X-Mailer` header | High | Attack Tool Fingerprint |

<br><br>

## 🧠 MITRE ATT&CK Mapping

| Field | Detail |
|-------|--------|
| **Tactic** | Initial Access (TA0001) |
| **Technique** | T1566 — Phishing |
| **Sub-technique** | T1566.002 — Spearphishing Link |
| **Data Sources** | Network Traffic, Application Log, Email Gateway |
| **Detection** | Email header anomalies, X-Mailer fingerprint, mismatched `Received` IP |
| **Mitigation** | M1054 — SPF/DKIM/DMARC enforcement |
| **Mitigation** | M1017 — User Training |
| **Mitigation** | M1021 — Restrict Web-Based Content |

<br><br>

## 🛡️ Detection Opportunities

The following detection opportunities were identified during the phishing investigation:

- Detect inbound emails containing internal IP-based URLs
- Alert on suspicious `X-Mailer` values such as `swaks`
- Monitor SPF/DKIM/DMARC authentication failures
- Detect spoofed internal sender domains
- Correlate repeated SMTP connections to mail server on port 25

<br><br>

## 📈 SIEM Detection Use Cases

| Use Case | Logic |
|----------|-------|
| Suspicious X-Mailer Detection | Detect emails containing `swaks` in headers |
| Internal Domain Spoofing | Alert when sender domain matches internal domain but fails SPF |
| Suspicious URL Detection | Detect private/internal IP URLs inside email body |
| SMTP Brute Activity | Monitor abnormal SMTP connections to port 25 |

<br><br>

## 🔐 Security Recommendations

- Enforce SPF, DKIM, and DMARC policies
- Block emails containing internal IP-based URLs
- Restrict SMTP relay permissions
- Implement secure email gateway filtering
- Conduct phishing awareness training
- Monitor anomalous SMTP traffic

<br><br>

## 📄 Key Documents

| Document | Description |
|----------|-------------|
| [`Email_Header_Analysis.md`](./03_Email_Forensics/Email_Header_Analysis.md) | Full annotated forensic breakdown of the phishing email header |
| [`IOC_Table.md`](./04_IOC_Extraction/IOC_Table.md) | All IOCs with confidence levels and disposition |
| [`MITRE_Mapping.md`](./06_MITRE_ATT%26CK/MITRE_Mapping.md) | T1566.002 mapping with detection logic and data sources |
| [`SOC_Incident_Report.md`](./07_Incident_Report/SOC_Incident_Report.md) | Enterprise-grade incident report (exec summary → remediation) |
| [`Lessons_Learned.md`](./08_Lessons_Learned/Lessons_Learned.md) | Analyst reflection, SIEM rule concepts, future improvements |

<br><br>

## 🧠 Skills Demonstrated

`SOC Analysis` `Email Forensics` `Phishing Investigation` `SMTP Protocol` `IOC Extraction`  
`Threat Intelligence` `VirusTotal` `MITRE ATT&CK` `Incident Response` `IR Report Writing`  
`SPF / DKIM / DMARC` `Firewall Configuration` `VirtualBox Lab Build` `hMailServer`  
`swaks` `Windows Server 2022` `Kali Linux` `Blue Team Operations`

<br><br>

## 👩‍💻 About the Analyst

**Priyanka Rane**  
SOC Analyst L1 | Threat Detection & Incident Response  

📧 ranepriyanka567@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/priyanka-rane-606a71257/)  
🐙 [GitHub](https://github.com/priyanka-sec)

<br><br>

<div align="center">

*This project demonstrates a realistic SOC investigation workflow for analysing and responding to a phishing email incident in an enterprise environment.*

</div>
