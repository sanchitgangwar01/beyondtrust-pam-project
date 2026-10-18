# 07. Operational SOP: Password Safe

| Field | Value |
|---|---|
| Version | 1.0 |
| Owner | PAM Administrator |
| Review cycle | Annually |

## 1. Request & Use Privileged Access
1. Raise/identify ticket.
2. Log in to Password Safe with MFA.
3. Select asset/account, enter duration and reason (include ticket ID).
4. Wait for approval (if required).
5. Launch the proxied session; do not copy or store credentials.
6. Complete work and **check in** promptly.
7. Confirm rotation occurred (PAM admin spot-check).

## 2. Onboard a New Account
Follow the [Onboarding Checklist](06-onboarding-checklist.md).

## 3. Daily Tasks (PAM Admin)
- Review failed rotations and failed connection tests.
- Review pending/expired requests.
- Review break-glass usage (expected: none).
- Check `SG-Acct-Stale` and `SG-Asset-Unowned`.

## 4. Weekly Tasks
- Review discovery results for new privileged accounts.
- Review denied requests and unusual patterns (off-hours, repeated denials).
- Sample 3-5 session recordings for policy compliance.

## 5. Monthly / Quarterly
- Monthly: password-reveal exceptions review; access-request metrics.
- Quarterly: owner recertification for Tier 0/1; Smart Rule review; role-group membership review.

## 6. Offboarding
- **User leaves/changes role:** remove from requester groups same day; review open requests.
- **Account retired:** disable on target, remove from vault, archive logs, update inventory.

## 7. Incident Handling
Suspected credential compromise → block requests for the account → force rotation → review session recordings/logs → notify Security → document in incident record.

## 8. RACI
| Activity | PAM Admin | Owner | Approver | Security | Auditor |
|---|---|---|---|---|---|
| Onboarding | R | A | I | C | I |
| Access approval | I | C | R/A | I | I |
| Rotation monitoring | R | I | I | A | I |
| Recertification | C | R/A | I | C | I |
| Audit review | C | I | I | R | A |
