# 🏗️ Lab Setup Guide

## 📌 Overview

This document explains the complete setup of the SOC Email Security Investigation Lab used throughout this project.

The objective of this lab was to create an isolated environment where phishing attacks could be safely simulated, investigated, and documented using real SOC investigation methodologies.

The lab was built using Oracle VM VirtualBox and consists of:

* 🐉 Kali Linux (Attacker Machine)
* 🖥️ Windows Server 2022 (Victim / Mail Server)
* 📧 hMailServer
* 🌐 Windows DNS Server
* 📊 Sysmon
* 🔍 Wireshark

<br><br>

# 🎯 Lab Objectives

The lab was designed to achieve the following goals:

✅ Simulate phishing email delivery

✅ Capture SMTP network traffic

✅ Perform email header analysis

✅ Configure SPF, DKIM, and DMARC

✅ Generate investigation artifacts

✅ Create SOC detection opportunities

✅ Practice incident response workflows

✅ Map activity to MITRE ATT&CK

<br><br>

# 🏛️ Lab Architecture

```text
+----------------------------------------------------+
|                 VirtualBox Host                    |
+----------------------------------------------------+

      Kali Linux                     Windows Server 2022
      (Attacker)                     (Victim/Mail Server)

      192.168.56.10                  192.168.56.110

            |                               |
            |---------- SMTP : 25 ----------|
            |                               |

      Tools:                         Services:
      • swaks                        • hMailServer
      • Wireshark                    • DNS Server
                                     • Sysmon
                                     • Windows Event Logs
```

<br><br>

# 🖥️ Virtual Machines

## 1️⃣ Kali Linux

### Purpose

Used to simulate attacker activity and phishing email delivery.

### Operating System

```text
Kali Linux
```

### Network Adapters

| Adapter   | Type              | Purpose                           |
| --------- | ----------------- | --------------------------------- |
| Adapter 1 | NAT               | Internet Access                   |
| Adapter 2 | Host-Only Adapter | Communication with Windows Server |

### IP Address

```text
192.168.56.10
```

### Installed Tools

| Tool      | Purpose                |
| --------- | ---------------------- |
| swaks     | SMTP attack simulation |
| Wireshark | Packet capture         |
| dig       | DNS validation         |
| ping      | Connectivity testing   |

<br><br>

## 2️⃣ Windows Server 2022

### Purpose

Acts as the victim environment and email infrastructure server.

### Operating System

```text
Windows Server 2022
```

### Network Adapters

| Adapter   | Type              | Purpose                       |
| --------- | ----------------- | ----------------------------- |
| Adapter 1 | NAT               | Internet Access               |
| Adapter 2 | Host-Only Adapter | Communication with Kali Linux |

### IP Address

```text
192.168.56.110
```

<br><br>

# 🌐 Network Configuration

## Host-Only Network

```text
Network Range:
192.168.56.0/24
```

### Assigned Addresses

| System         | IP Address     |
| -------------- | -------------- |
| Kali Linux     | 192.168.56.10  |
| Windows Server | 192.168.56.110 |

<br><br>

# 📧 Email Infrastructure

## hMailServer

hMailServer was installed on Windows Server 2022 to provide SMTP functionality.

### Purpose

* Receive emails
* Process SMTP traffic
* Generate mail logs
* Support phishing simulation

### Configured Domain

```text
lab.local
```

### Email Accounts

```text
attacker@lab.local
victim@lab.local
admin@lab.local
```

<br><br>

# 🌐 DNS Infrastructure

Windows DNS Server was configured to host email authentication records.

### DNS Zone

```text
lab.local
```

### Records Configured

#### SPF

```text
v=spf1 ip4:192.168.56.110 -all
```

#### DKIM (Simulation)

```text
selector1._domainkey.lab.local
```

#### DMARC

```text
v=DMARC1; p=reject; rua=mailto:admin@lab.local
```

<br><br>

# 📊 Logging Configuration

## Sysmon

Sysmon was installed to capture endpoint telemetry.

### Logging Objectives

* Process Creation Events
* Network Connections
* DNS Queries
* Security Monitoring

### Verification

Sysmon service successfully installed and running.

<br><br>

# 🔍 Network Monitoring

## Wireshark

Wireshark was installed to capture SMTP traffic generated during phishing simulations.

### Captured Protocols

* SMTP
* DNS
* TCP

### Purpose

* Packet analysis
* SMTP conversation review
* Evidence collection
* PCAP preservation

<br><br>

# 🧪 Connectivity Validation

The following tests were performed before beginning attack simulations.

### Kali → Windows Server

```bash
ping 192.168.56.110
```

Result:

```text
Successful
```

### Windows Server → Kali

```powershell
ping 192.168.56.10
```

Result:

```text
Successful
```

### SMTP Connectivity

```bash
nc -vz 192.168.56.110 25
```

Result:

```text
SMTP Port Reachable
```

<br><br>

# 📸 Supporting Evidence

The following screenshots validate successful lab setup.

| Screenshot                                            | Description                          |
| ----------------------------------------------------- | ------------------------------------ |
| 01_VirtualBox_Both_VMs_Running.png                    | Both virtual machines operational    |
| 02_KaliLinux_IP_Address_eth0_eth1.jpg                 | Kali network configuration           |
| 03_WindowsServer_IPConfig_Both_Adapters.jpg           | Windows Server network configuration |
| 04_KaliLinux_Ping_To_WindowsServer.jpg                | Connectivity validation              |
| 05_WindowsServer_Ping_To_KaliLinux.jpg                | Connectivity validation              |
| 06_KaliLinux_Required_Tools_Installed.jpg             | Required tools installed             |
| 07_WindowsServer_Sysmon_Installation_Verification.jpg | Sysmon installation verification     |
| 09_WindowsServer_hMailServer_Service_Status.jpg       | hMailServer operational              |

<br><br>

# ✅ Lab Setup Status

| Component                       | Status     |
| ------------------------------- | ---------- |
| VirtualBox Environment          | ✅ Complete |
| Kali Linux Configuration        | ✅ Complete |
| Windows Server Configuration    | ✅ Complete |
| hMailServer Setup               | ✅ Complete |
| DNS Server Setup                | ✅ Complete |
| Sysmon Deployment               | ✅ Complete |
| Wireshark Installation          | ✅ Complete |
| Network Connectivity Validation | ✅ Complete |

<br><br>

# 🎯 Key Takeaways

* Successfully built a fully isolated phishing investigation lab.
* Configured enterprise-style email infrastructure.
* Implemented SPF, DKIM, and DMARC records.
* Enabled endpoint and network logging.
* Created a realistic environment for SOC investigations.
* Established a repeatable platform for future Email Security, SOC, and Detection Engineering projects.

