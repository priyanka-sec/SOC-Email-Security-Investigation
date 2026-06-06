# SIEM Use Cases

## Use Case 1 — Suspicious SMTP Tool Detection

Objective:

Detect emails sent using suspicious SMTP tools.

Detection Logic:

IF X-Mailer contains:

swaks
curl
python-requests

THEN generate alert.

Severity:

High

<br><br>

## Use Case 2 — Password Reset Phishing Detection

Objective:

Detect suspicious password-reset themed emails.

Detection Logic:

IF subject contains:

Urgent
Password
Reset
Verify

THEN generate alert.

Severity:

Medium

<br><br>

## Use Case 3 — Raw IP Address Detection

Objective:

Detect URLs using raw IP addresses.

Detection Logic:

IF email body contains:

http://IP_ADDRESS

THEN generate alert.

Severity:

High
