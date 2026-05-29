# Incident 001: Brute Force Login Attempts

## Alert Summary

| Field | Details |
|---|---|
| Alert Name | Possible Brute Force Login Attempts |
| Severity | Medium |
| Detection File | `detections/brute-force-login-detection.kql` |
| Data Source | Windows Security Events |
| Event ID | 4625 - Failed Logon |
| MITRE ATT&CK | T1110 - Brute Force |
| Status | Investigation Required |

## Executive Summary

This incident report documents a potential brute-force login attempt detected through repeated Windows failed logon events.

The detection identifies multiple failed login attempts from the same source IP address targeting the same user account and endpoint. This behaviour may indicate password guessing, credential stuffing, misconfigured services, expired credentials, or repeated failed authentication by a legitimate user.

## Detection Logic

The KQL query searches Windows Security Event logs for Event ID `4625`, which represents failed logon attempts. It groups events by account, source IP address, and host, then triggers when five or more failed attempts are observed.

## Investigation Objectives

The objective of this investigation is to determine whether the failed login activity is:

- A true brute-force attack
- A credential stuffing attempt
- A misconfigured service or application
- A legitimate user entering incorrect credentials
- A stale password saved on a device or mapped drive

## Key Evidence to Collect

| Evidence | Purpose |
|---|---|
| Affected user account | Identify the targeted identity |
| Source IP address | Determine origin of activity |
| Destination host | Identify the affected endpoint |
| Failed attempt count | Measure attack volume |
| First and last attempt time | Build timeline |
| Successful login after failures | Identify potential compromise |
| MFA status | Validate account protection |
| IP reputation | Assess malicious infrastructure risk |

## Analyst Triage Steps

1. Confirm the affected user account.
2. Review the source IP address and determine whether it is internal or external.
3. Check whether the same IP targeted multiple accounts.
4. Check whether the same account was targeted by multiple IP addresses.
5. Search for successful login events after the failed attempts.
6. Review whether the affected account is privileged.
7. Confirm whether MFA is enabled for the user.
8. Contact the user if required to validate legitimate activity.
9. Review related alerts involving the same user, host, or IP.
10. Determine whether escalation is required.

## False Positive Scenarios

| Scenario | Explanation |
|---|---|
| User forgot password | Legitimate user repeatedly entered the wrong password |
| Password recently changed | Old credentials may still be saved on another device |
| Mobile email sync issue | Mobile device may repeatedly authenticate with stale credentials |
| Mapped network drive | Cached credentials may cause repeated failures |
| Service account issue | Expired service account password may generate repeated failures |
| VPN reconnect issue | VPN clients may retry authentication multiple times |

## True Positive Indicators

- External suspicious IP address involved
- Multiple user accounts targeted
- Privileged account targeted
- Failed attempts followed by successful login
- Login attempt from unusual country or region
- Same IP associated with threat intelligence indicators
- Activity observed outside normal working hours

## Response Actions

| Action | Purpose |
|---|---|
| Reset password | Protect potentially targeted account |
| Revoke active sessions | Remove possible attacker access |
| Enforce MFA | Reduce account takeover risk |
| Block malicious IP | Prevent further authentication attempts |
| Disable account temporarily | Contain suspected compromise |
| Escalate to Tier 2/Senior Analyst | Required for privileged or confirmed compromise cases |

## MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name |
|---|---|---|
| Credential Access | T1110 | Brute Force |

## Analyst Verdict

Pending investigation.

## Recommendation

Monitor for successful login activity following failed attempts, verify MFA status, review IP reputation, and escalate if the activity involves a privileged account, suspicious external IP, or successful authentication after repeated failures.
