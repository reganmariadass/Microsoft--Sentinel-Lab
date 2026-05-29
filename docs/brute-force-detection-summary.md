# Brute Force Login Detection Summary

## Overview

This document summarises the brute-force login detection use case developed as part of the Microsoft Sentinel SOC Detection Engineering Lab.

The use case focuses on identifying repeated failed Windows login attempts that may indicate brute-force attacks, password guessing, password spraying, credential stuffing, or misconfigured authentication activity.

## Detection Objective

The objective of this detection is to identify multiple failed login attempts from the same source IP address against the same user account and host.

This type of activity is commonly reviewed by SOC analysts to determine whether an attacker is attempting unauthorised access using guessed or stolen credentials.

## Related Files

| File Type | Path |
|---|---|
| Detection Query | `detections/brute-force-login-detection.kql` |
| Incident Report | `incidents/incident-001-brute-force-login.md` |
| Response Playbook | `playbooks/brute-force-response-playbook.md` |
| MITRE Mapping | `mitre-attack/brute-force-mitre-mapping.md` |
| Sample Logs | `sample-logs/windows-security-brute-force-sample.json` |

## Data Source

| Source | Details |
|---|---|
| Log Source | Windows Security Events |
| Event ID | 4625 - Failed Logon |
| Related Event ID | 4624 - Successful Logon |
| SIEM Platform | Microsoft Sentinel |
| Query Language | Kusto Query Language - KQL |

## MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name |
|---|---|---|
| Credential Access | T1110 | Brute Force |

## Detection Logic Summary

The KQL query filters Windows Security Events for failed login attempts using Event ID `4625`.

The query then groups events by:

- Account
- Source IP address
- Computer

If the number of failed attempts reaches the defined threshold, the activity is flagged as a possible brute-force login attempt.

## Why This Detection Matters

Brute-force login attempts are commonly seen in SOC environments and may indicate attempts to gain unauthorised access to user accounts, privileged accounts, endpoints, VPN services, or cloud applications.

Early detection helps reduce the risk of account compromise, lateral movement, and unauthorised access to sensitive systems.

## SOC Analyst Workflow

1. Review the alert details.
2. Identify the affected user account.
3. Check the source IP address.
4. Review failed login count.
5. Check for successful login after failed attempts.
6. Determine whether the source is internal or external.
7. Check whether the affected account is privileged.
8. Review related alerts.
9. Decide whether the alert is true positive or false positive.
10. Escalate if suspicious activity is confirmed.

## False Positive Possibilities

- User entered an incorrect password multiple times
- Password was recently changed
- Mobile device used old saved credentials
- VPN client retried authentication
- Service account password expired
- Scheduled task used stale credentials
- Mapped drive attempted login with old password

## High-Risk Indicators

- Failed logins followed by successful login
- Privileged account targeted
- External suspicious IP address involved
- Multiple users targeted from one IP
- Activity outside normal working hours
- Source IP linked to threat intelligence
- User confirms the activity was not legitimate

## Recommended Response

If suspicious activity is confirmed, the SOC analyst should:

- Reset the affected user password
- Revoke active sessions
- Enforce or verify MFA
- Block malicious source IP if appropriate
- Review endpoint activity
- Monitor for further authentication attempts
- Escalate to Tier 2 or Incident Response if compromise is suspected

## Skills Demonstrated

This use case demonstrates:

- KQL query writing
- Windows Event Log analysis
- Authentication monitoring
- SOC alert triage
- MITRE ATT&CK mapping
- Incident response documentation
- Detection engineering methodology
- Security operations reporting

## Analyst Conclusion

This brute-force detection use case provides a practical example of how SOC analysts can detect, investigate, and respond to suspicious authentication activity using Microsoft Sentinel-style detection logic and structured incident response documentation.
