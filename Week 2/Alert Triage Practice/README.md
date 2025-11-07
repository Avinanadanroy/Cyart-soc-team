# Alert Triage Practice  
CYART  
inquiry@cyart.io  
www.cyart.io  

<br>

## 1. Triage Simulation  

Triage simulation includes analyzing a mock alert  
(e.g., **“Brute-Force SSH Attempts”**) in Wazuh.  

<br>

### Alert Simulation  

**Attack Preparation:**  
An attacker on **Kali Linux** prepares an SSH brute-force attack using **Metasploit**.  
The target is **192.168.0.107 (RHOSTS)** attempting to guess the password for user `msfadmin`  
using a wordlist located at:  
/home/kali/password.txt

<br>

**Attack Detection:**  
On the victim server (**metasploitable**), authentication logs at:
/var/log/auth.log

show multiple failed SSH logins from attacker IP **192.168.0.106**.  
Log entries confirm brute-force behavior, including use of username `msfadmin`.  

<br>

---

## 2. Alert Analysis  

Alert analysis involves reviewing metadata:  
- Alert ID  
- Description  
- Source IP  
- Priority  
- Status  

<br>

### Alert Metadata Table  

| Alert ID | Description            | Source IP     | Priority | Status |
|----------|------------------------|---------------|----------|--------|
| 001      | Brute-Force SSH Attempts | 192.168.0.106 | Medium   | Open   |

<br>

---

## 3. Threat Intelligence Validation  

Threat intelligence validation confirms potential threats using IOCs.  
Platforms such as **AlienVault OTX** and **VirusTotal** are used to inspect:  
- IP addresses  
- Domains  
- File Hashes  
- URLs  

This process helps validate attacker activity and detect malicious intent.  

<br>

---
