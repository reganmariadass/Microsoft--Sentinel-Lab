# Brute Force Login Response Playbook

## Purpose

This playbook provides a structured response process for SOC analysts investigating brute-force login attempts detected through Windows Security Event logs or Microsoft Sentinel alerts.

The objective is to determine whether the alert represents malicious authentication activity, misconfiguration, stale credentials, or legitimate user error.

## Trigger Condition

This playbook should be used when an alert detects:

- Multiple failed login attempts against a user account
- Multiple failed login attempts from the same source IP address
- Failed login attempts followed by a successful login
- Failed authentication activity involving privileged accounts
- Repeated authentication failures from unusual locations or suspicious IP addresses

## Related Detection

| Field | Details |
|---|---|
| Detection Name | Brute Force Login Attempts |
| Detection File | `detections/brute-force-login-detection.kql` |
| Incident Report | `incidents/incident-001-brute-force-login.md` |
| Data Source | Windows Security Events |
| Event ID | 4625 - Failed Logon |
| MITRE ATT&CK | T1110 - Brute Force |

## Initial Triage Steps

1. Identify the affected user account.
2. Identify the source IP address.
3. Identify the destination host.
4. Count the number of failed login attempts.
5. Review the first and last observed timestamps.
6. Check whether the login attempts were followed by a successful login.
7. Determine whether the account is privileged.
8. Confirm whether MFA is enabled.
9. Review whether similar activity exists for other users or hosts.
10. Check whether the source IP is internal, external, VPN, or known business infrastructure.

## Investigation Questions

| Question | Why It Matters |
|---|---|
| Is the source IP internal or external? | Helps determine whether the activity may come from inside or outside the organisation |
| Is the account privileged? | Privileged accounts increase business risk |
| Did any login succeed after the failures? | May indicate successful compromise |
| Are multiple accounts targeted? | Could indicate credential stuffing or password spraying |
| Is MFA enabled? | MFA reduces account takeover likelihood |
| Is the activity outside normal working hours? | May indicate suspicious behaviour |
| Has the user changed password recently? | Could explain stale credential failures |
| Is the source IP known malicious? | Supports true positive assessment |

## Evidence to Collect

- Alert timestamp
- Affected username
- Source IP address
- Destination hostname
- Number of failed attempts
- Logon type
- Successful logon events after failures
- MFA status
- Account privilege level
- User location and expected working pattern
- IP reputation result
- Related alerts involving the same account, host, or IP

## False Positive Checks

Common benign causes include:

- User repeatedly entering the wrong password
- Password changed recently but old credentials remain cached
- Mobile device mail client using stale credentials
- VPN authentication retry loop
- Service account password expired
- Mapped drive using old credentials
- Scheduled task using outdated credentials

## True Positive Indicators

Treat the incident as higher risk if any of the following are observed:

- Failed attempts followed by successful authentication
- Privileged account targeted
- Multiple accounts targeted from one IP
- One account targeted by multiple external IPs
- Source IP has poor threat intelligence reputation
- Sign-in attempt from unusual country or region
- Activity occurs outside normal user behaviour
- Additional alerts are linked to the same user or host

## Containment Actions

| Action | When to Use |
|---|---|
| Force password reset | When account compromise is suspected |
| Revoke active sessions | When successful login occurred after failures |
| Temporarily disable account | When high-risk compromise is suspected |
| Block source IP | When malicious external source is confirmed |
| Enforce MFA | When account lacks strong authentication |
| Escalate to Tier 2 | When privileged account or confirmed compromise is involved |

## Escalation Criteria

Escalate the incident if:

- A successful login occurred after repeated failures
- The affected account is privileged
- The same IP targeted multiple users
- The activity is linked to known malicious infrastructure
- The user confirms the activity was not legitimate
- Lateral movement or endpoint compromise indicators are observed

## Recovery Actions

1. Confirm password reset completion.
2. Confirm MFA status.
3. Review account sign-in history.
4. Review endpoint activity for suspicious process execution.
5. Monitor account for repeat authentication failures.
6. Validate that malicious IP blocking has been applied, if required.
7. Document final findings and close or escalate the incident.

## Final Documentation Checklist

- Alert name recorded
- User account identified
- Source IP reviewed
- Host reviewed
- Timeline created
- False positive checks completed
- MITRE ATT&CK mapping included
- Containment action documented
- Final analyst verdict added
- Escalation decision documented

## Analyst Notes

This playbook supports consistent SOC triage and helps analysts distinguish between brute-force attacks, password spraying, stale credentials, and benign authentication failures.
