# Engineering Decisions

This page highlights decisions that make UWMS more than a CRUD portfolio.

## 1. Coverage is a minimum, not an exact headcount

If required staffing is 3:

- 2 = shortage
- 3 = satisfied
- 4 = valid surplus

A legal surplus is different from a domain violation.

## 2. Workforce Member is not the same as Login Identity

A worker can participate in scheduling without having an application account. This allows managers to schedule employees who never use staff self-service. Login identity is linked only when application access is required.

## 3. UUID for internal identity; business code for humans

Internal relationships should remain stable when human-readable codes change. UWMS therefore separates immutable system identity from business identifiers and display names.

## 4. HARD constraints must not be relaxed to hide shortages

If staffing demand cannot be satisfied legally, the product should preserve the rule and expose the shortage instead of creating an invalid roster that merely appears complete.

## 5. Night D → 明 D+1 is one cross-date assignment

`明` is not a second independent Shift Template. It is a continuation/reserved next-day state from the previous Night assignment.

## 6. Long-lived worker conditions and one-off requests are separate

Recurring Scheduling Terms such as weekday eligibility belong to long-lived worker conditions. Date-specific requests such as 希望休 / 希望シフト belong to the planning/request lifecycle.

## 7. Candidate and Publication are lifecycle concepts

A generated Candidate is not the final official roster. The manager remains the final decision-maker, while Publication represents the official lifecycle boundary.

## 8. Historical integrity matters

Past Candidates and Publications should not silently change only because current worker settings have changed. The system therefore treats retained evidence and current configuration as different concerns.
