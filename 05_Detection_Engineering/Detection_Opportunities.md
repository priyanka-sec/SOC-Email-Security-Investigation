# 🎯 Detection Opportunities

## 📌 Objective

The purpose of this document is to identify potential detection opportunities discovered during the phishing email investigation.

A key responsibility of a SOC Analyst is not only to investigate security incidents but also to improve future detection capabilities.

Following the completion of the phishing investigation, several opportunities were identified to strengthen monitoring, alerting, and threat detection across the environment.

<br><br>

# 🧠 What Are Detection Opportunities?

Detection opportunities are security events, behaviors, or indicators that can be monitored to identify malicious activity before it causes significant impact.

During an investigation, analysts often ask:

> "How could we have detected this earlier?"

The answer becomes a detection opportunity.

These opportunities can later be converted into:

* Sigma Rules
* SIEM Correlation Rules
* Alerting Logic
* Threat Hunting Queries
* Detection Engineering Use Cases

<br><br>

# ⚔️ Attack Overview

The phishing simulation followed the attack path below:

```text
Attacker (Kali Linux)
        │
        ▼
Direct SMTP Connection
        │
        ▼
Phishing Email Delivery
        │
        ▼
Mail Server Processing
        │
        ▼
Email Received by Victim
        │
        ▼
SOC Investigation
```

During this workflow, multiple activities were identified that could generate security alerts.

<br><br>

# 🚨 Detection Opportunity #1

## Direct SMTP Connections

### Description

The attacker system established a direct SMTP connection to the mail server on TCP Port 25.

### Evidence

| Indicator      | Value          |
| -------------- | -------------- |
| Source IP      | 192.168.56.10  |
| Destination IP | 192.168.56.110 |
| Protocol       | TCP            |
| Port           | 25             |

### Why It Matters

Most user workstations do not normally send emails directly through SMTP.

Unexpected SMTP traffic may indicate:

* Phishing Campaigns
* Spam Activity
* Unauthorized Mail Servers
* Malware Sending Emails

### Detection Recommendation

Generate alerts when:

* Internal hosts communicate directly with SMTP servers.
* Non-mail systems initiate SMTP connections.
* Large volumes of SMTP traffic are observed.

### Severity

🔴 High

<br><br>

# 🚨 Detection Opportunity #2

## Suspicious Sender Addresses

### Description

The phishing email originated from:

```text
attacker@lab.local
```

### Why It Matters

Attackers frequently spoof sender identities to appear legitimate.

Common examples include:

* [support@company.com](mailto:support@company.com)
* [security@company.com](mailto:security@company.com)
* [hr@company.com](mailto:hr@company.com)
* [helpdesk@company.com](mailto:helpdesk@company.com)

### Detection Recommendation

Generate alerts when:

* New sender addresses appear.
* Sender addresses fail validation checks.
* Internal domains are spoofed.

### Severity

🟠 Medium

<br><br>

# 🚨 Detection Opportunity #3

## Suspicious Email Subjects

### Description

The phishing email used social engineering techniques to create urgency.

Example themes:

* Password Expiration
* Security Alert
* Account Suspension
* Urgent Action Required

### Why It Matters

These are commonly used phishing lures.

### Detection Recommendation

Generate alerts when email subjects contain:

```text
password
reset
verify
urgent
security alert
account suspended
```

### Severity

🟠 Medium

<br><br>

# 🚨 Detection Opportunity #4

## Malicious URLs Inside Emails

### Description

The phishing email contained a URL designed to attract user interaction.

Example:

```text
http://192.168.56.10/reset
```

### Why It Matters

Malicious URLs are one of the most common phishing indicators.

### Detection Recommendation

Inspect email bodies for:

* IP-based URLs
* Newly Registered Domains
* Known Malicious Domains
* URL Shorteners

### Severity

🔴 High

<br><br>

# 🚨 Detection Opportunity #5

## SPF Validation Failures

### Description

SPF verifies whether an email was sent from an authorized mail server.

### Why It Matters

Failed SPF validation can indicate:

* Sender Spoofing
* Phishing Attempts
* Unauthorized Infrastructure

### Detection Recommendation

Generate alerts when SPF validation fails.

### Severity

🔴 High

<br><br>

# 🚨 Detection Opportunity #6

## DKIM Validation Failures

### Description

DKIM validates the integrity of an email message.

### Why It Matters

Missing or invalid DKIM signatures may indicate:

* Email Tampering
* Spoofed Messages
* Unauthorized Email Sources

### Detection Recommendation

Generate alerts when:

* DKIM signatures are missing.
* DKIM validation fails.

### Severity

🟠 Medium

<br><br>

# 🚨 Detection Opportunity #7

## DMARC Policy Violations

### Description

DMARC combines SPF and DKIM results to determine email legitimacy.

### Why It Matters

DMARC failures often indicate phishing activity.

### Detection Recommendation

Generate alerts for:

* DMARC Failures
* DMARC Quarantine Actions
* DMARC Reject Events

### Severity

🔴 High

<br><br>

# 🚨 Detection Opportunity #8

## Suspicious X-Mailer Headers

### Description

Email header analysis identified the tool used to send the phishing email.

Example:

```text
swaks v20240103.0
```

### Why It Matters

Attack tools often leave fingerprints in email headers.

### Detection Recommendation

Alert when email headers contain:

* swaks
* smtp-cli
* custom mailers
* penetration testing tools

### Severity

🟠 Medium

<br><br>

# 🚨 Detection Opportunity #9

## SMTP Activity Correlation

### Description

Multiple evidence sources observed the same activity.

Evidence Sources:

* Wireshark
* hMailServer Logs
* Sysmon Logs
* Email Headers

### Why It Matters

Correlating multiple sources reduces false positives.

### Detection Recommendation

Create SIEM correlation rules that combine:

* SMTP Logs
* Email Headers
* Sysmon Network Events
* DNS Events

### Severity

🔴 High

<br><br>

# 🚨 Detection Opportunity #10

## Threat Intelligence IOC Matching

### Description

Indicators extracted during the investigation can be monitored continuously.

Examples:

```text
192.168.56.10
attacker@lab.local
http://192.168.56.10/reset
```

### Why It Matters

Known malicious indicators should always trigger alerts.

### Detection Recommendation

Continuously compare logs against:

* IOC Watchlists
* Threat Intelligence Feeds
* Internal Blacklists

### Severity

🔴 High

<br><br>

# 📊 Detection Priority Matrix

| Detection Opportunity   | Priority | Severity  |
| ----------------------- | -------- | --------- |
| Direct SMTP Connections | P1       | 🔴 High   |
| SPF Failures            | P1       | 🔴 High   |
| DMARC Failures          | P1       | 🔴 High   |
| Malicious URLs          | P1       | 🔴 High   |
| SMTP Correlation Rules  | P1       | 🔴 High   |
| Threat Intel Matching   | P1       | 🔴 High   |
| Suspicious Senders      | P2       | 🟠 Medium |
| DKIM Failures           | P2       | 🟠 Medium |
| Suspicious Subjects     | P2       | 🟠 Medium |
| X-Mailer Detection      | P2       | 🟠 Medium |

<br><br>

# 🧠 SOC Analyst Recommendations

Following the investigation, the following security improvements are recommended:

✅ Implement SPF validation monitoring

✅ Implement DKIM validation monitoring

✅ Enforce DMARC policy checks

✅ Monitor SMTP traffic patterns

✅ Create Sigma detection rules

✅ Deploy SIEM correlation logic

✅ Integrate threat intelligence feeds

✅ Monitor suspicious email subjects

✅ Inspect embedded URLs

✅ Continuously tune detection logic

<br><br>

# 📋 Conclusion

The phishing investigation identified multiple opportunities to improve detection coverage across the environment.

The most valuable detections include:

* SMTP Traffic Monitoring
* Email Authentication Failures
* Malicious URL Detection
* Threat Intelligence Matching
* Multi-Source Event Correlation

These detections would significantly improve the organization's ability to identify and respond to phishing attacks at earlier stages of the attack lifecycle.

<br><br>

# 🏁 Final Assessment

| Category                           | Result  |
| ---------------------------------- | ------- |
| Detection Opportunities Identified | 10      |
| High Priority Detections           | 6       |
| Medium Priority Detections         | 4       |
| Detection Engineering Value        | 🔴 High |
| SOC Improvement Potential          | 🔴 High |

**Analyst Verdict:** The phishing investigation revealed multiple high-value detection opportunities that can be converted into Sigma rules, SIEM alerts, and threat hunting content to strengthen overall security monitoring capabilities.

