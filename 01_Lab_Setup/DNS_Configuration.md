# 🌐 DNS Configuration for Email Authentication

## 🎯 Objective

The purpose of this configuration was to build a DNS infrastructure capable of supporting modern email authentication mechanisms.

A Windows DNS Server was deployed and configured to host:

* SPF (Sender Policy Framework)
* DKIM (DomainKeys Identified Mail) – Simulated
* DMARC (Domain-based Message Authentication, Reporting and Conformance)

These controls help organizations protect against:

✅ Email Spoofing

✅ Phishing Attacks

✅ Domain Impersonation

✅ Unauthorized Email Sending

<br><br>

# 🏗️ Why DNS Matters in Email Security

Email authentication relies heavily on DNS records.

When an email arrives, the receiving mail server can query DNS to determine:

* Who is authorized to send email
* Whether the email was digitally signed
* What action should be taken if authentication fails

Without these controls, attackers can easily impersonate legitimate domains.

<br><br>

# 🖥️ Environment Details

| Component               | Value                        |
| ----------------------- | ---------------------------- |
| DNS Server              | Windows DNS Server           |
| Operating System        | Windows Server 2022          |
| DNS Server IP           | 192.168.56.110               |
| Zone Name               | lab.local                    |
| Record Type             | TXT                          |
| Authentication Controls | SPF, DKIM (Simulated), DMARC |

<br><br>

# 🌐 DNS Zone Configuration

A Forward Lookup Zone was created.

### Zone Name

```text
lab.local
```

### Zone Type

```text
Primary Zone
```

### Lookup Type

```text
Forward Lookup Zone
```

Purpose:

* Host email authentication records
* Support DNS lookups from client systems
* Enable SPF, DKIM, and DMARC validation

<br><br>

# 📧 SPF Configuration

## What is SPF?

SPF (Sender Policy Framework) specifies which servers are allowed to send email on behalf of a domain.

Receiving mail servers verify whether the sending server is authorized.

<br><br>

## SPF Record Configured

```text
v=spf1 ip4:192.168.56.110 -all
```

<br><br>

## SPF Record Breakdown

| Component          | Meaning                   |
| ------------------ | ------------------------- |
| v=spf1             | SPF Version 1             |
| ip4:192.168.56.110 | Authorized sending server |
| -all               | Reject all other senders  |

<br><br>

## Security Benefit

SPF helps detect:

* Sender spoofing
* Unauthorized email delivery
* Domain impersonation

<br><br>

## Validation Performed

The SPF record was queried from Kali Linux using DNS lookups.

Validation Result:

✅ SPF Record Successfully Resolved

Evidence:

```text
27_SPF_Validation.jpg
```

<br><br>

# 🔐 DKIM Configuration (Simulated)

## What is DKIM?

DKIM (DomainKeys Identified Mail) uses cryptographic signatures to verify that an email was not modified during transmission.

Normally:

* Private Key → Mail Server
* Public Key → DNS

For this lab, a simulated public key was published to demonstrate the validation workflow.

<br><br>

## DKIM Selector

```text
selector1
```

<br><br>

## DKIM Record Location

```text
selector1._domainkey.lab.local
```

---

## DKIM Record

```text
v=DKIM1; k=rsa; p=MIGfMA0GCSqGSlb3DQEBAQUAA4GNADCBiQKBgQDKIMSimulationPublicKeyExample123456789ABCDEF
```

<br><br>

## DKIM Record Breakdown

| Component | Meaning                  |
| --------- | ------------------------ |
| v=DKIM1   | DKIM Version             |
| k=rsa     | RSA Encryption Algorithm |
| p=        | Public Key               |

<br><br>

## Security Benefit

DKIM helps detect:

* Message tampering
* Email modification
* Forged messages

<br><br>

## Validation Performed

The DKIM TXT record was queried from Kali Linux.

Validation Result:

✅ DKIM Record Successfully Resolved

Evidence:

```text
27(b)_DKIM_Validation.jpg
```

<br><br>

# 🛡️ DMARC Configuration

## What is DMARC?

DMARC builds on SPF and DKIM.

It tells receiving mail servers what action to take when email authentication fails.

DMARC also enables reporting and visibility into spoofing attempts.

<br><br>

## DMARC Record Location

```text
_dmarc.lab.local
```

---

## DMARC Record Configured

```text
v=DMARC1; p=reject; rua=mailto:admin@lab.local
```

<br><br>

## DMARC Record Breakdown

| Component | Meaning                        |
| --------- | ------------------------------ |
| v=DMARC1  | DMARC Version                  |
| p=reject  | Reject authentication failures |
| rua=      | Send aggregate reports         |

<br><br>

## Security Benefit

DMARC helps protect against:

* Business Email Compromise (BEC)
* CEO Fraud
* Domain Spoofing
* Phishing Campaigns

<br><br>

## Validation Performed

The DMARC record was queried from Kali Linux.

Validation Result:

✅ DMARC Record Successfully Resolved

Evidence:

```text
27(a)_DMARC_Validation.jpg
```

<br><br>

# 🔍 DNS Validation Process

DNS records were validated using:

```bash
dig TXT lab.local @192.168.56.110
```

```bash
dig TXT _dmarc.lab.local @192.168.56.110
```

```bash
dig TXT selector1._domainkey.lab.local @192.168.56.110
```

Successful responses confirmed:

✅ DNS Server Reachability

✅ Zone Configuration

✅ SPF Record Availability

✅ DKIM Record Availability

✅ DMARC Record Availability

<br><br>

# 📸 Configuration Evidence

### DNS Zone Creation

```text
28_DNS_Email_Authentication_Records.jpg
```

### SPF Validation

```text
27_SPF_Validation.jpg
```

### DMARC Validation

```text
27(a)_DMARC_Validation.jpg
```

### DKIM Validation

```text
27(b)_DKIM_Validation.jpg
```

<br><br>

# 🧠 SOC Investigation Relevance

Understanding SPF, DKIM, and DMARC is critical for SOC analysts because these records are frequently reviewed during phishing investigations.

Analysts often verify:

* Whether a sender was authorized
* Whether authentication checks passed
* Whether spoofing indicators exist
* Whether email security controls were bypassed

These checks help determine whether an email is legitimate or malicious.

<br><br>

# ✅ Configuration Outcome

The Windows DNS Server was successfully configured to support email authentication.

The environment successfully demonstrated:

✅ SPF Validation

✅ DKIM Record Publishing (Simulation)

✅ DMARC Enforcement

✅ DNS-Based Email Authentication

✅ Phishing Defense Concepts

This DNS infrastructure provided the foundation for email authentication analysis and phishing investigation activities performed throughout this project.
