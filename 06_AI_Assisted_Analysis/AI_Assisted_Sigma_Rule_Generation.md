# 🤖 AI-Assisted Sigma Rule Generation

## 📌 Overview

Detection engineering is one of the most important responsibilities within modern Security Operations Centers (SOCs).

SOC analysts and detection engineers continuously develop rules to identify malicious activity, suspicious behaviors, and indicators of compromise (IOCs) across enterprise environments.

In this project, Artificial Intelligence (AI) was used to assist with Sigma rule generation based on findings identified during the phishing email investigation.

The objective was not to allow AI to create detections independently, but rather to accelerate rule development while maintaining human validation and oversight.

<br><br>

# 🎯 Objective

The purpose of this exercise was to evaluate how AI can assist SOC analysts with:

* Detection logic creation
* Sigma rule drafting
* ATT&CK technique mapping
* Detection engineering workflows
* Investigation-to-detection conversion

<br><br>

# 🧠 What Is Sigma?

Sigma is an open and vendor-neutral detection rule format used to describe suspicious activities in a structured way.

Sigma rules can later be converted into:

* Splunk SPL
* Microsoft Sentinel KQL
* Elastic Queries
* QRadar AQL
* Chronicle Queries
* Other SIEM platforms

This allows security teams to write detections once and deploy them across multiple technologies.

<br><br>

# 🔍 Why Detection Engineering Matters

Every SOC investigation should answer an important question:

> "How can we detect this attack earlier next time?"

Detection engineering transforms investigation findings into security monitoring logic.

Without detections:

❌ Attacks may go unnoticed

❌ Threats may repeat

❌ Security visibility remains limited

❌ Investigation lessons are lost

Sigma rules help convert investigative knowledge into operational detections.

<br><br>

# 📊 Investigation Findings Used For Detection Development

The phishing investigation identified several valuable detection opportunities.

| Finding                         | Source                  |
| ------------------------------- | ----------------------- |
| Suspicious sender activity      | Email Headers           |
| Direct SMTP communication       | SMTP Logs               |
| SWAKS tool usage                | Email Headers           |
| Internal phishing URL           | Email Content           |
| SMTP traffic patterns           | Wireshark PCAP          |
| Email authentication weaknesses | SPF/DKIM/DMARC Analysis |

These findings were used as inputs for AI-assisted detection generation.

<br><br>

# 🤖 AI-Assisted Detection Workflow

The workflow used during this project is shown below.

```text
Investigation Findings
          │
          ▼
IOC Extraction
          │
          ▼
AI-Assisted Rule Drafting
          │
          ▼
Human Validation
          │
          ▼
Sigma Rule Development
          │
          ▼
SIEM Detection Use Cases
```

AI accelerated the drafting process while the analyst remained responsible for validation.

<br><br>

# 🛠️ Detection Use Case 1 – SWAKS Email Tool Detection

## Investigation Finding

Email header analysis identified:

```text
X-Mailer: swaks v20240103.0
```

<br><br>

## AI Assistance

AI was used to:

* Explain why the artifact is suspicious
* Identify detection opportunities
* Generate initial Sigma rule structure
* Suggest ATT&CK mappings

<br><br>

## Draft Detection Logic

```yaml
selection:
  X-Mailer|contains:
    - "swaks"
```

<br><br>

## Human Validation

The analyst verified:

* Header evidence
* Email artifacts
* SMTP logs

<br><br>

## ATT&CK Mapping

| Technique | Description        |
| --------- | ------------------ |
| T1566     | Phishing           |
| T1566.002 | Spearphishing Link |

<br><br>

# 🛠️ Detection Use Case 2 – Direct SMTP Connection Detection

## Investigation Finding

The attacker connected directly to:

```text
SMTP Port 25
```

using the SWAKS tool.

<br><br>

## AI Assistance

AI helped identify:

* Direct SMTP delivery patterns
* Detection opportunities
* Monitoring recommendations

<br><br>

## Draft Detection Logic

```yaml
selection:
  DestinationPort:
    - 25
```

<br><br>

## Human Validation

Validated through:

* Wireshark PCAP
* SMTP Logs
* Email Delivery Evidence

<br><br>

## ATT&CK Mapping

| Technique | Description        |
| --------- | ------------------ |
| T1566     | Phishing           |
| T1566.002 | Spearphishing Link |

<br><br>

# 🛠️ Detection Use Case 3 – Password Reset Phishing Themes

## Investigation Finding

The phishing email used urgent language related to password expiration.

Example:

```text
URGENT: Password Expiry Notification
```

<br><br>

## AI Assistance

AI suggested:

* Keyword-based detections
* Subject-line monitoring
* Social engineering indicators

<br><br>

## Draft Detection Logic

```yaml
selection:
  Subject|contains:
    - "password"
    - "expiry"
    - "urgent"
```

<br><br>

## Human Validation

Reviewed against:

* Phishing email sample
* Email headers
* Investigation findings

<br><br>

# 🛠️ Detection Use Case 4 – Suspicious Embedded URL Detection

## Investigation Finding

The phishing email contained:

```text
http://192.168.56.10/reset
```

<br><br>

## AI Assistance

AI helped identify:

* Credential harvesting indicators
* Suspicious URL patterns
* Detection recommendations

<br><br>

## Draft Detection Logic

```yaml
selection:
  URL|contains:
    - "/reset"
```

<br><br>

## Human Validation

Verified using:

* Email body
* IOC extraction
* Threat intelligence findings

<br><br>

# 📈 AI Benefits During Detection Development

Several benefits were observed during the exercise.

<br><br>

## Faster Rule Creation

AI significantly reduced time required to:

* Create rule templates
* Structure Sigma rules
* Generate detection ideas

<br><br>

## Improved Documentation

AI helped create:

* Detection descriptions
* Rule explanations
* ATT&CK mappings

<br><br>

## Enhanced Learning

AI assisted with:

* Detection engineering concepts
* Rule-writing best practices
* SOC workflow understanding

<br><br>

# ⚠️ Risks of AI-Generated Sigma Rules

AI-generated rules should never be deployed without validation.

Potential issues include:

<br><br>

## False Positives

AI may create overly broad rules.

Example:

```yaml
Subject|contains:
  - "password"
```

This may trigger on legitimate emails.

<br><br>

## Missing Context

AI does not understand:

* Organizational baselines
* Business processes
* Normal user behavior

<br><br>

## Invalid Logic

AI may produce:

* Incorrect fields
* Unsupported syntax
* Inefficient detection logic

<br><br>

# 🛡️ Human Validation Process

Every AI-generated rule was reviewed before acceptance.

The analyst validated:

✅ Detection logic

✅ Sigma syntax

✅ Investigation evidence

✅ ATT&CK mappings

✅ False positive considerations

✅ Operational relevance

<br><br>

# 📊 AI vs Human Responsibilities

| Activity                  | AI | Human Analyst |
| ------------------------- | -- | ------------- |
| Draft Sigma Rules         | ✅  |               |
| Suggest Detection Ideas   | ✅  |               |
| Create ATT&CK Suggestions | ✅  |               |
| Validate Logic            |    | ✅             |
| Review Syntax             |    | ✅             |
| Assess False Positives    |    | ✅             |
| Approve Deployment        |    | ✅             |
| Own Detection Strategy    |    | ✅             |

<br><br>

# 🎯 SOC Detection Engineering Best Practices

When using AI for detection development:

### Recommended

✅ Use AI for initial drafts

✅ Use AI for ATT&CK suggestions

✅ Use AI for documentation

✅ Validate every rule manually

✅ Test rules before deployment

<br><br>

### Avoid

❌ Direct production deployment

❌ Blind trust in AI outputs

❌ Skipping testing

❌ Ignoring false positives

❌ Replacing analyst review

<br><br>

# 📚 Lessons Learned

This exercise demonstrated that AI can significantly accelerate Sigma rule development.

Key observations:

* AI improves detection engineering productivity.
* AI helps convert investigations into detections.
* AI speeds up ATT&CK mapping.
* Human validation remains mandatory.
* Detection quality depends on analyst expertise.

The most effective approach combines AI-generated drafts with human review and testing.

<br><br>

# 🏁 Analyst Conclusion

During this phishing investigation, AI was used to assist with Sigma rule generation based on observed attacker behavior, email artifacts, SMTP activity, and IOC findings.

AI accelerated the creation of detection ideas and rule structures while reducing the time required to document detection opportunities.

However, all Sigma rules were reviewed, validated, and approved by the analyst before inclusion in the project.

This demonstrates a realistic modern SOC workflow where AI acts as a detection engineering assistant while human analysts remain responsible for rule quality, testing, validation, and operational deployment.

The future of detection engineering is not **AI replacing detection engineers**, but rather **AI helping analysts create better detections faster while maintaining human oversight and decision-making authority**.

