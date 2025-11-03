# Phishing-Investigation-Greenholt-PLC-Email-Analysis-TryHackMe-SOC-Simulation-
The scenario is only a simulation and does not contain any real company or individual data. The simulation is provided by TryHackMe.com meant for educational training purposes of real-world incidents.

**Author:** Blake Anderson  
**Platform:** TryHackMe.com  
**Tools Used:** VirusTotal, SPF Surveyor, dmarcian.com, Hashing Utilities, ServiceNow  

---

## Scenario Overview
This simulation replicates a real-world **phishing investigation** performed by a SOC analyst.  
A **Sales Executive at Greenholt PLC** reported an unexpected email from a known customer that included a suspicious attachment and unusual greeting (“Good day”).  
The user escalated the email to the **SOC team** for analysis.

---

## Incident Description

**Alert:** Possible phishing email with attachment  
**Sender Domain:** `mutawamarine.com`  
**Victim:** Sales Executive, Greenholt PLC  
**Email Indicators:**  
- Unfamiliar tone and greeting  
- Unexpected attachment  
- Unrequested transfer of funds  

The goal was to determine if the email was **legitimate or malicious** and identify any indicators of compromise.

---

## Investigation Steps

1. **Initial Triage**
   - Advised the employee **not to click or interact** with the email until analysis was complete.
   - Opened the email safely within an isolated analysis environment (VM).

2. **Header Analysis**
   - Examined the **email headers** to identify the originating IP address being 192.11.71.157.
   - Used `Ctrl + F` to search for “Received” fields and isolate the true source IP.

3. **Threat Intelligence Lookups**
   - Queried the sender IP on **VirusTotal** for prior malicious activity — results were inconclusive.  
   - Checked **SPF records** using **SPF Surveyor**.  
   - Queried **DMARC records** for `mutawamarine.com` using **dmarcian.com**.  
   - Findings showed a suspicious DMARC configuration suggesting possible domain spoofing.

4. **Attachment Analysis**
   - Saved the attachment to the virtual machine for sandboxed analysis.  
   - Used terminal command to compute the **SHA256 hash**:
     ```bash
     sha256sum SWT_#09674321___PDF__.CAB
     ```
   - Queried the hash on **VirusTotal** — confirmed positive detection linked to known phishing malware.

---

## Findings

- **Classification:** Confirmed *Spear-Phishing Attempt*  
- **Target:** Single high-value employee (Sales Executive)  
- **IOC:** Sender domain `mutawamarine.com` (malicious)  
- **Indicators:**  
  - Suspicious attachment  
  - Mismatched domain records  
  - Abnormal greeting and financial request  

---

## Actions Taken

- Documented all investigation steps, timestamps, and findings in **ServiceNow**.  
- **Escalated** the case to the internal threat response team for deeper review.  
- **Contacted the affected user:**
  - Confirmed the phishing attempt.
  - Assisted in **password reset** to prevent potential account compromise.
  - Updated **firewall and endpoint filters** to block the malicious sender and domain.
  - Notified user of possible follow-up by the internal alert team.

---

## Outcome

The analysis confirmed the email was a **targeted spear-phishing attack** attempting to compromise a single employee via malicious attachment.  
The incident was fully contained through password resets, domain blocking, and user communication.

---

## Skills Demonstrated

- Email header and domain analysis  
- SPF/DMARC record validation  
- Malware hash lookup and verification  
- Safe environment handling and sandboxing  
- Documentation and escalation procedures  
- Communication with affected users  

---

##  Screenshots

<img width="732" height="210" alt="image" src="https://github.com/user-attachments/assets/7a0c451d-5f45-42f8-ab9b-69935a3a2928" />
<img width="694" height="61" alt="image" src="https://github.com/user-attachments/assets/16e099cf-b955-4255-8cfb-437928b7c3e2" />
<img width="676" height="167" alt="image" src="https://github.com/user-attachments/assets/e93ab288-71b4-4c53-b070-bfdb3f6e7568" />
<img width="390" height="405" alt="image" src="https://github.com/user-attachments/assets/578e97dd-6f0b-49f5-9a22-8c07dc73a2d5" />
<img width="685" height="127" alt="image" src="https://github.com/user-attachments/assets/7bf40d58-3c0b-47f2-8832-b343cd35317b" />
<img width="668" height="503" alt="image" src="https://github.com/user-attachments/assets/24024614-ce8b-49f1-a08d-72ffa4346dbf" />

---

## 🔗 Reference

> **TryHackMe:** [https://tryhackme.com](https://tryhackme.com)  
> **Scenario:** Phishing Investigation (Greenholt PLC)
