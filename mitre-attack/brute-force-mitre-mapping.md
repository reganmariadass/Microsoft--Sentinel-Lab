# MITRE ATT&CK Mapping: Brute Force Login Attempts

## Use Case Overview

This document maps the brute-force login detection use case to the MITRE ATT&CK framework. The detection focuses on repeated failed Windows logon attempts, which may indicate password guessing, credential stuffing, or password spraying activity.

## Related Project Files

| File Type | Path |
|---|---|
| Detection Query | `detections/brute-force-login-detection.kql` |
| Incident Report | `incidents/incident-001-brute-force-login.md` |
| Response Playbook | `playbooks/brute-force-response-playbook.md` |

## ATT&CK Mapping

| Category | Details |
|---|---|
| Tactic | Credential Access |
| Technique ID | T1110 |
| Technique Name | Brute Force |
| Sub-techniques | T1110.001 Password Guessing, T1110.003 Password Spraying, T1110.004 Credential Stuffing |
| Platform | Windows, Azure AD / Entra ID, Enterprise Networks |
| Data Source | Windows Security Logs |
| Event ID | 4625 - Failed Logon |

## Technique Description

Brute-force activity involves repeated authentication attempts using guessed, stolen, reused, or systematically generated credentials.

In a SOC environment, this behaviour is commonly observed through repeated failed login attempts from the same source IP, repeated failures against one account, or authentication attempts across multiple accounts.

## Detection Logic Summary

The detection uses Windows Security Event ID `4625`, which represents failed logon attempts. The query groups events by:

- Account
- Source IP address
- Hostname

The alert triggers when the number of failed attempts reaches the defined threshold.

## Detection Behaviour

| Behaviour | SOC Interpretation |
|---|---|
| Multiple failed logins against one account | Possible password guessing |
| One IP targeting multiple accounts | Possible password spraying |
| Multiple external IPs targeting one account | Possible credential stuffing |
| Failed attempts followed by success | Possible account compromise |
| Privileged account targeted | Higher business risk |

## Relevant Data Sources

| Data Source | Purpose |
|---|---|
| Windows Security Events | Identify failed and successful logon activity |
| Azure AD / Entra ID Sign-in Logs | Review cloud authentication attempts |
| VPN Logs | Validate remote access attempts |
| Firewall Logs | Review source IP activity |
| Threat Intelligence Feeds | Check IP reputation |
| Endpoint Logs | Identify post-login suspicious behaviour |

## SOC Triage Priority

| Condition | Priority |
|---|---|
| Failed attempts only, no success | Medium |
| Failed attempts followed by successful login | High |
| Privileged account targeted | High |
| External suspicious IP involved | High |
| Multiple accounts targeted | High |
| Confirmed malicious IP reputation | High |

## Detection Gaps

This detection may not identify:

- Low-and-slow brute-force attempts below the threshold
- Distributed password spraying from multiple IP addresses
- Authentication attempts hidden behind legitimate VPN infrastructure
- Successful use of valid credentials without repeated failures
- Attempts where logging is incomplete or disabled

## Improvement Opportunities

Future improvements can include:

- Time-window based thresholding
- Geo-location enrichment
- IP reputation enrichment
- Detection for failed attempts followed by success
- Detection for one IP targeting multiple accounts
- Detection for one account targeted by multiple IPs
- Integration with Azure AD / Entra ID sign-in logs

## Defensive Recommendations

- Enforce MFA for all users
- Apply account lockout policies
- Monitor privileged accounts separately
- Review risky sign-in activity
- Block malicious IP addresses where appropriate
- Educate users on password hygiene
- Disable unused or stale accounts
- Monitor for successful logins after repeated failures

## Analyst Summary

This mapping helps SOC analysts understand the relationship between brute-force login activity, MITRE ATT&CK technique T1110, and the required detection, triage, and response workflow.
