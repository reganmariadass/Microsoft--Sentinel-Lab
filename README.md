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

| Use Case | Description | MITRE ATT&CK Mapping |
|---|---|---|
| Brute Force Login Attempts | Detects multiple failed login attempts against user accounts | T1110 - Brute Force |
| Disabled Account Sign-in Attempts | Detects authentication attempts against disabled accounts | T1078 - Valid Accounts |
| Suspicious PowerShell Execution | Detects potentially malicious PowerShell command usage | T1059.001 - PowerShell |
| New Admin Account Created | Detects creation of new privileged accounts | T1136 - Create Account |
| Impossible Travel Sign-in | Detects suspicious logins from distant locations within a short period | T1078 - Valid Accounts |

## Repository Structure

```text
detections/       Microsoft Sentinel KQL detection queries
incidents/        SOC analyst investigation reports
mitre-attack/     MITRE ATT&CK mapping documentation
sample-logs/      Sample Windows and Azure log data
playbooks/        Incident response playbooks
screenshots/      Lab screenshots and evidence
docs/             Supporting documentation
