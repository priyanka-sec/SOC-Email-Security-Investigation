<div align="center">

# 🛡️ SOC Email Security Investigation Lab

### A Complete End-to-End Phishing Attack Simulation & SOC Investigation Portfolio

[![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=flat-square&logo=virtualbox)](https://www.virtualbox.org/)
[![Attacker](https://img.shields.io/badge/Attacker-Kali%20Linux-red?style=flat-square&logo=kalilinux)](https://www.kali.org/)
[![Victim](https://img.shields.io/badge/Victim-Windows%20Server%202022-0078D4?style=flat-square&logo=windows)](https://www.microsoft.com/)
[![Mail Server](https://img.shields.io/badge/Mail%20Server-hMailServer-grey?style=flat-square)](https://www.hmailserver.com/)
[![DNS](https://img.shields.io/badge/DNS-Windows%20DNS%20Server-0078D4?style=flat-square&logo=windows)](https://docs.microsoft.com/)
[![Sysmon](https://img.shields.io/badge/Logging-Sysmon-purple?style=flat-square)](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
[![Wireshark](https://img.shields.io/badge/PCAP-Wireshark-1679A7?style=flat-square&logo=wireshark)](https://www.wireshark.org/)
[![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-T1566.002-orange?style=flat-square)](https://attack.mitre.org/techniques/T1566/002/)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)]()

</div>

<br><br>

## 📌 What Is This Project?

This project is a **complete SOC (Security Operations Centre) investigation lab** built from scratch inside a virtual environment.

It simulates a real-world phishing attack — from the moment the attacker sends the email, all the way through to the final incident report and remediation plan. Every step follows the exact workflow a **SOC Analyst** would perform in an enterprise environment.

> 💡 **Why this matters for SOC roles:** Phishing is the #1 initial access technique used in cyber attacks worldwide (MITRE ATT&CK T1566). Every SOC Analyst — at every company — investigates phishing emails. This project proves you can do exactly that.

<br><br>

## 🎯 What This Lab Demonstrates

| Skill Area | What Was Done |
|------------|---------------|
| **Lab Engineering** | Built isolated virtual lab with Windows Server 2022, Kali Linux, DNS Server, hMailServer, Sysmon |
| **Attack Simulation** | Executed phishing attack using `swaks` with social engineering techniques |
| **Network Forensics** | Captured and analysed SMTP traffic using Wireshark PCAP |
| **Email Forensics** | Full raw header analysis — extracted attacker IP, tool fingerprint, timestamp analysis |
| **Email Authentication** | Configured and validated SPF, DKIM simulation, and DMARC records in DNS |
| **Log Analysis** | Investigated hMailServer SMTP logs and Sysmon Windows event logs |
| **IOC Extraction** | Extracted and classified all Indicators of Compromise with confidence levels |
| **Threat Intelligence** | Enriched IOCs using VirusTotal, MITRE ATT&CK, and TI validation workflow |
| **Detection Engineering** | Wrote Sigma detection rules and SIEM use cases (SPL/KQL) |
| **MITRE ATT&CK Mapping** | Mapped full attack to T1566.002 with data sources, detection logic, and mitigations |
| **AI-Assisted Analysis** | Used AI tools (Claude, ChatGPT) to accelerate IOC enrichment, report drafting, and Sigma rule generation — with human validation |
| **Incident Response** | Produced enterprise-grade SOC Incident Report, Remediation Plan, and Lessons Learned |

<br><br>

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        VirtualBox Host Machine                      │
│                                                                     │
│   ┌──────────────────────┐          ┌───────────────────────────┐   │
│   │    Kali Linux        │          │   Windows Server 2022     │   │
│   │    ATTACKER          │          │   VICTIM / MAIL SERVER    │   │
│   │                      │          │                           │   │
│   │  IP: 192.168.56.10   │─SMTP:25─▶│  IP: 192.168.56.110      │   │
│   │                      │          │                           │   │
│   │  Tools:              │          │  Services Running:        │   │
│   │  • swaks             │          │  • hMailServer (SMTP)     │   │
│   │  • Wireshark         │          │  • DNS Server             │   │
│   │                      │          │  • Sysmon                 │   │
│   └──────────────────────┘          │  • Windows Event Logging  │   │
│                                     └───────────────────────────┘   │
│                                                                     │
│              Host-Only Network: 192.168.56.0/24                     │
└─────────────────────────────────────────────────────────────────────┘
```

<br><br>

## 📁 Repository Structure

```
SOC-Email-Security-Investigation/
│
├── README.md                                    ← You are here
│
├── 01_Lab_Infrastructure/
│   ├── Lab_Setup_Guide.md                       ← Full VM + network setup
│   ├── hMailServer_Config.md                    ← Mail server configuration
│   ├── DNS_Configuration.md                     ← DNS zone + SPF/DKIM/DMARC
│   ├── Sysmon_Configuration.md                  ← Sysmon rules + event logging
│   └── Network_Topology_Diagram.png             ← Visual lab architecture
│
├── 02_Attack_Simulation/
│   ├── Attack_Scenario.md                       ← Full attack narrative + swaks command
│   ├── phishing_email_sample.eml                ← Raw phishing email artifact
│   └── Wireshark_Analysis.md                    ← PCAP + SMTP traffic analysis
│
├── 03_Email_Investigation/
│   ├── Email_Header_Analysis.md                 ← Deep forensic header breakdown
│   ├── Email_Authentication_Analysis.md         ← SPF / DKIM / DMARC findings
│   ├── IOC_Extraction.md                        ← All IOCs with confidence levels
│   └── Threat_Intel_Enrichment.md               ← TI validation per IOC
│
├── 04_Log_Analysis/
│   ├── hMailServer_Log_Analysis.md              ← SMTP log investigation
│   ├── Sysmon_Log_Analysis.md                   ← Windows event log analysis
│   └── Investigation_Timeline.md               ← Chronological attack reconstruction
│
├── 05_Detection_Engineering/
│   ├── Detection_Opportunities.md               ← Where detections could fire
│   ├── Sigma_Rules.md                           ← Production-ready Sigma rules
│   ├── SIEM_Use_Cases.md                        ← SPL and KQL queries
│   └── MITRE_ATT&CK_Mapping.md                  ← Full framework mapping
│
├── 06_AI_Assisted_Analysis/
│   ├── AI_in_SOC_Overview.md                    ← AI's role in modern SOC
│   ├── AI_Assisted_IOC_Enrichment.md            ← AI-accelerated IOC analysis
│   ├── AI_Assisted_Report_Writing.md            ← AI-drafted IR report workflow
│   ├── AI_Assisted_Sigma_Rule_Generation.md     ← AI + human Sigma validation
│   └── Human_vs_AI_Judgment.md                  ← Where human judgment is essential
│
├── 07_Incident_Response/
│   ├── SOC_Incident_Report.md                   ← Enterprise-grade IR report
│   ├── Remediation_Plan.md                      ← Technical remediation steps
│   └── Lessons_Learned.md                       ← Analyst reflection
│
└── Screenshots/
    └── INDEX.md                                 ← Captioned screenshot index
```

<br><br>

## ⚔️ Attack Scenario Summary

| Detail | Value |
|--------|-------|
| **Attack Type** | Phishing — Credential Harvesting |
| **MITRE Technique** | T1566.002 — Spearphishing Link |
| **Attacker Machine** | Kali Linux — `192.168.56.10` |
| **Victim Mail Server** | Windows Server 2022 — `192.168.56.110` |
| **Attack Tool** | `swaks` v20240103.0 |
| **Email Lure** | Fake password expiry notification — social engineering via urgency |
| **Payload** | Malicious URL embedded in email body |
| **Delivery Method** | Direct SMTP connection to port 25 |
| **Email Authentication** | SPF ✅ Configured | DKIM ✅ Simulated | DMARC ✅ Configured (p=reject) |

<br><br>

## 🔍 Investigation Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                    SOC INVESTIGATION FLOW                       │
└─────────────────────────────────────────────────────────────────┘

  PHASE 1 — DETECTION          PHASE 2 — INVESTIGATION
  ┌─────────────────┐          ┌──────────────────────────────┐
  │ Phishing email  │          │ Email header forensics       │
  │ arrives in      │─────────▶│ SPF/DKIM/DMARC analysis      │
  │ victim mailbox  │          │ IOC extraction               │
  └─────────────────┘          │ Threat intel enrichment      │
                               └──────────────┬───────────────┘
                                              │
  PHASE 4 — RESPONSE           PHASE 3 — ANALYSIS
  ┌─────────────────┐          ┌──────────────────────────────┐
  │ Incident report │          │ hMailServer log analysis     │
  │ Remediation     │◀─────────│ Sysmon event log analysis    │
  │ Lessons learned │          │ Wireshark PCAP analysis      │
  └─────────────────┘          │ Attack timeline              │
                               │ Detection engineering        │
                               │ MITRE ATT&CK mapping         │
                               └──────────────────────────────┘
```

<br><br>

## 🔐 Email Authentication Configuration

One of the key goals of this lab was to configure real email authentication controls and understand how their absence enables phishing attacks.

| Protocol | Record Configured | Value |
|----------|------------------|-------|
| **SPF** | ✅ Yes — DNS TXT record | `v=spf1 ip4:192.168.56.110 -all` |
| **DKIM** | ✅ Simulated — DNS TXT record | `selector1._domainkey.lab.local` |
| **DMARC** | ✅ Yes — DNS TXT record | `v=DMARC1; p=reject; rua=mailto:admin@lab.local` |

> 📖 Full configuration details: [`01_Lab_Infrastructure/DNS_Configuration.md`](./01_Lab_Infrastructure/DNS_Configuration.md)

<br><br>

## 📊 IOC Summary

| # | Type | Value | Confidence | Disposition |
|---|------|-------|------------|-------------|
| 1 | IP Address | `192.168.56.10` | 🔴 High | Attacker Machine |
| 2 | IP Address | `192.168.56.110` | 🔴 High | Victim Mail Server |
| 3 | Email Address | `attacker@lab.local` | 🔴 High | Spoofed Sender |
| 4 | Email Address | `victim@lab.local` | 🔴 High | Targeted Victim |
| 5 | URL | `http://192.168.56.10/reset` | 🔴 High | Credential Harvesting Page |
| 6 | Hostname | `kali` | 🟠 Medium | Attacker Hostname |
| 7 | Tool Signature | `swaks v20240103.0` | 🔴 High | Attack Tool Fingerprint |
| 8 | Subject Pattern | Fake password expiry lure | 🟡 Medium | Social Engineering Indicator |

> 📖 Full IOC analysis: [`03_Email_Investigation/IOC_Extraction.md`](./03_Email_Investigation/IOC_Extraction.md)

<br><br>

## 🧠 MITRE ATT&CK Coverage

| Tactic | Technique | Sub-Technique | Observed |
|--------|-----------|---------------|----------|
| Initial Access | T1566 — Phishing | T1566.002 — Spearphishing Link | ✅ |
| Reconnaissance | T1598 — Phishing for Info | T1598.003 — Spearphishing Link | ✅ |
| Defense Evasion | T1036 — Masquerading | T1036.005 — Match Legitimate Name | ✅ |

> 📖 Full mapping with detection logic: [`05_Detection_Engineering/MITRE_ATT&CK_Mapping.md`](./05_Detection_Engineering/MITRE_ATT&CK_Mapping.md)

<br><br>

## 🤖 AI-Assisted Analysis

This project also documents how **AI tools were used to accelerate SOC investigation tasks** — reflecting the reality of modern SOC operations in 2025/2026.

| AI Task | Tool Used | Human Validation Applied |
|---------|-----------|--------------------------|
| IOC extraction from raw header | Claude | ✅ Verified every IOC against raw .eml |
| Initial Sigma rule drafting | Claude / ChatGPT | ✅ Tested logic against actual log data |
| IR report structure and drafting | Claude | ✅ Rewrote sections AI got wrong |
| MITRE technique suggestions | Claude | ✅ Cross-checked against ATT&CK Navigator |

> 📖 Full AI workflow with prompts and outputs: [`06_AI_Assisted_Analysis/`](./06_AI_Assisted_Analysis/)

<br><br>

## 🛠️ Tools & Technologies

| Category | Tool | Purpose |
|----------|------|---------|
| Virtualisation | Oracle VM VirtualBox | Isolated lab environment |
| Attacker OS | Kali Linux | Attack simulation platform |
| Victim OS | Windows Server 2022 | Mail server + DNS + logging host |
| Mail Server | hMailServer | SMTP/POP3 mail server |
| DNS Server | Windows DNS Server | Hosts SPF, DKIM, DMARC records |
| Endpoint Logging | Sysmon (Sysinternals) | Process, network, DNS event logging |
| Network Capture | Wireshark | PCAP — SMTP traffic analysis |
| Attack Tool | swaks v20240103.0 | Phishing email delivery |
| Detection | Sigma | Vendor-agnostic detection rules |
| Framework | MITRE ATT&CK Navigator | Technique mapping and visualisation |
| AI Tools | Claude, ChatGPT | Investigation acceleration + validation |

<br><br>

## 🚦 Investigation Outcome

| Finding | Detail |
|---------|--------|
| **Attack succeeded?** | ✅ Email delivered — no controls blocked delivery initially |
| **Root cause** | SPF/DKIM/DMARC were configured *after* the attack to demonstrate before vs after |
| **Attacker identified?** | ✅ `192.168.56.10` confirmed via `Received` header |
| **Tool identified?** | ✅ `swaks v20240103.0` via `X-Mailer` header |
| **Detection rule created?** | ✅ Sigma rule for X-Mailer + direct SMTP |
| **Remediation documented?** | ✅ SPF/DKIM/DMARC enforcement + SIEM alerting |

<br><br>

## 📄 Key Documents

| Document | Description |
|----------|-------------|
| [`SOC_Incident_Report.md`](./07_Incident_Response/SOC_Incident_Report.md) | Enterprise-grade incident report — executive summary to remediation |
| [`Email_Header_Analysis.md`](./03_Email_Investigation/Email_Header_Analysis.md) | Full annotated forensic header breakdown |
| [`Sigma_Rules.md`](./05_Detection_Engineering/Sigma_Rules.md) | Production-ready Sigma detection rules |
| [`Investigation_Timeline.md`](./04_Log_Analysis/Investigation_Timeline.md) | Chronological reconstruction of the entire attack |
| [`Human_vs_AI_Judgment.md`](./06_AI_Assisted_Analysis/Human_vs_AI_Judgment.md) | Where AI helped and where human judgment was essential |

<br><br>

## 🧩 Skills Demonstrated

`SOC Analysis` `Email Forensics` `Phishing Investigation` `SMTP Protocol` `Wireshark` `PCAP Analysis`
`Sysmon` `Windows Event Logs` `DNS Configuration` `SPF / DKIM / DMARC` `IOC Extraction`
`Threat Intelligence` `VirusTotal` `MITRE ATT&CK` `Sigma Rules` `SIEM Query Writing`
`Incident Response` `IR Report Writing` `Remediation Planning` `AI-Assisted SOC Analysis`
`hMailServer` `swaks` `Kali Linux` `Windows Server 2022` `VirtualBox` `Blue Team Operations`

<br><br>

## 👩‍💻 About the Analyst

**Priyanka Rane**
SOC Analyst (Entry Level) | Blue Team | Threat Detection & Incident Response

🎓 BSc Information Technology
🏅 Certified Ethical Hacker v13 AI (CEHv13 AI)
🏅 eLearnSecurity Network Penetration Tester (eNPT)
📍 Mumbai, India

📧 ranepriyanka567@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/priyanka-rane-606a71257/)
🐙 [GitHub](https://github.com/priyanka-sec)

<br><br>

## ⚡ How to Use This Repository

**If you are a recruiter or hiring manager:**
Start with [`07_Incident_Response/SOC_Incident_Report.md`](./07_Incident_Response/SOC_Incident_Report.md) — it summarises the entire investigation in enterprise report format.

**If you are a SOC professional reviewing the technical work:**
Start with [`03_Email_Investigation/Email_Header_Analysis.md`](./03_Email_Investigation/Email_Header_Analysis.md) then follow through `04_Log_Analysis/` and `05_Detection_Engineering/`.

**If you are a fellow learner wanting to reproduce this lab:**
Start with [`01_Lab_Infrastructure/Lab_Setup_Guide.md`](./01_Lab_Infrastructure/Lab_Setup_Guide.md) — every step is documented for reproducibility.

**If you are interested in AI in SOC:**
Start with [`06_AI_Assisted_Analysis/AI_in_SOC_Overview.md`](./06_AI_Assisted_Analysis/AI_in_SOC_Overview.md).

<br><br>

<div align="center">

*This project was built as a practical demonstration of SOC analyst skills —*
*from lab construction through attack simulation to enterprise incident reporting.*

*Every artifact in this repository was generated from a real lab environment,*
*not simulated or copied from tutorials.*

</div>
