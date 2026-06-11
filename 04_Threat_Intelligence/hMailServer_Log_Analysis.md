# 📧 hMailServer Log Analysis

## 🎯 Objective

This document provides an analysis of hMailServer logs collected during the phishing email investigation lab.

The purpose of this analysis was to determine:

* Who sent the email
* When the email was delivered
* Which systems were involved
* Whether delivery was successful
* How the attack could be reconstructed using SMTP logs

The findings were correlated with:

* Email Header Analysis
* Wireshark PCAP Analysis
* Sysmon Log Analysis
* DNS Authentication Records

to perform a complete end-to-end phishing investigation.

<br><br>

# 📌 Why hMailServer Logs Matter

Mail server logs are one of the most important evidence sources during phishing investigations.

They help SOC analysts answer critical questions such as:

* Who sent the email?
* What IP address was used?
* Was the email successfully delivered?
* Which account received the email?
* Did the mail server reject or accept the message?

In enterprise environments, mail server logs are often one of the first places investigators look when responding to phishing incidents.

<br><br>

# 🏗️ Mail Server Environment

| Component            | Value                                           |
| -------------------- | ----------------------------------------------- |
| Mail Server          | hMailServer                                     |
| Operating System     | Windows Server 2022                             |
| Server IP            | 192.168.56.110                                  |
| Protocol             | SMTP                                            |
| Listening Port       | 25                                              |
| Investigation Domain | lab.local                                       |
| Recipient Account    | [victim@lab.local](mailto:victim@lab.local)     |
| Sender Account       | [attacker@lab.local](mailto:attacker@lab.local) |

<br><br>

# 📧 Attack Overview

The attacker used Kali Linux to send a phishing email directly to the hMailServer SMTP service.

The objective was to simulate a real-world phishing attack and investigate the resulting email artifacts.

<br><br>

# 🔍 Investigation Questions

The analysis focused on answering the following questions:

### Question 1

Was an email successfully delivered?

### Question 2

What IP address sent the email?

### Question 3

Which mailbox received the email?

### Question 4

When did the delivery occur?

### Question 5

Can the activity be correlated with other evidence sources?

<br><br>

# 📊 Log Source

## hMailServer SMTP Logs

The following log source was reviewed:

```text
hMailServer Logs
```

The logs contain detailed SMTP transaction information including:

* Connection activity
* Sender information
* Recipient information
* Delivery status
* SMTP commands
* Error messages

<br><br>

# 🔎 SMTP Connection Analysis

## Evidence Observed

The logs confirmed an SMTP connection from the attacker system.

### Source System

```text
Kali Linux
```

### Source IP

```text
192.168.56.10
```

### Destination System

```text
Windows Server 2022
```

### Destination IP

```text
192.168.56.110
```

### Protocol

```text
SMTP
```

### Port

```text
25/TCP
```

<br><br>

# 📨 Email Delivery Analysis

## Sender Address

```text
attacker@lab.local
```

## Recipient Address

```text
victim@lab.local
```

## Subject Theme

```text
Password Expiry Notification
```

## Delivery Result

```text
SUCCESSFUL
```

The mail server accepted the message and delivered it to the intended recipient mailbox.

<br><br>

# 📅 Timeline Evidence

The SMTP logs provided a reliable timeline of events.

### Event Sequence

1. SMTP connection established
2. Sender authenticated/identified
3. Recipient specified
4. Email content transmitted
5. Server accepted message
6. Delivery completed

This sequence matched the activity observed in Wireshark packet captures.

<br><br>

# 🔗 Evidence Correlation

The SMTP logs were compared with other investigation artifacts.

| Evidence Source       | Finding                          |
| --------------------- | -------------------------------- |
| hMailServer Logs      | Email delivery confirmed         |
| Email Header Analysis | Sender IP identified             |
| Wireshark PCAP        | SMTP traffic captured            |
| Sysmon Logs           | Network connection observed      |
| DNS Records           | Authentication records validated |

All evidence sources produced consistent results.

<br><br>

# 🌐 Attacker Attribution

The SMTP logs identified the originating system responsible for sending the phishing email.

## Identified Source

| Indicator   | Value               |
| ----------- | ------------------- |
| Host        | Kali Linux          |
| IP Address  | 192.168.56.10       |
| Protocol    | SMTP                |
| Destination | Windows Server 2022 |

The identified source matched:

* Email headers
* Wireshark captures
* Sysmon network events

This increased confidence in the investigation findings.

<br><br>

# 🚨 Security Findings

## Finding 1

### Email Successfully Delivered

The phishing email successfully reached the target mailbox.

### Risk

Users could interact with malicious content contained in the email.

<br><br>

## Finding 2

### Direct SMTP Communication Observed

The attacker established a direct SMTP session with the mail server.

### Risk

Unauthorized SMTP activity may indicate phishing or spam campaigns.

<br><br>

## Finding 3

### Internal Testing Infrastructure Successfully Simulated Attack

The lab successfully reproduced a realistic phishing scenario.

### Value

This provided an opportunity to practice:

* Email forensics
* Log analysis
* Threat hunting
* Incident response

<br><br>

# 🛠️ Detection Opportunities

## Detection Opportunity 1

### Direct SMTP Connections

Generate alerts when non-mail systems communicate directly with SMTP services.

<br><br>

## Detection Opportunity 2

### Suspicious Sender Domains

Monitor sender addresses that do not match trusted domains.

<br><br>

## Detection Opportunity 3

### High-Risk Email Subjects

Alert on social engineering themes such as:

* Password Expiration
* Account Verification
* Urgent Action Required
* Security Alerts

<br><br>

## Detection Opportunity 4

### Correlation Rules

Correlate:

* SMTP Logs
* Email Headers
* Sysmon Events
* Network Traffic

to improve phishing detection capabilities.

<br><br>

# 🧠 SOC Analyst Findings

The hMailServer logs provided definitive evidence that the phishing email was successfully delivered.

Key observations included:

✅ SMTP connection successfully established

✅ Email transmitted to target mailbox

✅ Sender and recipient identified

✅ Timeline reconstructed

✅ Activity correlated with Wireshark captures

✅ Activity correlated with Sysmon logs

✅ Activity correlated with email header evidence

The logs served as a critical evidence source for validating the phishing attack lifecycle.

<br><br>

# 📋 Conclusion

The hMailServer logs successfully documented the complete email delivery process and provided high-confidence evidence supporting the phishing investigation.

The logs enabled investigators to:

* Confirm email delivery
* Identify sender infrastructure
* Validate attack timing
* Correlate multiple evidence sources
* Reconstruct the phishing attack lifecycle

Combined with Wireshark, Sysmon, and email header analysis, the SMTP logs provided a comprehensive view of attacker activity.

<br><br>

# 🏁 Final Assessment

| Category                 | Result           |
| ------------------------ | ---------------- |
| Evidence Source          | hMailServer Logs |
| SMTP Connection Observed | ✅ Yes            |
| Email Delivery Confirmed | ✅ Yes            |
| Sender Identified        | ✅ Yes            |
| Recipient Identified     | ✅ Yes            |
| Timeline Reconstructed   | ✅ Yes            |
| Correlation Successful   | ✅ Yes            |
| Investigation Confidence | 🔴 High          |

**Analyst Verdict:** hMailServer logs successfully validated the phishing attack and provided critical SMTP evidence required for complete incident reconstruction.

