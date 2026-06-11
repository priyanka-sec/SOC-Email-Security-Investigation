# 🧠 MITRE ATT&CK Mapping

## 📌 Overview

This document maps the phishing attack simulation conducted in this lab to the MITRE ATT&CK framework.

MITRE ATT&CK provides a globally recognized knowledge base of adversary tactics, techniques, and procedures (TTPs). Mapping observed attacker behavior to ATT&CK techniques helps SOC analysts understand:

* How the attack was executed
* Which tactics were used
* Where detections can be implemented
* What mitigations should be applied
* How the attack aligns with real-world threat activity

<br><br>

# 🎯 ATT&CK Mapping Summary

| Tactic               | Technique ID | Technique Name               | Observed              |
| -------------------- | ------------ | ---------------------------- | --------------------- |
| Initial Access       | T1566        | Phishing                     | ✅ Yes                 |
| Initial Access       | T1566.002    | Spearphishing Link           | ✅ Yes                 |
| Resource Development | T1583        | Acquire Infrastructure       | ⚠️ Simulated          |
| Defense Evasion      | T1036        | Masquerading                 | ✅ Yes                 |
| Credential Access    | T1056        | Input Capture                | ⚠️ Intended Objective |
| Discovery            | T1082        | System Information Discovery | ❌ Not Performed       |

<br><br>

# 🔍 Technique 1 – T1566 Phishing

## MITRE Details

| Field          | Value          |
| -------------- | -------------- |
| Technique ID   | T1566          |
| Technique Name | Phishing       |
| Tactic         | Initial Access |

## Description

Phishing is a social engineering technique used to trick users into performing actions such as:

* Opening malicious links
* Downloading malware
* Revealing credentials
* Executing malicious files

It is one of the most common attack vectors observed by SOC teams worldwide.

<br><br>

## Evidence From This Lab

The attacker crafted and delivered a phishing email using the SWAKS SMTP testing tool.

The email contained:

* Social engineering language
* Urgent action request
* Password expiration theme
* Embedded malicious URL

### Evidence

* Screenshot: `13_KaliLinux_Phishing_Email_Sent.jpg`
* Screenshot: `14_hMailServer_Email_Received_Logs.jpg`
* Email Artifact: `phishing_email_sample.eml`

<br><br>

## Detection Opportunities

Monitor for:

* Suspicious sender domains
* Newly observed senders
* External email links
* High urgency subject lines

<br><br>

# 🔍 Technique 2 – T1566.002 Spearphishing Link

## MITRE Details

| Field          | Value              |
| -------------- | ------------------ |
| Technique ID   | T1566.002          |
| Technique Name | Spearphishing Link |
| Tactic         | Initial Access     |

## Description

Adversaries send emails containing malicious links designed to redirect victims to credential harvesting pages or malicious websites.

<br><br>

## Evidence From This Lab

The phishing email included:

```text
http://192.168.56.10/reset
```

The link was designed to simulate a credential harvesting portal.

<br><br>

## Evidence

* Email Body Analysis
* IOC Extraction Results
* URL Validation Findings

### Screenshot References

* `16(a)_VirusTotal_Malicious_URL_Validation.jpg`
* `23_Email_Investigation_Findings.jpg`

<br><br>

## Detection Opportunities

Alert on:

* Internal IP addresses embedded in emails
* Newly observed URLs
* Suspicious login-themed URLs
* Password reset themed phishing emails

<br><br>

# 🔍 Technique 3 – T1036 Masquerading

## MITRE Details

| Field          | Value           |
| -------------- | --------------- |
| Technique ID   | T1036           |
| Technique Name | Masquerading    |
| Tactic         | Defense Evasion |

## Description

Masquerading occurs when attackers make malicious content appear legitimate.

Common examples include:

* Fake login portals
* Spoofed sender addresses
* Fake update notifications
* Password reset messages

<br><br>

## Evidence From This Lab

The phishing email pretended to be a legitimate password expiration notification.

The attacker attempted to create trust by using:

* Professional wording
* Corporate-style formatting
* Urgent language
* Credential reset instructions

<br><br>

## Evidence

Subject Example:

```text
URGENT: Password Expiry Notification
```

Observed within:

* Email Header Analysis
* Phishing Email Artifact

<br><br>

## Detection Opportunities

Monitor for:

* Password expiry subjects
* Account verification requests
* Urgent action language
* Spoofed internal domains

<br><br>

# 🔍 Technique 4 – T1056 Input Capture (Credential Harvesting Objective)

## MITRE Details

| Field          | Value             |
| -------------- | ----------------- |
| Technique ID   | T1056             |
| Technique Name | Input Capture     |
| Tactic         | Credential Access |

<br><br>

## Description

Credential harvesting attacks often attempt to capture usernames and passwords through fake login pages.

<br><br>

## Lab Context

No credential collection occurred during this lab.

However, the phishing email was designed to redirect users to a fake password reset page.

Therefore, credential harvesting was the intended attacker objective.

<br><br>

## Status

| Category            | Value |
| ------------------- | ----- |
| Fully Observed      | ❌ No  |
| Simulated Objective | ✅ Yes |

<br><br>

# 📊 Detection Mapping Matrix

| ATT&CK Technique | Data Source            | Detection Method                     |
| ---------------- | ---------------------- | ------------------------------------ |
| T1566            | Email Gateway Logs     | Suspicious sender detection          |
| T1566.002        | Email Content Analysis | URL extraction and reputation checks |
| T1036            | Email Header Analysis  | Spoofing and impersonation detection |
| T1056            | Web Proxy Logs         | Credential harvesting monitoring     |

<br><br>

# 🛡️ Recommended Mitigations

## Email Security Controls

* SPF Enforcement
* DKIM Validation
* DMARC Enforcement

<br><br>

## User Awareness

* Phishing awareness training
* Password reset verification procedures
* Suspicious email reporting process

<br><br>

## SOC Monitoring

* Email security alerts
* IOC monitoring
* URL reputation monitoring
* Threat intelligence enrichment

<br><br>

# 📈 ATT&CK Coverage Summary

| Technique | Name                            | Status       |
| --------- | ------------------------------- | ------------ |
| T1566     | Phishing                        | ✅ Observed   |
| T1566.002 | Spearphishing Link              | ✅ Observed   |
| T1036     | Masquerading                    | ✅ Observed   |
| T1056     | Credential Harvesting Objective | ⚠️ Simulated |

<br><br>

# 🎯 Analyst Conclusion

The phishing simulation successfully demonstrated how attackers leverage social engineering and malicious links to gain initial access into an environment.

Through email header analysis, IOC extraction, threat intelligence validation, DNS authentication analysis, and log investigation, the attack was mapped to relevant MITRE ATT&CK techniques.

The primary observed technique was **T1566.002 (Spearphishing Link)**, supported by **Masquerading (T1036)** and a simulated **Credential Harvesting objective (T1056)**.

This mapping enables SOC analysts to build detections, improve monitoring coverage, and strengthen defenses against phishing-based attacks.

