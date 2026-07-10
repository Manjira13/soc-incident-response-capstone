# Investigation Notes

## Task Information

| Field | Value                                              |
|------------------|-----------------------------------------|
| **Task Title**   | Samba Backdoor Detected                 |
| **Case ID**      | ~8294592                                |
| **Assignee**     | SOC Analyst                             |
| **Severity**     | Medium                                  |
| **TLP**          | Amber                                   |
| **Status**       | Completed                               |
| **MITRE ATT&CK** | T1210 - Exploitation of Remote Services |

---

## Incident Details

| Item                 | Value                               |
|----------------------|-------------------------------------|
| **Exploit**          | Metasploit `usermap_script`         |
| **Source IP**        | `192.168.1.39`                      |
| **Destination IP**   | `192.168.1.36`                      |
| **Protocol**         | SMB (Port 139)                      |
| **Zeek Notice**      | `Samba_Backdoor`                    |
| **Detection Source** | `/opt/zeek/logs/current/notice.log` |

---

## Actions Performed

- Verified Zeek detection of the Samba `usermap_script` exploit.
- Created an incident case in **TheHive** using an authorized administrator account.
- Added source and destination IP addresses as observables in TheHive.
- Initiated containment using **CrowdSec**.
- Blocked the attacker IP (`192.168.1.39`) using the CrowdSec Firewall Bouncer.
- Marked the containment task as **Completed** in TheHive.

---

## Investigation Findings

- Zeek successfully detected and logged multiple Samba backdoor exploitation attempts.
- TheHive case creation and observable management functioned correctly after using an account with the required `manageCase/create` permissions.
- CrowdSec containment was manually validated and confirmed to be active.
- Zeek alerts did not automatically populate TheHive; only the incident case was created.
- An attempt was made to calculate:
  - Mean Time to Detect (MTTD)
  - Mean Time to Respond (MTTR)
  - Dwell Time

### Challenges Encountered

The metrics could not be calculated due to the following issues:

- Missing or inconsistent timestamp fields required to determine attack start and detection times.
- The `attack_start_time` field was unavailable.
- Kibana runtime field scripts generated the following error:

```text
Cannot cast from [double] to [void]
```

- Kibana Lens visualizations could display event timelines but were unable to calculate the required security metrics.

---

## Root Cause Summary

The Samba exploit was successful due to:

- Exposed legacy SMB services.
- Incomplete system hardening.
- Lack of automated detection and enforcement workflows during the initial attack phase.

---

## Recommendations

- Disable legacy SMB scripts and unnecessary SMB services.
- Restrict SMB traffic to trusted hosts through network segmentation.
- Strengthen patch management and routine vulnerability scanning.
- Improve integration between **Zeek**, **TheHive**, and **CrowdSec** to automate detection, alerting, and containment.
- Explore alternative methods for collecting and calculating **MTTD**, **MTTR**, and **Dwell Time** for future incident reporting.
