# Capstone Project  
CYART  
inquiry@cyart.io  
www.cyart.io  

<br>

## 1. Objective  

- This report outlines the tasks related to attack simulation, detection & triage, response, reporting, and stakeholder briefing.  
- The objectives of these tasks are to:  
  • Simulate a system compromise scenario to gain authorized access for training purposes.  
  • Configure a SIEM platform to generate alerts for detected threats.  
  • Isolate the affected virtual machine and use CrowdSec to block the attacker’s IP address.  
  • Create documentation following the recommended SANS template.  

<br>

## 2. Introduction  

This task includes the creation of a complete alert-to-response cycle.  
The cycle includes:  
- Attack Simulation  
- Detection & Triage  
- Response  
- Reporting  
- Stakeholder Briefing  

<br>

## 3. Target & Attacker Description  

- Local Virtual Machine  
- **Target:** Host A (Metasploit)  
- **IP Address:** 192.168.0.107  
- **Attacker:** Host B (Linux machine)  

<br>

## 4. Tools & Setup  

- **Metasploit:** Install Metasploit on a Linux VM  

sudo apt install metasploit-framework

- **CrowdSec:** Install from documentation  
https://docs.crowdsec.net/  

- **Google Docs** accessible via docs.google.com  

<br>

## 5. Attack Simulation  

An attack was performed on the target machine **Metasploitable2** using **Kali Linux**, via `msfconsole`.

Example module used:  
use exploit/unix/ftp/vsftpd_234_backdoor

<br>

### Nmap Scan (192.168.0.107)  

- Nmap 7.95 used to scan 192.168.0.107  
- Target reachable and confirmed online  
- 977 closed TCP ports (not shown)  
- Open ports discovered:  
  - 21 (FTP)  
  - 22 (SSH)  
  - 23 (Telnet)  
  - 25 (SMTP)  
  - 53 (DNS)  
  - 80 (HTTP)  
  - 3306 (MySQL)  
  - 5432 (PostgreSQL)  
  - 5900 (VNC)  
  - Many additional ports → indicates broad attack surface  
- MAC address points to an **Oracle VirtualBox NIC**, confirming virtualization  

<br>

### Metasploit: vsftpd 2.3.4 Backdoor Exploit  

- Metasploit used to locate exploit for vsftpd 2.3.4  
- Module loaded:  

exploit/unix/ftp/vsftpd_234_backdoor

- Module options required: RHOSTS + RPORT (21)  
- Configuration target: **192.168.0.107**  
- Result:  
- FTP banner received  
- Exploit executed  
- **No session created** → attack unsuccessful  

<br>

## 6. Detection and Triage  

Wazuh was configured to raise alerts when attack logs were detected.  
The screenshot indicates the backdoor attempt triggered an alert.

<br>

| Timestamp     | Source IP     | Alert Description | MITRE Technique |
|----------------|---------------|------------------|-----------------|
| 2025-11-07     | 192.168.0.106 | VSFTPD           | T1190           |

<br>

## 7. Response  

- VM was isolated  
- Attacker IP address was blocked using **CrowdSec**  
- Blocklisted IP is visible in CrowdSec dashboard  

<br>

## 8. Reporting  

Reporting followed the **SANS template**, including:  
- Executive Summary  
- Timeline  
- Recommendations  

<br>

### 1) Executive Summary  

- **Incident Title / Name:** VSFTPD  
- **Date & Time Detected:** 07-11-2025 10:02:00  
- **Reported By / Detection Source:** SIEM  
- **Analyst Assigned:** SOC Analyst  
- **Severity Level:** Critical  

<br>

### 2) Timeline  

| Date/Time | Event Description |
|-----------|------------------|
| 10:02:00  | Wazuh alert triggered for VSFTPD exploit from IP [192.168.0.106] |
| 10:20:12  | SOC Analyst confirmed exploit + assigned Critical severity |
| 10:35:38  | Containment → VM isolated |
| 10:55:10  | Eradication → Attacker IP [192.168.0.106] blocked via CrowdSec |

<br>

### 3) Recommendations  

- **Immediate Remediation:**  
Disable/remove vulnerable **vsftpd 2.3.4** or upgrade.

- **Network Hardening:**  
Enforce host-based firewall rules; restrict access ports.

- **Vulnerability Management:**  
Conduct daily/weekly scans to identify high severity CVEs.  

<br>

## 9. Stakeholder Briefing  

Stakeholder briefing translates the incident into non-technical business language.  

<br>

### Example Briefing Email  

**Subject:**  
Security Incident Briefing: Critical Vulnerability Contained  

**Message:**  
We effectively addressed a high-severity security event involving an attempted compromise of an outdated public-facing system.  
An external threat actor tried exploiting a known vulnerability to gain unauthorized server access.  

Monitoring platforms generated an alert, enabling the SOC team to quickly isolate the affected system and block the attacker’s IP.  
The incident was fully contained within minutes, with **no data loss or business disruption**.  

Decommissioning the vulnerable asset immediately is strongly recommended.  
The threat has been eradicated.  

<br>

---

CYART  
inquiry@cyart.io  
www.cyart.io  
