# Root Cause Analysis (RCA)

## Post-Incident Analysis – 5 Whys

**Incident:** Samba `usermap_script` exploit attempt detected on host `192.168.1.36`.

### 1. Why did the exploit succeed in reaching the host?

The target host had SMB services exposed without proper network segmentation or access restrictions.

---

### 2. Why were SMB services exposed without restrictions?

Legacy Samba scripts were enabled, and network policies did not restrict SMB traffic to trusted hosts.

---

### 3. Why were legacy scripts enabled and traffic unrestricted?

System hardening and patch management processes were incomplete, leaving unnecessary services active.

---

### 4. Why were patch management and hardening processes incomplete?

There was no automated vulnerability monitoring or enforcement mechanism in place for SMB services.

---

### 5. Why was there no automated monitoring and enforcement?

The security environment had not yet fully integrated network monitoring (**Zeek**), incident management (**TheHive**), and automated containment (**CrowdSec**) into a unified SOC workflow.

---

# Fishbone (Ishikawa) Analysis

The Fishbone (Ishikawa) diagram identified multiple contributing factors that enabled the exploit, including:

- Legacy SMB functionality remaining enabled
- Incomplete system hardening
- Limited network segmentation
- Lack of automated detection and response workflows
- Insufficient vulnerability monitoring

> **Note:** A visual Fishbone diagram is included in the `screenshots/` directory of this repository.

---

# Root Cause Summary

The Samba backdoor exploit was made possible due to exposed legacy SMB functionality, incomplete system hardening, and the absence of integrated monitoring and automated containment mechanisms. Although the attack was detected and contained successfully, the incident highlighted opportunities to improve preventive security controls and SOC automation.

---

# Recommendations

- Disable unnecessary legacy Samba scripts and services.
- Implement network segmentation to restrict SMB access to trusted hosts.
- Automate patch management and routine vulnerability scanning.
- Integrate **Zeek**, **TheHive**, and **CrowdSec** to provide automated detection, alerting, and containment.
- Regularly validate incident response playbooks through simulated attack scenarios and tabletop exercises.
