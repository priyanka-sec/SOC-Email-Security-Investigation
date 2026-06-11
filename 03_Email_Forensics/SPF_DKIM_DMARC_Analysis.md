# 🔐 SPF, DKIM & DMARC Analysis

## 📌 Overview

Email authentication technologies help organizations protect users from phishing, spoofing, and email impersonation attacks.

During this lab, SPF, DKIM, and DMARC records were configured and validated using a Windows DNS Server to simulate how modern organizations protect their email infrastructure.

The objective was to understand:

* How email authentication works
* How attackers abuse the absence of authentication controls
* How SOC analysts validate authentication results during investigations
* How SPF, DKIM, and DMARC contribute to phishing detection

<br><br>

# 🎯 Investigation Objective

The goal of this analysis was to determine whether email authentication controls were properly configured and whether the phishing email could be validated against those controls.

The following technologies were analyzed:

1. SPF (Sender Policy Framework)
2. DKIM (DomainKeys Identified Mail)
3. DMARC (Domain-based Message Authentication, Reporting & Conformance)

<br><br>

# 📧 SPF Analysis

## What is SPF?

SPF (Sender Policy Framework) is an email authentication mechanism that identifies which mail servers are authorized to send emails on behalf of a domain.

When a receiving mail server receives an email, it checks the sender's IP address against the SPF record published in DNS.

If the IP address is not listed, the SPF check fails.

<br><br>

## SPF Record Configured

```dns
v=spf1 ip4:192.168.56.110 -all
```

<br><br>

## SPF Record Breakdown

| Component          | Meaning                   |
| ------------------ | ------------------------- |
| v=spf1             | SPF version               |
| ip4:192.168.56.110 | Authorized mail server IP |
| -all               | Reject all other senders  |

<br><br>

## Validation Command

```bash
dig TXT lab.local @192.168.56.110
```

<br><br>

## Validation Result

```dns
lab.local. IN TXT "v=spf1 ip4:192.168.56.110 -all"
```

### Result

✅ SPF Record Successfully Published

<br><br>

## SOC Analyst Perspective

When investigating phishing emails:

* Check SPF results in email headers
* Identify unauthorized sender IP addresses
* Detect spoofed domains
* Validate sender legitimacy

<br><br>

# ✉️ DKIM Analysis

## What is DKIM?

DKIM (DomainKeys Identified Mail) digitally signs outgoing emails using cryptographic keys.

A receiving mail server verifies the signature using a public key stored in DNS.

This ensures:

* Message integrity
* Sender authenticity
* Protection against email tampering

<br><br>

## DKIM Record Configured

```dns
selector1._domainkey.lab.local
```

<br><br>

## DKIM TXT Record

```dns
v=DKIM1; k=rsa; p=MIGfMA0GCSqGSl...
```

<br><br>

## DKIM Record Breakdown

| Component | Meaning        |
| --------- | -------------- |
| v=DKIM1   | DKIM Version   |
| k=rsa     | RSA Encryption |
| p=        | Public Key     |

<br><br>

## Validation Command

```bash
dig TXT selector1._domainkey.lab.local @192.168.56.110
```

<br><br>

## Validation Result

```dns
selector1._domainkey.lab.local IN TXT
"v=DKIM1; k=rsa; p=MIGfMA0GCSq..."
```

### Result

✅ DKIM Simulation Successfully Validated

<br><br>

## SOC Analyst Perspective

During phishing investigations:

* Review DKIM authentication results
* Verify domain ownership
* Detect forged emails
* Identify unauthorized message modifications

<br><br>

# 🛡️ DMARC Analysis

## What is DMARC?

DMARC (Domain-based Message Authentication, Reporting & Conformance) defines how receiving mail servers should handle emails that fail SPF or DKIM checks.

DMARC helps organizations:

* Prevent spoofing
* Reduce phishing attacks
* Receive authentication reports

<br><br>

## DMARC Record Configured

```dns
v=DMARC1; p=reject; rua=mailto:admin@lab.local
```

<br><br>

## DMARC Record Breakdown

| Component | Meaning              |
| --------- | -------------------- |
| v=DMARC1  | DMARC Version        |
| p=reject  | Reject failed emails |
| rua=      | Reporting mailbox    |

<br><br>

## Validation Command

```bash
dig TXT _dmarc.lab.local @192.168.56.110
```

<br><br>

## Validation Result

```dns
_dmarc.lab.local IN TXT
"v=DMARC1; p=reject; rua=mailto:admin@lab.local"
```

### Result

✅ DMARC Successfully Configured

<br><br>

# 🔍 Authentication Validation Evidence

The following DNS queries were executed from the Kali Linux machine:

```bash
dig TXT lab.local @192.168.56.110
dig TXT _dmarc.lab.local @192.168.56.110
dig TXT selector1._domainkey.lab.local @192.168.56.110
```

All records were successfully returned by the Windows DNS Server.

This confirms:

* SPF Record Published
* DKIM Record Published
* DMARC Record Published
* DNS Resolution Working Correctly

<br><br>

# 📊 Authentication Summary

| Technology | Status       | Purpose                       |
| ---------- | ------------ | ----------------------------- |
| SPF        | ✅ Configured | Validate Sender IP            |
| DKIM       | ✅ Simulated  | Validate Email Integrity      |
| DMARC      | ✅ Configured | Enforce Authentication Policy |

<br><br>

# 🚨 Security Impact

Without SPF, DKIM, and DMARC:

* Attackers can spoof domains
* Phishing emails appear legitimate
* Email impersonation becomes easier
* Users are more likely to trust malicious emails

With proper implementation:

* Unauthorized senders are detected
* Spoofed emails are rejected
* Email trust is improved
* Phishing risk is reduced

<br><br>

# 🎯 SOC Investigation Findings

The phishing email investigation demonstrated that:

✅ SPF was correctly configured

✅ DKIM simulation records were successfully published

✅ DMARC policy was configured with reject enforcement

✅ DNS records were validated from an independent host

✅ Email authentication controls were operational

<br><br>

# 📚 Key SOC Analyst Takeaways

* Always review SPF, DKIM, and DMARC results during email investigations.
* Failed authentication checks may indicate phishing or spoofing attempts.
* DMARC policies provide visibility into authentication failures.
* Email authentication is one of the most effective defenses against phishing attacks.
* Authentication results should always be correlated with email headers, DNS records, and threat intelligence findings.

<br><br>

## 🏁 Conclusion

This analysis validated the successful configuration and operation of SPF, DKIM, and DMARC within the lab environment.

The exercise demonstrated how email authentication technologies help protect organizations from phishing and spoofing attacks while providing valuable investigative data for SOC analysts.

These controls form a critical layer of defense in modern enterprise email security.

