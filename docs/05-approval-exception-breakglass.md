# 05. Approval, Exception & Break-Glass Workflow

## Standard Request
```mermaid
sequenceDiagram
    participant U as Requester
    participant PS as Password Safe
    participant A as Approver
    participant T as Target System
    U->>PS: Request access (asset, account, duration, reason, ticket)
    PS->>PS: Evaluate access policy
    alt Auto-approve policy
        PS-->>U: Approved (time-bound)
    else Approval required
        PS->>A: Notify
        A->>PS: Approve / Deny
        PS-->>U: Decision
    end
    U->>PS: Launch session
    PS->>T: Proxy connection with vaulted credential
    Note over PS,T: Session recorded
    U->>PS: Check-in or timeout
    PS->>T: Rotate password
    PS->>PS: Write audit log
```

## Approver Checklist
1. Is the ticket/change valid and current?
2. Does the business justification match the requested asset?
3. Is the requested duration minimal?
4. Is the requester in the correct role group?
5. Any conflicting change/incident?

## Break-Glass Procedure
**When:** Password Safe unavailable, or critical incident requiring immediate Tier 0 access.
1. Declare incident; get approval from Security Manager and Head of Infrastructure.
2. Retrieve sealed emergency credential (two-person control).
3. Log start time, reason, people involved.
4. Perform only the actions needed.
5. Rotate the emergency credential immediately afterward and re-seal.
6. Post-incident review within 2 working days; attach logs/recordings.
7. Alert is generated on any use of the break-glass account.
