# Engineering Decisions

This page highlights the decisions that make UWMS more than a CRUD portfolio project.

---

## 1. Staffing Demand is a minimum, not an exact headcount

If required staffing is 3:

- 2 → shortage of 1
- 3 → satisfied
- 4 → valid surplus

A legal surplus is not the same thing as a domain violation. UWMS therefore treats shortage and surplus differently.

---

## 2. Workforce Member is not the same as Login Identity

A worker may participate in scheduling without ever logging in to UWMS.

```text
Workforce Member = business worker
Login Identity   = application user
```

The two concepts are linked only when application access is required.

---

## 3. Internal identity is separated from human-facing business codes

Employee codes and display names may change. Internal relationships should remain stable.

UWMS therefore separates immutable internal identity such as UUIDs from business-facing codes.

---

## 4. HARD constraints must not be relaxed just to hide shortages

A schedule can appear complete if the system silently breaks an important rule.

UWMS instead preserves HARD constraints and surfaces unresolved demand as a shortage. A valid incomplete schedule is preferable to an invalid schedule that merely looks full.

---

## 5. Planning limits and compliance limits are different concepts

A worker being legally allowed to work up to 28 hours does not automatically mean the scheduler should plan 28 hours.

For example, a normal planning target and planning maximum may be 24 hours while 28 hours is only the compliance ceiling. The remaining headroom should not be consumed automatically to satisfy coverage.

UWMS therefore keeps **planning target / planning maximum / compliance maximum** conceptually distinct.

---

## 6. Night D → next-day continuation D+1 is one duty

Night work crosses a date boundary.

```text
10/01 Night
10/02 Post-night continuation
```

The next-day continuation is not a second independent Shift Template. Treating it as one duty keeps night counts, scheduled-day counts and consecutive-work semantics meaningful.

---

## 7. Long-lived worker conditions and one-off requests are separate

Examples of long-lived conditions:

- weekday eligibility
- public-holiday eligibility
- night eligibility
- weekly scheduled-day expectations

Examples of one-off requests:

- requested day off
- requested shift
- paid leave
- absence

These concepts have different business lifecycles and should not be stored or interpreted as the same kind of data.

---

## 8. Candidate and Publication are different lifecycle concepts

A generated result is not yet the official roster.

```text
Candidate
   ↓
Review / Correction
   ↓
Publication
```

Candidate represents a schedule proposal that can still be reviewed and corrected. Publication represents the official roster boundary.

This keeps the human manager as the final decision-maker.

---

## 9. Published schedules should not be silently overwritten

If the official roster changes, replacing the previous state without history makes it impossible to understand what was official at an earlier point in time.

UWMS therefore treats Publication as a revision/history concept rather than one mutable row that is repeatedly overwritten.

---

## 10. Historical Candidates and Publications should not be rebuilt from current settings alone

Worker conditions and Shift Templates can change over time.

Reconstructing an old schedule from only today's configuration can produce a state that never existed when the schedule was created.

UWMS therefore separates retained planning evidence from current configuration.

---

## 11. Important validation belongs on the backend too

Frontend restrictions improve usability, but they are not a sufficient integrity boundary.

Authorization and important scheduling rules are also checked by backend logic so business rules cannot be bypassed simply by calling an API directly.

---

## 12. Planning-period boundaries do not reset real scheduling semantics

A monthly planning screen does not mean real work resets at the end of a month.

Examples include:

- consecutive work continuing from the previous month
- a Night shift at month end whose next-day continuation falls in the next month
- a Monday–Sunday week that crosses the planning-period boundary

UWMS therefore treats cross-period continuity as part of scheduling semantics rather than resetting everything at the visible month boundary.

---

## Summary

The project is designed around several principles:

- preserve the meaning of business rules
- let humans review automated results
- expose shortages rather than hide them
- preserve historical integrity
- maintain continuity across planning-period boundaries
- keep important validation backend-authoritative

日本語版: [engineering-decisions.md](engineering-decisions.md)
