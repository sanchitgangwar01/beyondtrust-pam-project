# 03. Smart Rules & Smart Groups

Smart Rules automatically place assets/accounts into Smart Groups so policies apply consistently as new items are onboarded.

## Naming Convention
`SR-<Type>-<Tier>-<Platform>-<Criteria>`  →  Group: `SG-<Type>-<Tier>-<Platform>`

## Smart Rule Design
| Smart Rule | Filter criteria (conceptual) | Smart Group | Used by |
|---|---|---|---|
| SR-Acct-T0-DomainAdmins | Account type = Directory; name matches `DA-*` | SG-Acct-T0-DomainAdmins | Policy P1 |
| SR-Acct-T1-WinLocalAdmin | Platform = Windows; account = Administrator | SG-Acct-T1-WinLocalAdmin | Policy P2 |
| SR-Acct-T1-LinuxRoot | Platform = Linux; account = root | SG-Acct-T1-LinuxRoot | Policy P2 |
| SR-Acct-T1-ServiceAccounts | Account name matches `svc_*` | SG-Acct-T1-Service | Policy P3 |
| SR-Acct-T1-SQLPriv | Asset type = Database; account = sa | SG-Acct-T1-SQL | Policy P4 |
| SR-Acct-T2-NetworkAdmin | Asset type = Network device | SG-Acct-T2-Network | Policy P5 |
| SR-Asset-Unowned | Owner attribute empty | SG-Asset-Unowned | Weekly cleanup report |
| SR-Acct-Stale | Password not changed > rotation window | SG-Acct-Stale | Alerting/report |

## Ownership & Access Mapping
| Smart Group | Account Owner | Requester groups | Approver |
|---|---|---|---|
| SG-Acct-T0-DomainAdmins | Head of Infrastructure | `PAM-T0-Admins` | Security Manager |
| SG-Acct-T1-WinLocalAdmin | Windows Team Lead | `PAM-WinOps` | Team Lead (auto for low-risk) |
| SG-Acct-T1-LinuxRoot | Linux Team Lead | `PAM-LinuxOps` | Team Lead |
| SG-Acct-T1-Service | App Owner | `PAM-AppOps` | App Owner + Security |
| SG-Acct-T1-SQL | DBA Lead | `PAM-DBA` | DBA Lead |
| SG-Acct-T2-Network | Network Lead | `PAM-NetOps` | Network Lead (change ticket) |

## Maintenance
- Review Smart Rules quarterly; test criteria before activation.
- `SG-Asset-Unowned` must be empty; anything in it is assigned an owner within 5 working days.
