# Microsoft Sentinel SOC Detection Engineering Lab

## Overview

This repository is a hands-on SOC Analyst portfolio project focused on Microsoft Sentinel detection engineering, KQL query development, alert triage, MITRE ATT&CK mapping, and incident response documentation.

The objective of this lab is to simulate real-world SOC workflows by analysing security events, developing detection logic, documenting investigation steps, and creating response playbooks for common security incidents.

## Project Objectives

- Develop practical Microsoft Sentinel KQL detection queries
- Analyse Windows Security and Azure AD/Entra ID logs
- Create SOC-style incident investigation reports
- Map suspicious activity to MITRE ATT&CK techniques
- Document response playbooks for common alerts
- Demonstrate alert triage, evidence collection, and escalation logic
- Build a professional cybersecurity portfolio for SOC Analyst roles

## Tools and Technologies

- Microsoft Sentinel
- Kusto Query Language - KQL
- Windows Security Event Logs
- Azure AD / Microsoft Entra ID Sign-in Logs
- MITRE ATT&CK Framework
- Incident Response Documentation
- SIEM Alert Triage
- Security Monitoring

## Detection Use Cases

| Use Case | Description | MITRE ATT&CK | Project Files |
|---|---|---|---|
| Brute Force Login Attempts | Detects repeated failed login attempts against user accounts using Windows Security Event ID 4625 | T1110 - Brute Force | [Detection](detections/brute-force-login-detection.kql) · [Incident Report](incidents/incident-001-brute-force-login.md) · [Playbook](playbooks/brute-force-response-playbook.md) · [MITRE Mapping](mitre-attack/brute-force-mitre-mapping.md) · [Summary](docs/brute-force-detection-summary.md) |
| Disabled Account Sign-in Attempts | Detects authentication attempts against disabled accounts | T1078 - Valid Accounts | Coming soon |
| Suspicious PowerShell Execution | Detects potentially malicious PowerShell command usage | T1059.001 - PowerShell | Coming soon |
| New Admin Account Created | Detects creation of new privileged accounts | T1136 - Create Account | Coming soon |
| Impossible Travel Sign-in | Detects suspicious logins from distant locations within a short period | T1078 - Valid Accounts | Coming soon |
## Repository Structure

##SKILLS DEMMONSTRATED
## Completed Use Case: Brute Force Login Attempts

The first completed detection package focuses on brute-force login activity using Windows Security Event ID `4625`.

This use case includes:

- Microsoft Sentinel KQL detection logic
- SOC incident investigation report
- MITRE ATT&CK mapping
- Incident response playbook
- Sample Windows Security log data
- Documentation summary

### Key SOC Concepts Demonstrated

- Authentication monitoring
- Failed logon analysis
- Source IP investigation
- True positive and false positive assessment
- Credential Access detection
- Alert escalation logic

```text
detections/       Microsoft Sentinel KQL detection queries

incidents/        SOC analyst investigation reports
mitre-attack/     MITRE ATT&CK mapping documentation
sample-logs/      Sample Windows and Azure log data
playbooks/        Incident response playbooks
screenshots/      Lab screenshots and evidence
docs/             Supporting documentation


