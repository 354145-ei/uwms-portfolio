# UWMS Portfolio Demo Scenario

Target duration: approximately 3–5 minutes.

The final demo should show both **product appearance** and **real operational utility** using only safe fictional/demo data.

## 0. Opening — 15 seconds

Show the UWMS title and Planning entry point.

Explain:

> UWMS is a workforce planning and scheduling system. It combines staffing demand, worker conditions, requests and leave, then generates a candidate roster for manager review and publication.

## 1. 必要人数 — 20 seconds

Open staffing demand and show a compact example.

Key sentence:

> Coverage is the minimum staffing requirement. Surplus can be legal; shortage is shown honestly.

## 2. 対象スタッフ / 勤務条件 — 25 seconds

Show worker selection and representative Scheduling Terms that exist in the current build.

Key sentence:

> Long-term worker conditions are separated from one-off requests.

## 3. 勤務希望・休暇 — 25 seconds

Show representative request / leave facts supported by the current build.

Key sentence:

> Approved planning facts become authoritative input to the scheduling process.

## 4. 作成前チェック — 25 seconds

Show Generation Readiness.

Key sentence:

> UWMS detects incompatible hard rules before generation instead of silently choosing which rule to ignore.

## 5. Candidate Generation — 20 seconds

Generate a Candidate using prepared fictional acceptance/demo data.

Keep this part short and predictable.

## 6. Candidate Review — 45 seconds

This is the main manager-side showcase.

Show only capabilities present in the current accepted build, for example:
- roster
- shift presentation
- Night / 明 semantics
- Candidate state
- shortage visibility
- correction entry point

Key sentence:

> Generation is not the final decision. The manager reviews, diagnoses and corrects the Candidate.

## 7. Staffing Shortage Utility — 25 seconds

Open 人員不足 and show the available shortage analysis.

Key sentence:

> UWMS does not hide unmet demand by violating hard constraints.

## 8. Correction — 25 seconds

Use the supported correction experience and change one assignment if the demo fixture safely supports it.

Key sentence:

> Optimization assists the manager; it does not replace the manager's final decision.

## 9. Publication — 20 seconds

Show the current publication action / lifecycle.

Key sentence:

> The official roster is published through a separate lifecycle instead of simply overwriting the generated Candidate.

## 10. My Schedule — 40 seconds

My Schedule is now an official Portfolio Release 1.0 showcase target.

Demonstrate the **current implementation exactly as it exists**. Do not add or simulate a missing utility only for the portfolio.

Suggested sequence:

1. Enter the Staff-facing My Schedule experience.
2. Show the main schedule view.
3. Select a representative work day and show its detail if supported.
4. Show a representative Night → 明 case when available in the prepared demo data.
5. Show the currently implemented schedule status / leave / off presentation that is useful to explain.
6. Show the real utility or self-service entry points currently available from the Staff experience.
7. Show shift-swap related UX only if it is present and accepted in the current build.

Key sentence:

> Staff can view the current effective official schedule through a Staff-oriented experience, while controlled workflows remain separate from direct modification of the published roster.

## 11. Utility Showcase — 20 seconds

Briefly show 2–3 utilities that best demonstrate product depth. Select them from the current build rather than forcing a predetermined list.

Good candidates include:
- Generation Readiness
- 人員不足 / diagnostics
- Candidate correction utilities
- Publication / revision history
- Workforce / Scheduling Terms
- Staff utilities in My Schedule

## 12. Closing — 15 seconds

Show the architecture diagram / GitHub README / portfolio page.

Closing message:

> I designed and implemented the project end-to-end: requirements, domain model, backend, database, REST API, frontend, scheduling rules, tests, UX and acceptance.

## Capture rule

The demo is evidence, not marketing fiction.

- Use only the current implementation.
- Use fictional/anonymized data.
- Do not expose secrets or private development information.
- Do not redesign the product only for the recording.
- If a capability is unstable during capture, omit it and record the omission in the capture report.
