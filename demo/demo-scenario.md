# UWMS Portfolio Demo Scenario

Target duration: approximately 3–5 minutes.

The final demo should show both **product appearance** and **real operational utility**.

## 0. Opening — 15 seconds

Show the UWMS title and Planning entry point.

Explain:

> UWMS is a workforce planning and scheduling system. It combines staffing demand, worker conditions, requests and leave, then generates a candidate roster for manager review.

## 1. 必要人数 — 20 seconds

Open staffing demand.

Show a compact example such as:

- Day Shift
  - Care Worker: 2
  - Nurse: 1
- Night Shift
  - Care Worker: 1

Key sentence:

> Coverage is the minimum staffing requirement. Surplus can be legal; shortage is shown honestly.

## 2. 対象スタッフ / 勤務条件 — 25 seconds

Show worker selection and representative Scheduling Terms.

Point out:
- weekday eligibility
- holiday eligibility
- Night eligibility
- Profession

Key sentence:

> Long-term worker conditions are separated from one-off requests.

## 3. 勤務希望・休暇 — 25 seconds

Show examples of:
- 希望休
- 希望シフト
- 有給 / 欠勤

Key sentence:

> Approved planning facts become authoritative input to the scheduling process.

## 4. 作成前チェック — 25 seconds

Show Generation Readiness.

Key sentence:

> UWMS detects incompatible hard rules before generation instead of silently choosing which rule to ignore.

## 5. Candidate Generation — 20 seconds

Generate a Candidate using prepared fictional acceptance data.

Keep this part short and predictable.

## 6. Candidate Review — 50 seconds

This is the main demo moment.

Show:
- roster
- shift colors
- Night / 明
- Public-Off / leave indicators where available
- Candidate state
- Staffing shortages
- correction entry point

Key sentence:

> Generation is not the final decision. The manager reviews, diagnoses and corrects the Candidate.

## 7. Staffing Shortage Utility — 30 seconds

Open 人員不足.

Show:
- total shortage
- affected dates
- shift
- profession
- shortage count
- expandable detail where supported

Key sentence:

> UWMS does not hide unmet demand by violating hard constraints.

## 8. Correction — 30 seconds

Open the supported correction experience and change one assignment.

Key sentence:

> Optimization assists the manager; it does not replace the manager's final decision.

## 9. Publication — 20 seconds

Show the existing publication action/lifecycle.

Key sentence:

> The official roster is published through a separate lifecycle instead of simply overwriting the generated Candidate.

## 10. My Schedule — after current implementation is complete — 45 seconds

Do not record this section until the current My Schedule implementation passes acceptance.

Target sequence:

1. Login/view as Staff
2. Open My Schedule
3. Show month view
4. Select one work day
5. Show selected-day detail
6. Show a Night → 明 example
7. Show Public-Off / leave distinction where implemented
8. Show the actual available staff utilities / request entry points
9. Optionally show shift swap if present and accepted in the final build

Key sentence:

> Staff see the current effective official schedule; self-service actions do not directly rewrite the published roster.

## 11. Closing — 15 seconds

Show the architecture diagram / GitHub README.

Closing message:

> I designed and implemented the project end-to-end: requirements, domain model, backend, database, REST API, frontend, scheduling rules, tests, UX and acceptance.
