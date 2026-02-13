# Wazuh-SOC-Lab
A hands-on SOC lab environment for threat detection, vulnerability management, and file integrity monitoring.

# SOC Automation & Threat Detection Lab (Wazuh SIEM)

## Project Objective
This lab demonstrates the deployment of a Security Operations Center (SOC) environment using Wazuh SIEM to monitor endpoint security, detect network-based attacks, and perform vulnerability management. 

### Prerequisites
* **SIEM:** Wazuh Manager & Dashboard (v4.14.3) on Kali Linux
* **Endpoint:** Windows 11 Enterprise Evaluation
* **Attack Station:** Kali Linux (Hydra, IP: 192.168.1.5)

---

## 1. Vulnerability Management
Upon deploying the Wazuh agent, I initiated an automated vulnerability scan. The dashboard identified **2 Critical** and **195 High-severity** vulnerabilities, allowing for prioritized remediation based on the global CVE database.

<img src="https://github.com/user-attachments/assets/2971931d-9234-43a5-ad2e-7ec6c491bdcc" width="800">

## 2. RDP Brute Force Detection
I simulated a dictionary-based brute force attack against the Windows endpoint using **Hydra**. 

> **Forensic Findings:**
> * **Attacker IP:** `192.168.1.5`
> * **Target Account:** `Victim-User`
> * **Detection Rule:** Rule 60122 (Logon Failure)

<img src="https://github.com/user-attachments/assets/e3c8f016-d100-4c51-bf68-1151485e3d6d" width="800">
<img src="https://github.com/user-attachments/assets/c7db259a-ba24-402c-a68b-cb10dca8c431" width="800">

## 3. Real-Time File Integrity Monitoring (FIM)
I manually configured the Wazuh Agent's `ossec.conf` file to monitor the `C:\Users\Victim-User\Desktop` directory in real-time.

<img src="https://github.com/user-attachments/assets/0fffdcb0-91f2-4e8a-b8cb-0ea8ddabbc63" width="800">

### Incident Simulation:
By creating, modifying, and deleting files on the Desktop, I verified the agent's ability to ship forensic data to the SIEM:
* **Rule 554:** File added to the system.
* **Rule 550:** Integrity checksum changed (Content modification).
* **Rule 553:** File deleted.

<img src="https://github.com/user-attachments/assets/2a3c3f6f-f86c-472b-985e-3c6d08b3092f" width="800">
<img src="https://github.com/user-attachments/assets/52bf4a73-8c41-4816-af63-2ec1fdd93578" width="800">

---

## 4. Conclusion
This lab successfully demonstrates the "Detect, Analyze, and Respond" lifecycle. By configuring granular monitoring and analyzing security telemetry, I established end-to-end visibility over an endpoint's security posture.

## Disclaimer
All activities demonstrated in this laboratory were performed within a controlled, isolated virtual environment. These experiments were conducted for educational purposes to understand defensive security operations and threat detection methodologies.
