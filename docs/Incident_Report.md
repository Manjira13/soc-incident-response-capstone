# Incident Report

## Executive Summary

On **September 12, 2025**, a potential **Samba backdoor exploit** targeting **192.168.1.36** was detected within the lab environment. The attack leveraged the **Metasploit `usermap_script` module** and was identified through **Zeek** network monitoring, with supporting evidence available in **Wazuh** logs.

Immediate containment actions were initiated using **CrowdSec**, preventing further compromise. No critical data exfiltration or lateral movement was observed, and the incident was successfully contained within minutes of detection.

---

## Timeline of Events

| Time      | Event                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------|
| **16:47** | Zeek detected unusual SMB traffic from **192.168.1.39** to **192.168.1.36**.                       |
| **16:48** | Metasploit exploitation attempt successfully executed in the lab environment.                      |
| **16:49** | Zeek generated a custom **`Samba_Backdoor`** notice, which was ingested into Kibana.               |
| **16:51** | A case was created in **TheHive**, observables were added, and the containment task was initiated. |
| **17:30** | CrowdSec Firewall Bouncer blocked the malicious IP address.                                        |
| **17:32** | Incident marked as contained. No lateral movement was detected.                                    |

---

## Root Cause Analysis (RCA)

The incident originated from an external test host exploiting the **Samba `usermap_script` vulnerability**. The attack succeeded because legacy SMB functionality was exposed on the target system.

Although the exploit was detected through Zeek's custom detection logic, the absence of continuous SMB vulnerability monitoring and automated response workflows delayed immediate enforcement until the custom alert was generated.

---

## Recommendations

- **Patch Management**
  - Apply the latest Samba security updates.
  - Disable legacy Samba scripts and unused services whenever possible.

- **Network Segmentation**
  - Restrict SMB access to authorized hosts only.
  - Limit exposure of SMB services across network segments.

- **Automated Containment**
  - Enhance integration between **Zeek**, **TheHive**, and **CrowdSec** to enable real-time detection and automated response.

- **Monitoring & Metrics**
  - Implement dashboards to track:
    - Mean Time to Detect (MTTD)
    - Mean Time to Respond (MTTR)
    - Dwell Time
  - Improve timestamp collection for accurate security metrics.

- **Training & Playbooks**
  - Maintain and regularly update incident response playbooks for known SMB exploitation techniques.
  - Conduct periodic validation exercises to ensure response procedures remain effective.
