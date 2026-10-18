# 01. Architecture & Design Principles

## Components (Password Safe concepts)
| Component | Role in this design |
|---|---|
| **Managed System** | A target asset (server, DB, network device, directory) registered in the vault |
| **Managed Account** | A privileged account on a managed system whose password is vaulted and rotated |
| **Functional Account** | A service account Password Safe uses to connect to managed systems and change passwords |
| **Smart Rule** | Dynamic rule that filters assets/accounts and places them into Smart Groups |
| **Smart Group** | Result set used as the target for access policies and reporting |
| **Access Policy** | Defines who may request what, when, for how long, with which approval |
| **Session Proxy / Recording** | RDP/SSH sessions are brokered and recorded; user never sees the password |
| **Discovery Scan** | Finds accounts/assets not yet onboarded |

## Roles (separation of duties)
| Role | Responsibility | Must NOT |
|---|---|---|
| PAM Administrator | Configure platform, functional accounts, Smart Rules | Approve own requests |
| Account Owner | Owns business justification for account(s) | Change vault config |
| Requester (Engineer/Admin) | Requests access via policy | Access vault without policy |
| Approver | Approves high-risk requests | Be the requester |
| Auditor | Read-only access to logs/recordings | Modify anything |

## Design Principles
1. **Least privilege**: access only to the assets/accounts needed for the task.
2. **Just-in-time, time-bound**: default short release windows; extension needs justification.
3. **No standing knowledge of passwords**: prefer session proxy over password reveal.
4. **Rotate after use**: especially Tier 0/1.
5. **Everything is owned**: no account onboarded without an owner and justification.
6. **Everything is logged**: request, approval, session, check-in, rotation.
7. **Break-glass is exceptional**: separately controlled, alerted, reviewed.
