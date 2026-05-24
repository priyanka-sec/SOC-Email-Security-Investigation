# 📧 Email Header Forensic Analysis

**Investigation ID:** INC-2026-001  
**Analyst:** Priyanka Rane  
**Date of Analysis:** 06 May 2026  
**Severity:** 🔴 High  
**Classification:** Phishing — Credential Harvesting  

<br><br>

## 1. Raw Email (.eml File)

> **Source:** `C:\Program Files (x86)\hMailServer\Data\lab.local\victim\3B\`  
> **Opened with:** Notepad (raw text extraction)

```
Return-Path: attacker@lab.local
Received: from kali (Unknown [192.168.56.10])
                      by 192.168.56.110 with ESMTP
                      ; Wed, 6 May 2026 07:19:47  -0700
Date: Wed, 06 May 2026 19:49:46 +0530
To: victim@lab.local
From: attacker@lab.local
Subject: Urgent: Reset Your Password Immediately
Message-Id: <20260506194946.003466@kali>
X-Mailer: swaks v20240103.0 jetmore.org/john/code/swaks/

Dear User, Your account has been compromised. Click here to reset your
password immediately: http://192.168.56.10/reset. Regards, IT Security Team
```

<br><br>

## 2. Header Field-by-Field Forensic Breakdown

### 🔴 Field 1 — `Received` (Most Critical)

```
Received: from kali (Unknown [192.168.56.10])
          by 192.168.56.110 with ESMTP
          ; Wed, 6 May 2026 07:19:47 -0700
```

| Sub-field | Value | Forensic Significance |
|-----------|-------|----------------------|
| `from kali` | Hostname declared by sending machine | Self-reported — attacker controlled, **cannot be trusted** |
| `Unknown` | Reverse DNS result for sending IP | **No PTR record exists** — legitimate mail servers always have one. Absence is a red flag. |
| `[192.168.56.10]` | **True originating IP of the attacker** | This field is added by the *receiving* mail server and is considered significantly more trustworthy than attacker-controlled fields. |
| `by 192.168.56.110` | IP of the receiving mail server (victim) | Confirms our hMailServer instance received the email |
| `with ESMTP` | Protocol used for delivery | Extended SMTP — standard delivery protocol |
| Timestamp | `Wed, 6 May 2026 07:19:47 -0700` | Receiving server's timestamp (UTC-7) |

> 🔍 **Analyst Note:** The `Received` field is always written by the **receiving mail server**, not the sender. This makes `192.168.56.10` the highest-confidence IOC in this investigation because it was recorded by the receiving mail server and is considered a highly reliable forensic artifact.

<br><br>

### 🟠 Field 2 — `Return-Path`

```
Return-Path: attacker@lab.local
```

| Sub-field | Value | Forensic Significance |
|-----------|-------|----------------------|
| Return-Path | `attacker@lab.local` | The bounce-back address if delivery fails. Set by the attacker via `swaks`. Confirms the sender address used in the attack. |

> 🔍 **Analyst Note:** `Return-Path` should match the `From` field in legitimate email. Here both are `attacker@lab.local` — the attacker did not attempt to spoof a trusted domain, which means there was **no domain impersonation** in this specific scenario. The attack relied on urgency/social engineering instead.

<br><br>

### 🟡 Field 3 — `Date` (Timestamp Discrepancy)

```
Date: Wed, 06 May 2026 19:49:46 +0530
```

| Detail | Value | Forensic Significance |
|--------|-------|-----------------------|
| Claimed send time | `19:49:46 +0530` (IST) | **Set by the attacker machine (Kali Linux)** — can be manipulated |
| Server-stamped receive time | `07:19:47 -0700` (PDT) | Set by hMailServer — reliable |
| IST to UTC conversion | 19:49:46 − 5:30 = **14:19:46 UTC** | |
| PDT to UTC conversion | 07:19:47 + 7:00 = **14:19:47 UTC** | |
| **Discrepancy** | **1 second** | Negligible — confirms timestamps are consistent |

> 🔍 **Analyst Note:** Converting both timestamps to UTC reveals only a 1-second gap — this is normal network transmission delay. The timestamps are **consistent and corroborate each other**. In real phishing attacks, large timestamp discrepancies (hours or days) indicate timezone spoofing or delayed relay through a compromised server.

<br><br>

### 🟡 Field 4 — `From`

```
From: attacker@lab.local
```

| Detail | Value | Forensic Significance |
|--------|-------|-----------------------|
| Display name | *(none set)* | Attacker did not craft a deceptive display name. In real phishing, this would be `"IT Security Team" <attacker@lab.local>` to hide the address in email clients. |
| Domain | `lab.local` | Internal lab domain — in a real attack this would be a lookalike domain (e.g. `support@lab-secure.com`) |

<br><br>

### 🟡 Field 5 — `To`

```
To: victim@lab.local
```

| Detail | Value | Forensic Significance |
|--------|-------|-----------------------|
| Recipient | `victim@lab.local` | Confirms the targeted mailbox. In real attacks, `To` may be generic (`undisclosed-recipients`) if BCC was used for bulk phishing. |

<br><br>

### 🟠 Field 6 — `Subject`

```
Subject: Urgent: Reset Your Password Immediately
```

| Technique | Detail |
|-----------|--------|
| **Urgency trigger** | "Urgent" and "Immediately" create time pressure — a classic social engineering tactic |
| **Authority impersonation** | Implies the email comes from IT/Security team |
| **Action demand** | Directs the victim to take a specific action (click a link) |
| **MITRE mapping** | T1566.002 — Spearphishing Link; also aligns with T1585 social engineering patterns |

> 🔍 **Analyst Note:** This subject line uses two of the most effective phishing triggers: **urgency** and **authority**. Security awareness training programs specifically train users to pause when they see these words together. Flagging subject lines with `Urgent:` + password-related terms is a simple but effective email gateway rule.

<br><br>

### 🔴 Field 7 — `X-Mailer` (Attack Tool Fingerprint)

```
X-Mailer: swaks v20240103.0 jetmore.org/john/code/swaks/
```

| Detail | Value | Forensic Significance |
|--------|-------|-----------------------|
| Tool identified | `swaks` (Swiss Army Knife for SMTP) | A command-line SMTP testing tool commonly associated with SMTP testing and scripted email delivery activity |
| Version | `v20240103.0` | Specific build date: 3 January 2024 |
| Source URL | `jetmore.org/john/code/swaks/` | Openly included — attacker did not strip this header |

> 🔴 **Critical Finding:** The presence of `X-Mailer: swaks` is a **definitive indicator of an automated/scripted email attack**. No legitimate email client or server produces this header. A SIEM rule or email gateway rule filtering for `X-Mailer` values containing `swaks`, `curl`, `python-requests`, or `Go-http-client` would have flagged and blocked this email automatically.
>
> **Detection Rule Concept (Sigma-style):**
> ```
> title: Swaks Tool Detected in Email X-Mailer Header
> condition: email.header.x_mailer contains 'swaks'
> severity: high
> ```

<br><br>

### 🟡 Field 8 — `Message-Id`

```
Message-Id: <20260506194946.003466@kali>
```

| Detail | Value | Forensic Significance |
|--------|-------|-----------------------|
| Timestamp component | `20260506194946` → 06 May 2026, 19:49:46 | Consistent with `Date` field — no anomaly |
| Domain component | `@kali` | The sending machine's hostname is `kali` — confirms attacker machine identity |
| Format | Non-standard (legitimate servers use FQDNs like `@mail.domain.com`) | Another signal that this did not come from a real mail infrastructure |

<br><br>

## 3. SPF / DKIM / DMARC Analysis

> **Finding: None of the three email authentication mechanisms are present in this header.**

| Protocol | Present? | Expected Header | Forensic Meaning |
|----------|----------|-----------------|------------------|
| **SPF** | ❌ Absent | `Received-SPF: pass` or `fail` | No SPF record exists for `lab.local`. The receiving server did not check or enforce SPF. |
| **DKIM** | ❌ Absent | `DKIM-Signature: v=1; a=rsa-sha256; ...` | No cryptographic signature on the email. Content integrity cannot be verified. |
| **DMARC** | ❌ Absent | `Authentication-Results: dmarc=pass` | No policy enforced. Even if SPF/DKIM failed, no action (quarantine/reject) would be taken. |

> 🔍 **Analyst Note:** The complete absence of SPF, DKIM, and DMARC is the **root cause that enabled this attack to be delivered**. In an enterprise environment with properly configured email authentication:
> - **SPF** would have flagged `192.168.56.10` as an unauthorised sender for `lab.local`
> - **DKIM** would have detected that the email was not cryptographically signed by `lab.local`'s mail server
> - **DMARC** policy (`p=reject`) would have caused the email to be **rejected outright** before reaching the victim's inbox
>
> **Remediation:** Configure SPF, DKIM, and DMARC records in DNS for `lab.local` and enforce `p=reject` DMARC policy.

<br><br>

## 4. Email Body Analysis

```
Dear User, Your account has been compromised. Click here to reset your
password immediately: http://192.168.56.10/reset. Regards, IT Security Team
```

| Element | Value | Forensic Significance |
|---------|-------|-----------------------|
| Salutation | `Dear User` | **Generic** — not personalised. In targeted spearphishing, attackers use the victim's real name. |
| Claim | `Your account has been compromised` | Fear-based trigger to lower critical thinking |
| Malicious URL | `http://192.168.56.10/reset` | Raw IP address — no domain masking used. In real attacks this would be a typosquatted domain with HTTPS. |
| Signature | `IT Security Team` | **Authority impersonation** — creates false legitimacy |
| Protocol | `http://` (not https) | Unencrypted link — legitimate password reset pages always use HTTPS |

> 🔍 **Analyst Note:** The use of a raw IP address (`192.168.56.10`) instead of a domain name in the malicious URL is a significant red flag that most email gateways and browser filters would catch. In a real-world attack this URL would be:
> - A lookalike domain: `http://lab-secure-reset.com/reset`
> - HTTPS-enabled with a free TLS certificate
> - Potentially URL-shortened to hide the destination

<br><br>

## 5. Full IOC Summary

| # | IOC Type | Value | Source in Header | Confidence | Disposition |
|---|----------|-------|-----------------|------------|-------------|
| 1 | IP Address | `192.168.56.10` | `Received` field | 🔴 High | Attacker Machine IP |
| 2 | IP Address | `192.168.56.110` | `Received` — `by` field | 🔴 High | Victim Mail Server |
| 3 | Email Address | `attacker@lab.local` | `Return-Path`, `From` | 🔴 High | Attacker / Spoofed Sender |
| 4 | Email Address | `victim@lab.local` | `To` | 🔴 High | Targeted Victim |
| 5 | URL | `http://192.168.56.10/reset` | Email body | 🔴 High | Fake Credential Harvesting Page |
| 6 | Hostname | `kali` | `Received` — `from` field, `Message-Id` | 🟠 Medium | Attacker Machine Hostname |
| 7 | Tool Signature | `swaks v20240103.0` | `X-Mailer` | 🔴 High | Attack Tool Fingerprint |
| 8 | Subject Pattern | `Urgent: Reset Your Password Immediately` | `Subject` | 🟡 Medium | Social Engineering Indicator |

<br><br>

## 6. Attack Reconstruction Timeline

```
19:49:46 IST  →  Attacker (192.168.56.10 / kali) initiates SMTP connection to 192.168.56.110:25
19:49:46 IST  →  swaks delivers phishing email via ESMTP
19:49:47 IST  →  hMailServer receives and stores email in victim mailbox
19:49:47 IST  →  .eml file written to: C:\Program Files (x86)\hMailServer\Data\lab.local\victim\3B\
[Post-delivery] →  Victim would see: urgent subject line, IT Security Team branding, password reset link
[If clicked]   →  Victim browser navigates to http://192.168.56.10/reset (credential harvesting page)
```

<br><br>

## 7. Analyst Conclusion

This phishing email was successfully delivered due to **three compounding failures**:

1. **No email authentication (SPF/DKIM/DMARC)** — the mail server accepted email from any source for `lab.local` without verification
2. **No email gateway filtering** — no rule to flag `X-Mailer: swaks`, raw IP URLs, or urgency-pattern subjects
3. **Social engineering effectiveness** — the email used authority impersonation and urgency to drive action

The **highest-confidence forensic artifact** is the IP address `192.168.56.10` stamped in the `Received` header by the victim mail server — this single field unambiguously identifies the attacker's machine and cannot be falsified.

<br><br>

*Document prepared as part of SOC Incident Investigation INC-2026-001*  
*Analyst: Priyanka Rane | Classification: Internal / Portfolio*
