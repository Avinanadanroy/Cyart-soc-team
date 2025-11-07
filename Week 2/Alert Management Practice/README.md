# Alert Management Practice  
CYART  
inquiry@cyart.io  
www.cyart.io  

<br>

## 1. Alert Classification System  

An alert classification framework that categorizes alerts by priority and maps them to MITRE ATT&CK techniques.  
A Google Sheets table was created with columns for **Alert ID, Type, Priority, and MITRE Tactic.**

<br>

### Alert Table

| Alert ID | Type                                | Priority | MITRE Tactic |
|----------|-------------------------------------|----------|--------------|
| 001      | Log4Shell Exploit                   | Critical | T1190        |
| 002      | Ransomware                          | Critical | T1486        |
| 003      | Phishing                            | High     | T1110        |
| 004      | Port Scan                           | Low      | T1046        |
| 005      | Remote System Discovery             | Low      | T1018        |
| 006      | Encryption of data for impact       | Medium   | T1486        |
| 007      | Command and Scripting Interpreter   | High     | T1059        |
| 008      | Brute-Force SSH                     | Medium   | T1130        |

<br>

### 1.1 Testing Mock Alert  

A mock alert example (e.g., **“Phishing Email: Suspicious Link”**) is analyzed to determine priority and MITRE mapping.  
The new alert is updated in the table.

| Alert ID | Type      | Priority | MITRE Tactic |
|----------|-----------|----------|--------------|
| 009      | Phishing  | High     | T1110        |

<br>

---

## 2. Prioritize Alerts  

Alert prioritization involves ranking threats by business or financial impact.  
Critical alerts are escalated to **Tier-2**.

To simulate severity, CVSS scoring was performed in Google Sheets.  
Example:  
- **Log4Shell CVSS: 9.8 → Critical**

<br>

### CVSS Scoring Table  

| CVSS Score | Priority Level | Action                             |
|------------|----------------|------------------------------------|
| 9.0–10.0   | Critical       | Immediate action required          |
| 7.0–8.9    | High           | Containment required quickly       |
| 4.0–6.9    | Medium         | Investigate → Schedule fix         |
| 0.0–3.9    | Low            | Triage when time permits           |

<br>

### CVSS Formula  


Example calculation for **Log4Shell Exploit**:  
- Asset = Production DB → 3  
- Exploit Likelihood = Public POC → 2.8  
- Business Impact = 4  
- **Total = 3 + 2.8 + 4 = 9.8 → Critical**

<br>

### Prioritized Alert Scorecard  

| Alert ID | Type                                | Priority | MITRE Tactic | CVSS score |
|----------|-------------------------------------|----------|--------------|------------|
| 001      | Log4Shell Exploit                   | Critical | T1190        | 9.8        |
| 002      | Ransomware                          | Critical | T1486        | 9.2        |
| 003      | Phishing                            | High     | T1110        | 8.9        |
| 004      | Command and Scripting Interpreter   | High     | T1059        | 8.2        |
| 005      | Brute-Force SSH                     | Medium   | T1130        | 6.5        |
| 006      | Encryption of data for impact       | Medium   | T1486        | 5.8        |
| 007      | Port Scan                           | Low      | T1046        | 0.1        |
| 008      | Remote System Discovery             | Low      | T1018        | 0.1        |

<br>

---

## 3. Dashboard Creation  

The main security dashboard displays **116 hits** on a timeline with a table listing alerts.  
Critical examples include:  
- **CRITICAL: Log4Shell (level 15)**  
- **Phishing Email (level 12)**  

Low-level noise example:  
- **Port Scan (level 3)**  

<br>

### Phishing Event

- Drilldown shows detailed logs, affected agent **(Avinandan)**  
- Confirmed **High-Level alert (level 12, rule 100001)**  

<br>

### Log4Shell Event

- Critical severity (level 15, rule 100800)  
- Full log data available  

<br>

### Port Scan Event

- `nmap-like-scan` identified  
- Low priority (level 3, rule 100801)  

<br>

### Visualization  

A pie chart was created to compare activity volume by rule level:

- Filter → `rule.level : (3 OR 15)`
- Results:  
  - Port Scan (level 3) → **98.93%**  
  - Log4Shell (level 15) → **1.07%**

<br>

---

## 4. Incident Ticket  

Incident ticket contains:  
- Title  
- Description  
- Priority  
- Assignee  

Ticketing documents the incident lifecycle and logs escalation to Tier-2 or higher when needed.  

<br>

---

## 5. Escalation Role-Play  

When a **critical incident** is detected, Tier-1 escalates to Tier-2 with a summary and IOCs.  

<br>

### Sample Escalation Email  

**Subject:**  
`[CRITICAL] EMERGENCY: Active Ransomware Incident on Server-X`

Tier 2 Team,

A critical ransomware incident has been identified on Server-X (172.23.0.107)
and requires immediate escalation.

Initial alert indicates a malicious executable crypto_locker.exe
with suspected attacker source IP: 172.23.0.107.

Action Taken:

Server-X isolated to contain encryption and prevent lateral spread

We require Tier-2 analysis → eradication → confirm backup integrity.
Incident ticket: TICKET-001 (TheHive)

Thanks,
Avinanadan Roy
Tier-1 SOC Analyst

**Body:**

