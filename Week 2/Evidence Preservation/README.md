# Evidence Preservation  
CYART  
inquiry@cyart.io  
www.cyart.io  

<br>

## 1. Objective  

• This report contains the details of tasks including **Volatile Data Collection** and **Evidence Collection**.  
The goal of this task is to:  
• Capture volatile system information and active network connections from a Windows virtual machine  
• Acquire a memory dump to preserve evidence  
• Generate a hash value to verify file integrity  

<br>

## 2. Introduction  

This task includes collecting evidence from different sources and learning how to:  
- Create a hash file using `SHA256sum`  
- Practice chain-of-custody  

<br>

## 3. Tools & Setup  

• Velociraptor  
• FTK Imager  

<br>

## 4. Evidence Preservation  

Evidence preservation refers to the systematic process of creating forensic copies and gathering relevant information in a manner that prevents unauthorized modification.  
This step is essential in incident response and digital forensics, ensuring integrity of data for future investigation and analysis.  

<br>

### 4.1 Volatile Data Collection  

Volatile data collection was completed using **Velociraptor** to obtain network connections:  

SELECT * FROM nestat

from a Windows VM.  

Velociraptor client and interface output were captured.  

The output displays network statistics including:  
- Protocols in use  
- Active connections  

<br>

### 4.2 Evidence Collection  

Using **Velociraptor**, a memory dump was collected:  

SELECT * FROM Artifacts.Windows.Memory.Acquisition


The memory dump was hashed using `sha256sum`.  

A SHA1 hash was generated as:  

3b7f3c6e4a5d911b2e4f89dc1dd0c1b7c8b4b9f1f23d8e2e1a6c4e782b92f4d3


<br>

### Evidence Log Table  

| Item         | Description | Collected By | Date       | Hash Value |
|--------------|-------------|--------------|------------|-----------|
| Memory Dump  | Server-X Dump | SOC Analyst | 2025-11-07 | 3b7f3c6e4a5d911b2e4f89dc1dd0c1b7c8b4b9f1f23d8e2e1a6c4e782b92f4d3 |

<br>

---

CYART  
inquiry@cyart.io  
www.cyart.io  
