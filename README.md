# Wazuh-SOC-Lab
A hands-on SOC lab environment for threat detection, vulnerability management, and file integrity monitoring.
# SOC Automation & Threat Detection Lab (Wazuh SIEM)

## Project Objective
This lab demonstrates the deployment of a Security Operations Center (SOC) environment using Wazuh SIEM to monitor endpoint security, detect network-based attacks, and perform vulnerability management. The environment was built on a private virtual network to simulate real-world SOC workflows.

### Environment & Tools
- **SIEM:** Wazuh Manager & Dashboard (Kali Linux)
- **Endpoint:** Windows 11 Enterprise (Monitored via Wazuh Agent)
- **Attack Station:** Kali Linux (Hydra, IP: 192.168.1.5)
- **Monitoring:** File Integrity Monitoring (FIM), Vulnerability Detection, RDP Brute Force Detection

---

## 1. Vulnerability Management
Upon deploying the Wazuh agent, I initiated an automated vulnerability scan. The dashboard identified **2 Critical** and **195 High-severity** vulnerabilities, allowing for prioritized remediation based on the global CVE database.

![Vulnerability Dashboard](./vulnerability_scan.png)

## 2. RDP Brute Force Detection
I simulated a dictionary-based brute force attack against the Windows endpoint using **Hydra**. 
- **Detection:** Wazuh triggered Rule 60122 (Logon Failure) with a significant spike of 584 hits in minutes.
- **Forensics:** Deep-dive analysis identified the attacker's source IP (`192.168.1.5`) and the targeted account (`Victim-User`).

![Brute Force Spike](./brute_force_alerts.png)
![Attacker Metadata](./attacker_telemetry.png)

## 3. Real-Time File Integrity Monitoring (FIM)
I manually configured the Wazuh Agent's `ossec.conf` file to monitor a specific high-value directory (User Desktop) in real-time.

![Configuration Snippet](./ossec_config.jpeg)

### Incident Simulation:
By creating, modifying, and deleting files on the Desktop, I verified the agent's ability to ship forensic data to the SIEM.
- **Rule 554:** File added to the system.
- **Rule 550:** Integrity checksum changed (Content modification).
- **Rule 553:** File deleted.

![FIM Lifecycle](./fim_event_log.png)
![FIM Dashboard](./fim_dashboard.png)

## 4. Conclusion
This lab successfully demonstrates the "Detect, Analyze, and Respond" lifecycle. By configuring granular monitoring and analyzing security telemetry, I established end-to-end visibility over an endpoint's security posture.

<img width="1920" height="892" alt="fim_dashboard.png" src="https://github.com/user-attachments/assets/52bf4a73-8c41-4816-af63-2ec1fdd93578" />
<img width="1920" height="892" alt="fim_event_log.png" src="https://github.com/user-attachments/assets/2a3c3f6f-f86c-472b-985e-3c6d08b3092f" />
![ossec config.jpeg](https://github.com/user-attachments/assets/0fffdcb0-91f2-4e8a-b8cb-0ea8ddabbc63)
<img width="1920" height="892" alt="attacker_telemetry.png" src="https://github.com/user-attachments/assets/c7db259a-ba24-402c-a68b-cb10dca8c431" />
<img width="1920" height="892" alt="brute_force_alerts.png" src="https://github.com/user-attachments/assets/e3c8f016-d100-4c51-bf68-1151485e3d6d" />
<img width="1920" height="892" alt="vulnerability_scan.png" src="https://github.com/user-attachments/assets/2971931d-9234-43a5-ad2e-7ec6c491bdcc" />
