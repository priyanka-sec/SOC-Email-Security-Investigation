# 🛡️ Sysmon Configuration

## 📌 Overview

Sysmon (System Monitor) is a Windows system service from the Microsoft Sysinternals Suite that provides detailed visibility into system activity.

Unlike default Windows Event Logs, Sysmon records high-value security events that help SOC analysts detect malicious activity, investigate incidents, and perform threat hunting.

In this project, Sysmon was deployed on the Windows Server 2022 mail server to collect endpoint telemetry during the phishing attack simulation.

<br><br>

# 🎯 Objectives

The primary objectives of deploying Sysmon were:

* Monitor network connections made during email delivery
* Capture process execution activity
* Record DNS-related events
* Improve endpoint visibility for investigations
* Generate forensic evidence for SOC analysis
* Support detection engineering use cases

<br><br>

# 🏗️ Environment Information

| Component        | Value                                |
| ---------------- | ------------------------------------ |
| Operating System | Windows Server 2022                  |
| Monitoring Tool  | Sysmon                               |
| Vendor           | Microsoft Sysinternals               |
| Configuration    | SwiftOnSecurity Sysmon Configuration |
| Host IP Address  | 192.168.56.110                       |
| Role             | Victim Mail Server                   |

<br><br>

# 🔧 Sysmon Installation Process

## Step 1 — Download Sysmon

Sysmon was downloaded from Microsoft Sysinternals.

Downloaded files:

```text
Sysmon64.exe
Sysmon.exe
```

<br><br>

## Step 2 — Download Sysmon Configuration

The SwiftOnSecurity Sysmon configuration was used because it is widely adopted by SOC teams and provides high-quality logging while minimizing unnecessary noise.

Configuration File:

```text
sysmonconfig-export.xml
```

<br><br>

## Step 3 — Install Sysmon

Sysmon was installed using an administrative PowerShell terminal.

Example command:

```powershell
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

<br><br>

## Step 4 — Verify Installation

Installation was verified using:

```powershell
Get-Service Sysmon64
```

Expected Result:

```text
Status : Running
Name   : Sysmon64
```

<br><br>

# 📊 Important Sysmon Event IDs

The following Sysmon events are commonly used by SOC analysts.

| Event ID | Description                |
| -------- | -------------------------- |
| 1        | Process Creation           |
| 2        | File Creation Time Changed |
| 3        | Network Connection         |
| 5        | Process Terminated         |
| 6        | Driver Loaded              |
| 7        | Image Loaded               |
| 8        | Create Remote Thread       |
| 10       | Process Access             |
| 11       | File Created               |
| 12       | Registry Object Created    |
| 13       | Registry Value Set         |
| 22       | DNS Query                  |
| 23       | File Delete                |
| 24       | Clipboard Change           |
| 25       | Process Tampering          |

<br><br>

# 🔍 Events Observed During Investigation

During the phishing attack simulation, Sysmon generated network connection events associated with SMTP communications.

Observed Event:

| Event ID | Description        |
| -------- | ------------------ |
| 3        | Network Connection |

Investigation Findings:

* SMTP traffic observed on Port 25
* Connection activity correlated with email delivery
* Network events supported attack timeline reconstruction
* Endpoint telemetry validated attacker-to-server communication

<br><br>

# 🧠 SOC Analyst Value

Sysmon significantly improves visibility compared to standard Windows logging.

Benefits for SOC Analysts:

✅ Process Monitoring

✅ Network Monitoring

✅ DNS Visibility

✅ Threat Hunting

✅ IOC Validation

✅ Incident Investigation

✅ Detection Engineering

✅ Forensic Analysis

<br><br>

# 🔎 Detection Opportunities

Sysmon logs can be used to create detections for:

* Suspicious SMTP activity
* Malware execution
* PowerShell abuse
* Credential dumping attempts
* Lateral movement activity
* Malicious DNS queries
* Persistence mechanisms
* Unauthorized network connections

<br><br>

# 📸 Evidence Collected

The following screenshots were captured during this project:

```text
07_WindowsServer_Sysmon_Installation_Verification.jpg
07(a)_WindowsServer_Sysmon_Service_Running.jpg
08_WindowsServer_Sysmon_Config_Downloaded.jpg
08(a)_WindowsServer_Sysmon_Config_Loaded.jpg
08(b)_WindowsServer_Sysmon_Config_Verification.jpg
19_Sysmon_Network_Connection_Events.jpg
```

<br><br>

# 🎯 Outcome

Sysmon was successfully deployed and configured on the Windows Server 2022 mail server.

The collected telemetry provided valuable endpoint visibility during the phishing investigation and enabled the identification of network activity associated with email delivery.

The implementation demonstrates practical experience with endpoint monitoring, log analysis, detection engineering, and SOC investigation workflows commonly used in enterprise Security Operations Centers.
