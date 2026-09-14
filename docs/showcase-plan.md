# UWMS Portfolio Visual Showcase Plan

## Goal

Show both the **appearance** and the **operational utility** of UWMS in a recruiter-friendly way.

The final portfolio should not rely on source code alone. A recruiter should be able to understand the product from screenshots and a short demo video, while an engineer can continue into architecture and implementation details.

---

## Showcase Structure

### Track A — Manager Operations

This track can be prepared before My Schedule is fully complete.

#### 1. Planning Workspace / 勤務表作成
Show the planning flow and where the manager is in the process.

What to demonstrate:
- current PlanningPeriod / Facility context
- planning steps
- clear progress/state

#### 2. 必要人数 / Staffing Demand
Show that staffing demand exists before schedule generation.

What to demonstrate:
- Shift
- Profession
- minimum required headcount
- human-readable setup

Key portfolio message:
> UWMS models staffing demand first instead of generating a roster blindly.

#### 3. 対象スタッフ / Workforce Scope
Show who participates in the current planning workspace.

What to demonstrate:
- selected workers
- profession/business identity
- clean manager interaction

#### 4. 勤務条件 / Scheduling Terms
Show a few representative constraints, not every field.

Good examples:
- weekday eligibility
- public-holiday eligibility
- Night eligibility / Night agreement
- working-time condition where useful

Key portfolio message:
> Long-lived worker rules are separate from one-off monthly requests.

#### 5. 勤務希望・休暇
Show period-specific information.

Good examples:
- 希望休
- 希望シフト
- 有給
- 欠勤

Avoid real employee/resident data.

#### 6. 作成前チェック / Generation Readiness
This is one of the most useful UWMS utilities to demo.

Show:
- ready / blocked state
- meaningful business validation
- exact contradiction when available

Key portfolio message:
> The system detects incompatible HARD rules before generation rather than silently guessing precedence.

#### 7. Candidate Generation
Keep this short.

Show:
- explicit Generate action
- transition to the newly created Candidate

#### 8. Candidate Review — HERO SCREEN
This should be the main portfolio screenshot.

Show:
- roster grid
- worker hierarchy
- shift semantic colors
- Night / 明
- Public-Off / leave where available
- Candidate state

This screenshot should become the README hero image after anonymization.

#### 9. Staffing Shortages / 人員不足
This is another strong utility showcase.

Show:
- shortage summary
- affected dates
- by-date operational grouping
- Shift + Profession + shortage count
- expandable detail where available

Key portfolio message:
> UWMS explains where staffing demand is not satisfied instead of hiding shortage behind illegal assignments.

#### 10. Candidate Diagnostics / Explanation
If the current build exposes explanation/diagnostic evidence, show it briefly.

Only display evidence the backend actually supports. Do not invent causal explanations for the demo.

#### 11. Interactive Correction
Show manager control after optimization.

Target evidence:
- open correction grid
- modify assignment with the current supported interaction
- preserve manager as final decision maker

#### 12. Publication
Show the transition from Candidate to official schedule using the existing publication lifecycle.

Do not present publication as a simple overwrite.

---

## Track B — Staff Experience / My Schedule

**Status: wait for current My Schedule work to finish before recording or claiming completion.**

The final staff demo should focus on clarity and usefulness, not backend terminology.

### 1. Current Effective Published Schedule
Show the staff member's current official schedule.

### 2. Monthly View
This should be the default hero view for Staff.

Show:
- calendar month
- shift indicators
- Public-Off / leave distinction where implemented
- clear selected day

### 3. Weekly View
Show it briefly as a secondary viewing mode.

### 4. Selected-Day Detail
Show:
- shift
- time
- Facility
- official/published state where appropriate

### 5. Night → 明
Demonstrate that an overnight assignment is visually understandable as one continued work event rather than two unrelated shifts.

### 6. 勤務希望・休暇 Utilities
After implemented/accepted, show the actual staff-facing entry points available in the build.

Possible categories include:
- 希望シフト
- 希望休
- 有給申請
- 申請状況

Only show functions that are actually implemented in the final portfolio build.

### 7. Shift Swap
If the existing staff UI exposes an eligible shift-swap flow in the final demo build, include one short example.

Key portfolio message:
> Staff actions do not directly rewrite the official roster; the official lifecycle remains controlled.

---

## Utility Showcase Matrix

Before recording, verify each utility against the final acceptance build.

| Utility | Target demo | Record now? |
| --- | --- | --- |
| Setup / Organization / Facility | Administration capability | Yes, if current UI remains accepted |
| Workforce Member management | Add/update/activate/deactivate | Yes |
| CSV workforce import | Bulk onboarding utility | Optional short clip |
| Active Facility selection | Operational context | Optional |
| Setup progress | Customer onboarding/resumability | Optional |
| Scheduling Terms | Worker contract/rule authority | Yes |
| 勤務希望・休暇 | Period-specific planning facts | Yes |
| Generation Readiness | Pre-generation validation | **Yes — important** |
| Candidate generation | Create candidate | Yes |
| Candidate Review | Roster review | **Yes — hero** |
| Staffing shortage analysis | Operational diagnostic | **Yes — important** |
| Correction | Human decision workflow | **Yes** |
| Publication | Official lifecycle | **Yes** |
| Administrative audit | Traceable admin operations | Optional technical clip |
| My Schedule | Staff official schedule | **After completion** |
| Staff self-service utilities | Requests / status | Only after implementation proof |
| Shift swap | Staff contextual workflow | If present in final accepted build |

---

## Screenshot Set for Release 1.0

Target 6–8 screenshots maximum.

Recommended:

1. **Hero:** Candidate Review — 勤務表
2. Staffing shortages / 人員不足
3. Planning Workspace / workflow
4. 勤務希望・休暇
5. Workforce / Scheduling Terms
6. **My Schedule — monthly view** (after completion)
7. My Schedule — selected-day detail or request utility
8. Optional architecture diagram

Do not overload the README with every screen.

---

## Video Structure

Recommended final video length: **3–5 minutes**.

### 0:00–0:25 — Problem / Product
Explain UWMS in one sentence.

### 0:25–1:30 — Planning Inputs
必要人数 → Workforce → Scheduling Terms → Requests / Leave.

### 1:30–2:00 — Readiness + Generate
Show pre-check and candidate creation.

### 2:00–3:05 — Candidate Review
Roster + shortages + correction.

### 3:05–3:30 — Publication
Show official lifecycle.

### 3:30–4:30 — My Schedule
After completion: month view, selected-day detail, staff utilities.

### 4:30–5:00 — Architecture / Developer Scope
Show Java/Spring/PostgreSQL/React architecture and explain end-to-end responsibility.

---

## Visual Rules

- Use fictional/anonymized worker names.
- No real resident/patient/customer data.
- Hide technical UUIDs unless the screenshot is explicitly about technical evidence.
- Keep browser chrome/account information out of screenshots where possible.
- Prefer consistent viewport sizes.
- Show real accepted UI; do not create portfolio-only mockups that misrepresent the product.
- My Schedule screenshots are added only after the current implementation is accepted.
