# 09. Audit Evidence & Reporting

| Control objective | Evidence to collect | Source | Frequency |
|---|---|---|---|
| All privileged accounts are managed | Managed account inventory vs. discovery report | Password Safe / discovery | Monthly |
| Access is authorized | Request + approval records with ticket ID | Request log | Monthly sample |
| Access is time-bound | Release start/end times | Request log | Monthly |
| Sessions are monitored | Session recordings, metadata | Session store | Sample weekly |
| Passwords rotate after use | Rotation history | Account audit trail | Monthly |
| Ownership is assigned | Owner field export; empty `SG-Asset-Unowned` | Smart Group report | Weekly |
| Periodic recertification | Signed owner recertifications | Recertification records | Quarterly |
| Role membership is accurate | Requester/approver group export | Directory | Quarterly |
| Break-glass is controlled | Alerts, incident record, rotation proof | Alerts / IR | Per use |

## Suggested KPIs
| KPI | Target |
|---|---|
| % privileged accounts vaulted | 100% of Tier 0/1 |
| % accounts with owner | 100% |
| Failed rotations unresolved > 24 h | 0 |
| Break-glass uses without incident | 0 |
| Recertification completed on time | ≥ 95% |
