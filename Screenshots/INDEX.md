# 📸 Screenshot Index

## 📌 Overview

This document serves as the master index for all screenshots captured during the **SOC Email Security Investigation Lab**.

The screenshots provide visual evidence of:

* Lab setup and infrastructure configuration
* Email server deployment
* DNS configuration
* Sysmon installation
* Attack simulation
* Email forensic investigation
* Threat intelligence validation
* MITRE ATT&CK mapping
* Network traffic analysis
* Incident response activities

All screenshots were captured from the live lab environment and are referenced throughout the project documentation.

<br><br>

# 🏗️ 01. Lab Setup & Infrastructure

| Screenshot                                  | Description                                                                             |
| ------------------------------------------- | --------------------------------------------------------------------------------------- |
| 01_VirtualBox_Both_VMs_Running.png          | Verification of Kali Linux and Windows Server 2022 running simultaneously in VirtualBox |
| 02_KaliLinux_IP_Address_eth0_eth1.jpg       | Kali Linux network configuration showing NAT and Host-Only adapters                     |
| 03_WindowsServer_IPConfig_Both_Adapters.jpg | Windows Server network configuration and assigned IP addresses                          |
| 04_KaliLinux_Ping_To_WindowsServer.jpg      | Connectivity validation from Kali Linux to Windows Server                               |
| 05_WindowsServer_Ping_To_KaliLinux.jpg      | Connectivity validation from Windows Server to Kali Linux                               |

<br><br>

# 🔧 02. Tool Installation & Verification

| Screenshot                                            | Description                                              |
| ----------------------------------------------------- | -------------------------------------------------------- |
| 06_KaliLinux_Required_Tools_Installed.jpg             | Verification of required tools installed on Kali Linux   |
| 06(a)_KaliLinux_Required_Tools_Installed.jpg          | Additional verification of installed tools               |
| 07_WindowsServer_Sysmon_Installation_Verification.jpg | Sysmon installation verification on Windows Server       |
| 07(a)_WindowsServer_Sysmon_Service_Running.jpg        | Confirmation that Sysmon service is running successfully |
| 08_WindowsServer_Sysmon_Config_Downloaded.jpg         | Sysmon configuration file downloaded                     |
| 08(a)_WindowsServer_Sysmon_Config_Loaded.jpg          | Sysmon configuration successfully loaded                 |
| 08(b)_WindowsServer_Sysmon_Config_Verification.jpg    | Validation of active Sysmon configuration                |

<br><br>

# 📧 03. Mail Server Configuration

| Screenshot                                              | Description                                            |
| ------------------------------------------------------- | ------------------------------------------------------ |
| 09_WindowsServer_hMailServer_Service_Status.jpg         | hMailServer service status verification                |
| 10_hMailServer_Domain_Verification.jpg                  | Email domain configuration validation                  |
| 10(a)_hMailServer_Account_Verification.jpg              | Mail account creation verification                     |
| 10(b)_hMailServer_IP_Ranges_Verification.jpg            | IP range configuration review                          |
| 10(c)_hMailServer_TCPIP_Ports_Verification.jpg          | SMTP/POP3 port configuration verification              |
| 11_hMailServer_Service_Status_Verification.jpg          | Confirmation that hMailServer services are operational |
| 11(a)_WindowsServer_SMTP_Port25_Listening.jpg           | SMTP port 25 listening successfully                    |
| 11(b)_WindowsServer_Firewall_SMTP_Rule_Verification.jpg | Windows Firewall SMTP rule verification                |

<br><br>

# 🌐 04. Email Connectivity Testing

| Screenshot                              | Description                                                   |
| --------------------------------------- | ------------------------------------------------------------- |
| 12_KaliLinux_SMTP_Connectivity_Test.jpg | SMTP connectivity validation between attacker and mail server |

<br><br>

# ⚔️ 05. Attack Simulation Evidence

| Screenshot                             | Description                                         |
| -------------------------------------- | --------------------------------------------------- |
| 13_KaliLinux_Phishing_Email_Sent.jpg   | Successful phishing email delivery using swaks      |
| 14_hMailServer_Email_Received_Logs.jpg | Email delivery confirmation within hMailServer logs |

<br><br>

# 🔍 06. Email Forensics Investigation

| Screenshot                              | Description                                              |
| --------------------------------------- | -------------------------------------------------------- |
| 15_Email_Raw_Header_Extraction.jpg      | Raw email header extraction process                      |
| 15(a)_Attacker_IP_Identification.jpg    | Identification of attacker IP address from email headers |
| 22_Email_Header_Analysis_Evidence.jpg   | Email header forensic analysis evidence                  |
| 23_Email_Investigation_Findings.jpg     | Summary of investigation findings                        |
| 24_Email_Investigation_Timeline.jpg     | Reconstructed attack timeline                            |
| 25_End_to_End_Email_Flow_Validation.jpg | End-to-end email delivery validation                     |
| 26_Email_Investigation_Completed.jpg    | Completion of email investigation workflow               |

<br><br>

# 🔐 07. Email Authentication Validation

| Screenshot                              | Description                                                |
| --------------------------------------- | ---------------------------------------------------------- |
| 27_SPF_Validation.jpg                   | SPF record validation                                      |
| 27(a)_DMARC_Validation.jpg              | DMARC record validation                                    |
| 27(b)_DKIM_Validation.jpg               | DKIM simulation validation                                 |
| 28_DNS_Email_Authentication_Records.jpg | DNS records containing SPF, DKIM, and DMARC configurations |

<br><br>

# 🌍 08. Threat Intelligence Validation

| Screenshot                                    | Description                                  |
| --------------------------------------------- | -------------------------------------------- |
| 16_VirusTotal_Attacker_IP_Validation.jpg      | VirusTotal validation of attacker IP address |
| 16(a)_VirusTotal_Malicious_URL_Validation.jpg | VirusTotal validation of phishing URL        |

<br><br>

# 🗺️ 09. MITRE ATT&CK Mapping

| Screenshot                                | Description                                      |
| ----------------------------------------- | ------------------------------------------------ |
| 17_MITRE_T1566_Mapping.jpg                | MITRE ATT&CK T1566 mapping evidence              |
| 18_ATTACK_Navigator_T1566_Highlighted.jpg | ATT&CK Navigator highlighting observed technique |

<br><br>

# 📊 10. Log Analysis & Network Forensics

| Screenshot                              | Description                               |
| --------------------------------------- | ----------------------------------------- |
| 19_Sysmon_Network_Connection_Events.jpg | Sysmon network connection telemetry       |
| 20_Wireshark_SMTP_Email_Traffic.jpg     | SMTP traffic captured in Wireshark        |
| 21_Wireshark_PCAP_Saved.jpg             | Saved PCAP file for forensic preservation |

<br><br>

# 📈 Evidence Summary

| Category                         | Screenshot Count |
| -------------------------------- | ---------------- |
| Lab Setup & Infrastructure       | 5                |
| Tool Installation & Verification | 6                |
| Mail Server Configuration        | 8                |
| Connectivity Testing             | 1                |
| Attack Simulation                | 2                |
| Email Forensics                  | 7                |
| Email Authentication             | 4                |
| Threat Intelligence              | 2                |
| MITRE ATT&CK                     | 2                |
| Log Analysis & Network Forensics | 3                |

### Total Screenshots Collected

**40+ Investigation Artifacts and Validation Screenshots**

<br><br>

# 🏁 Conclusion

The screenshots contained within this repository provide visual evidence supporting every phase of the phishing investigation lifecycle.

These artifacts demonstrate:

✅ Lab Construction

✅ Infrastructure Validation

✅ Email Server Deployment

✅ Attack Simulation

✅ Email Forensics

✅ Threat Intelligence Analysis

✅ MITRE ATT&CK Mapping

✅ Detection Engineering

✅ Incident Response Documentation

The collected evidence ensures the investigation remains reproducible, verifiable, and suitable for SOC analyst portfolio review.
