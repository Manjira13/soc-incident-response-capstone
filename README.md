# Project Overview

This repository documents a simulated Security Operations Center (SOC) incident response investigation involving the exploitation of the Samba `usermap_script` vulnerability. The objective was to detect malicious SMB activity, investigate the attack, validate the exploitation, perform containment, and document the complete incident response lifecycle.

The attack was simulated using the Metasploit Framework against a vulnerable Samba host. Network traffic was monitored using Zeek, security events were analyzed in Kibana (ELK Stack), incident management was performed in TheHive, and containment was executed using CrowdSec by blocking the attacker's IP address.

Throughout the investigation, evidence was collected from multiple security tools to validate the attack, correlate events, and document the incident. A post-incident analysis was conducted using the 5 Whys methodology and a Fishbone (Ishikawa) diagram to identify the underlying causes and recommend security improvements.

This project demonstrates practical SOC Analyst skills including:

- Security monitoring and alert triage
- Network traffic analysis with Zeek
- Log analysis using Kibana (ELK Stack)
- Incident management with TheHive
- Attack validation using Metasploit
- Threat containment using CrowdSec
- Root Cause Analysis (RCA)
- Incident documentation and reporting
- MITRE ATT&CK mapping and security recommendations

> **Note:** This project was originally completed as the capstone project during my SOC Analyst internship and has been restructured into a standalone repository with improved documentation and organization for portfolio purposes.
