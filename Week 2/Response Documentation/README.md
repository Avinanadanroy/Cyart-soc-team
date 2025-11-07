# Response Documentation  
CYART  
inquiry@cyart.io  
www.cyart.io  

<br>

## 1. Investigation Steps  

The investigation procedure follows the incident response lifecycle, emphasizing defense and recovery from attacks.  
The process includes:  
- Preparation for possible incidents  
- Detection and analysis of threats  
- Restoration of affected systems  

<br>

### Log Actions for Mock Incident  

| Time Stamp        | Action |
|-------------------|--------|
| 2025-11-05 16:29:05 | Isolated affected user’s device from the network. |
| 2025-11-05 16:46:20 | Suspicious login session terminated on the mail server. |
| 2025-11-05 17:07:10 | Collected memory dump from the isolated device for forensic analysis using Velociraptor. |
| 2025-11-05 17:35:32 | No mail forwarding rules were created on the compromised user account. |

<br>

## 2. Phishing Checklist  

A phishing response checklist was documented in Google Docs to minimize human error and ensure consistent, repeatable workflow for handling critical tasks.

<br>

### Initial Assessment  
- Confirm email headers.  
- Check link reputation via VirusTotal / URLScan.  
- Check file hash via VirusTotal.  
- Identify affected users.  

<br>

### Containment & Eradication  
- Force password reset for compromised users.  
- Block malicious IP at firewall.  
- Delete malicious emails from inboxes.  

<br>

### Post-Incident  
- Notify affected users and provide security awareness.  
- Complete an Incident Response Report.  

<br>

## 3. Post-Mortem  

A post-incident review evaluates a real or staged security event to determine root cause and measure response effectiveness.  

<br>

### Simulated Event  
A phishing attack led to limited data exposure because the affected system was not isolated promptly.  

<br>

### Lessons Learned  
Delayed endpoint isolation enabled unauthorized access to sensitive data.  
This highlighted the need to verify network-segmentation controls.  

A key improvement includes enabling auto
