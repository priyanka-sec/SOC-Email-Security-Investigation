# Detection Logic

## 🎯 Objective

Define how suspicious emails are transformed into actionable security alerts and investigations.

<br><br>

# 📥 Detection Workflow

Email Received

↓

Header Extraction

↓

IOC Extraction

↓

Threat Intelligence Validation

↓

Detection Rule Matching

↓

Alert Generation

↓

SOC Investigation

↓

Containment & Response

<br><br>

# 🔍 Detection Stages

## Stage 1 — Email Ingestion

Purpose:

Receive email through SMTP infrastructure.

Analyst Focus:

* Sender information
* Subject line
* Attachments
* Embedded URLs

<br><br>

## Stage 2 — Email Header Analysis

Purpose:

Identify suspicious metadata.

Analyst Checks:

* Received headers
* Sender IPs
* Return-Path
* Message-ID anomalies
* X-Mailer values

<br><br>

## Stage 3 — IOC Extraction

Purpose:

Extract indicators from email artifacts.

Extract:

* IP Addresses
* URLs
* Email Addresses
* Hostnames
* Tool Signatures

<br><br>

## Stage 4 — Threat Intelligence Validation

Purpose:

Validate extracted indicators.

Validation Sources:

* VirusTotal
* Threat Intelligence Platforms
* Internal Detection Rules

<br><br>

## Stage 5 — Detection Rule Evaluation

Trigger Alerts If:

✓ Suspicious X-Mailer values detected

✓ Raw IP URLs detected

✓ Password reset themes detected

✓ Social engineering indicators detected

<br><br>

## Stage 6 — Alert Generation

Alert Severity Examples:

🔴 High

* Credential harvesting
* Suspicious SMTP tools
* Known malicious indicators

🟠 Medium

* Suspicious language patterns

🟡 Low

* Unverified anomalies

<br><br>

## Stage 7 — SOC Investigation

Analyst Actions:

* Validate alert
* Confirm attack technique
* Map MITRE ATT&CK
* Determine impact

<br><br>

## Stage 8 — Containment & Response

Response Actions:

* Block indicators
* Update detections
* Improve filtering
* Document findings

<br><br>

# 🛡 Detection Philosophy

Good SOC detection is not:

"Generate many alerts"

Good SOC detection is:

"Generate meaningful alerts with context"

