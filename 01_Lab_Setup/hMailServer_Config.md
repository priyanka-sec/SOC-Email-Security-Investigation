# 📧 hMailServer Configuration Guide

## 🎯 Objective

The purpose of configuring hMailServer in this lab was to simulate a real-world email infrastructure that could receive, process, and log phishing emails for SOC investigation purposes.

The mail server acted as the victim email environment and allowed phishing emails sent from Kali Linux to be delivered, logged, and analysed throughout the investigation lifecycle.

<br><br>

# 🏗️ Overview

hMailServer is a free Windows-based email server that supports:

* SMTP (Simple Mail Transfer Protocol)
* POP3 (Post Office Protocol)
* IMAP (Internet Message Access Protocol)

In this project, hMailServer was used to:

✅ Receive phishing emails

✅ Generate SMTP logs

✅ Store email messages

✅ Provide raw email headers

✅ Support email forensic investigations

✅ Simulate enterprise email infrastructure

<br><br>

# 🖥️ Environment Details

| Component         | Value               |
| ----------------- | ------------------- |
| Mail Server       | hMailServer         |
| Operating System  | Windows Server 2022 |
| Server IP Address | 192.168.56.110      |
| Domain            | lab.local           |
| Protocol Used     | SMTP                |
| SMTP Port         | 25                  |
| Attacker System   | Kali Linux          |
| Attacker IP       | 192.168.56.10       |

<br><br>

# 📧 Domain Configuration

A new email domain was created inside hMailServer.

### Domain Name

```text
lab.local
```

Purpose:

* Simulate a corporate email environment
* Host user mailboxes
* Support phishing email delivery

<br><br>

# 👤 Email Account Configuration

A victim mailbox was created to receive phishing emails.

### Mailbox Created

```text
victim@lab.local
```

Purpose:

* Target account for phishing simulation
* Email forensic analysis
* Header extraction
* IOC investigation

<br><br>

# ⚙️ SMTP Service Configuration

SMTP was enabled to allow incoming email delivery.

### SMTP Port

```text
25
```

Purpose:

* Accept email messages
* Receive phishing emails from attacker machine
* Generate SMTP transaction logs

<br><br>

# 🌐 IP Range Configuration

The default Internet IP Range was used.

Purpose:

* Allow SMTP communication between lab systems
* Support email delivery from Kali Linux
* Enable phishing simulation

<br><br>

# 📜 Logging Configuration

SMTP logging was enabled within hMailServer.

The following logs were generated during testing:

* SMTP Connection Logs
* SMTP Delivery Logs
* Message Processing Logs
* Client Connection Logs

These logs were later used during the SOC investigation process.

<br><br>

# 🔍 Validation Performed

The following validation checks were completed after configuration:

### Domain Verification

Confirmed:

```text
lab.local
```

was successfully created.

Evidence:

```text
10_hMailServer_Domain_Verification.jpg
```

<br><br>

### Account Verification

Confirmed:

```text
victim@lab.local
```

exists and is operational.

Evidence:

```text
10(a)_hMailServer_Account_Verification.jpg
```

<br><br>

### IP Range Verification

Confirmed SMTP traffic was allowed through configured IP ranges.

Evidence:

```text
10(b)_hMailServer_IP_Ranges_Verification.jpg
```

<br><br>

### TCP/IP Port Verification

Confirmed SMTP service listening on:

```text
Port 25
```

Evidence:

```text
10(c)_hMailServer_TCPIP_Ports_Verification.jpg
```

<br><br>

### Service Status Verification

Confirmed hMailServer services were running successfully.

Evidence:

```text
09_WindowsServer_hMailServer_Service_Status.jpg
```

```text
11_hMailServer_Service_Status_Verification.jpg
```

<br><br>

### SMTP Port Verification

Confirmed Windows Server listening on SMTP Port 25.

Evidence:

```text
11(a)_WindowsServer_SMTP_Port25_Listening.jpg
```

<br><br>

### Firewall Rule Verification

Confirmed firewall permitted SMTP communication.

Evidence:

```text
11(b)_WindowsServer_Firewall_SMTP_Rule_Verification.jpg
```

<br><br>

# 🧪 Phishing Email Delivery Test

A phishing email was sent from Kali Linux using:

```bash
swaks
```

The email was successfully delivered to:

```text
victim@lab.local
```

Evidence:

```text
13_KaliLinux_Phishing_Email_Sent.jpg
```

<br><br>

# 📊 SOC Investigation Value

The hMailServer configuration enabled several important SOC investigation activities:

### Email Forensics

* Raw Header Analysis
* Message Tracing
* Sender Identification
* Timestamp Analysis

### Threat Hunting

* Attacker IP Discovery
* SMTP Session Tracking
* Delivery Verification

### IOC Extraction

* Email Addresses
* IP Addresses
* URLs
* Mail Client Artifacts

### Incident Response

* Email Validation
* Log Correlation
* Attack Timeline Reconstruction

<br><br>

# ✅ Configuration Outcome

The hMailServer deployment was successfully configured and validated.

The server successfully:

* Accepted SMTP connections
* Received phishing emails
* Generated investigation logs
* Supported email forensic analysis
* Enabled IOC extraction
* Supported end-to-end SOC investigation activities

This mail infrastructure served as the foundation for the phishing attack simulation and subsequent email security investigation performed throughout this project.

