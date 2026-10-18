# 08. Troubleshooting Notes

## A. Access / Session Issues
| Symptom | Likely cause | Checks | Fix |
|---|---|---|---|
| User cannot see the asset/account | Not in requester group or Smart Group scope | Group membership; Smart Rule filter; policy assignment | Correct group/rule; re-evaluate policy |
| Request stuck pending | Approver not mapped / notification issue | Approver group; notification config | Fix mapping; notify approver manually |
| Session launch fails | Proxy/network issue, port blocked, wrong platform | Connectivity to target; firewall; RDP/SSH enabled | Open port; correct platform/config |
| Access denied outside hours | Time-window restriction in policy | Policy schedule | Request via on-call exception |
| Login works but user lacks rights | Account lacks required privilege on target | Local group membership on target | Fix target account, not the policy |

## B. Credential Rotation Issues
| Symptom | Likely cause | Checks | Fix |
|---|---|---|---|
| Rotation fails: auth error | Functional account locked or password changed | Functional account status | Reset/unlock; update in vault |
| Rotation fails: network/timeout | Firewall, DNS, target offline | Ping/port test; DNS | Fix path; retry |
| Rotation fails: complexity rejected | Vault policy differs from target policy | Compare policies | Align password policy |
| Service breaks after rotation | Service/task/app uses old password | Dependency list from onboarding | Update dependent configs; consider managed service accounts |
| Vault and target out of sync | Password changed manually on target | Last-changed timestamps | Reset via functional account; block manual changes |

## C. Session Recording / Audit Issues
| Symptom | Likely cause | Checks | Fix |
|---|---|---|---|
| Session not recorded | Direct connection bypassed proxy; policy not set to record | Policy recording flag; connection path | Enforce proxy-only; correct policy |
| Recording unplayable/missing | Storage full or retention purge | Storage capacity; retention | Expand storage; adjust retention |
| Logs not in SIEM | Forwarding misconfigured | Syslog/connector status | Fix forwarding; backfill |
| Cannot map session to person | Shared login to vault | Authentication method | Enforce named accounts + MFA |

## D. Discovery / Onboarding Issues
| Symptom | Likely cause | Fix |
|---|---|---|
| Discovery finds nothing | Scan credentials/permissions or network scope wrong | Verify scan account rights and target ranges |
| Duplicate accounts | Same account found via multiple scans | De-duplicate by system + username before onboarding |
| Account in vault but no owner | Skipped checklist | Weekly `SG-Asset-Unowned` review |

## Escalation Template
```
Issue:
Affected asset/account:
Impact:
Steps already taken:
Logs/screenshots attached:
Requested action:
```
