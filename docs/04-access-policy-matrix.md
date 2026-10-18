# 04. Least-Privilege Access Policy Matrix

## Policy Definitions
| Policy | Applies to (Smart Group) | Access type | Max release | Approval | Session recording | Rotate | Ticket required |
|---|---|---|---|---|---|---|---|
| **P1: Tier 0** | SG-Acct-T0-DomainAdmins | RDP session only (no password reveal) | 60 min | Dual (Owner + Security) | Yes | After every use | Yes (CR/Incident) |
| **P2: Server admin** | SG-Acct-T1-WinLocalAdmin, SG-Acct-T1-LinuxRoot | RDP/SSH session; reveal only by exception | 120 min | Single (Team Lead); auto-approve in on-call window | Yes | After every use | Yes |
| **P3: Service account** | SG-Acct-T1-Service | Password reveal (exception) | 30 min | App Owner + Security | Audit log | After use + dependency check | Yes |
| **P4: Database** | SG-Acct-T1-SQL | Session only | 90 min | DBA Lead | Yes | After every use | Yes |
| **P5: Network** | SG-Acct-T2-Network | SSH session | 60 min | Network Lead | Yes | After every use | Change ticket |
| **P6: Break-glass** | Emergency accounts | Controlled reveal | 30 min | Dual + immediate alert | Yes | Immediately after | Post-incident |

## Role × Asset Tier Matrix
`A` = auto-approve, `1` = single approval, `2` = dual approval, `X` = denied

| Role | Tier 0 | Tier 1 Windows | Tier 1 Linux | Tier 1 DB | Tier 2 Network | Cloud |
|---|---|---|---|---|---|---|
| Helpdesk | X | X | X | X | X | X |
| Windows Admin | 2 | A / 1 | X | X | X | 1 |
| Linux Admin | X | X | A / 1 | X | X | 1 |
| DBA | X | X | X | 1 | X | X |
| Network Admin | X | X | X | X | 1 | X |
| Cloud Engineer | X | X | X | X | X | 1 |
| Security Analyst | Read-only audit | Read-only | Read-only | Read-only | Read-only | Read-only |
| Auditor | Logs/recordings read-only | same | same | same | same | same |

## Time-Bound Access Rules
- Default release: 60-120 min depending on tier; no standing access.
- Extensions: one extension max, requires fresh justification.
- Off-hours requests: require on-call confirmation.
- Emergency override: logged as exception (doc 05).

## Exception Handling
| Exception | Condition | Approval | Expiry | Review |
|---|---|---|---|---|
| Password reveal instead of session | Tool incompatible with proxy | Owner + Security | Single use | Monthly |
| Extended duration | Long maintenance window | Approver + ticket | Window end | After window |
| Temporary standing access | Project need | Security Manager | ≤ 14 days | At expiry |
