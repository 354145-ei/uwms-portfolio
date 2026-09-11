# Codex Task — UWMS Portfolio Capture

## Goal

Create a repeatable, evidence-based portfolio capture workflow for the current UWMS implementation.

This is **not** a product redesign task and **not** a feature-development task.

Do not invent missing functionality. Do not alter accepted business semantics only to make the portfolio look better.

## Evidence-first discovery

Before changing anything, inspect the current repository and report:

- supported local-preview/startup flow;
- current browser/E2E automation tooling;
- whether Playwright/Cypress/equivalent already exists;
- safe demo/acceptance data setup;
- authentication/bootstrap required for Manager and Staff views;
- screenshot and video capabilities already available;
- current authoritative routes for Manager planning, Candidate Review, Publication, and My Schedule.

Reuse existing tooling. Do not introduce a second browser automation framework if one is already present.

## Safety

Use only fictional/anonymized demo data.

Never expose:

- real employee/resident/patient data;
- passwords, tokens, client secrets, private keys;
- real database credentials;
- private development handoff documents;
- raw AI/Codex transcripts;
- local DB dumps;
- protected historical development data;
- unnecessary private filesystem paths.

Before capture, prove the environment is the intended safe demo/acceptance environment. If environment identity cannot be proven, stop rather than guessing.

## Required portfolio flow

Capture the current implementation of:

1. Planning Workspace
2. 必要人数 / staffing demand
3. Workforce / representative Scheduling Terms
4. 勤務希望・休暇
5. Generation Readiness / 作成前チェック
6. Candidate Generation
7. Candidate Review
8. 人員不足 / shortage diagnostics
9. Candidate correction utility
10. Publication
11. My Schedule
12. Useful Staff-side utilities currently available from My Schedule

Only show utilities that actually exist and are accepted in the current build.

## My Schedule

My Schedule is now a required Portfolio Release 1.0 showcase target.

Capture the current implementation exactly as it exists.

Where the prepared demo data supports it, prefer examples that make the screen understandable, such as a representative assigned work day and a Night → 明 sequence. Do not fabricate states or add UI solely for the portfolio.

## Screenshots

Produce recruiter-quality screenshots using a consistent desktop viewport.

Target assets, adjusted only when the current application structure requires better naming:

```text
portfolio/screenshots/
  01-planning-workspace.png
  02-staffing-demand.png
  03-requests-and-leave.png
  04-generation-readiness.png
  05-candidate-review.png
  06-staffing-shortage.png
  07-candidate-correction.png
  08-my-schedule.png
  09-my-schedule-utility.png
```

Candidate Review should be the primary hero screenshot if the current accepted UI remains the strongest manager-side view.

If the current My Schedule UI is meaningfully responsive and the repository already supports mobile viewport capture, also produce one mobile My Schedule screenshot. Do not add a new responsive implementation as part of this task.

Do not include browser developer tools in screenshots.

## Video

If the repository-supported browser tooling can reliably record video, generate one short portfolio demo.

Target duration: approximately 3–5 minutes.

Suggested sequence:

```text
Opening
→ Planning / staffing demand
→ Scheduling Terms
→ Requests / leave
→ Generation Readiness
→ Generate
→ Candidate Review
→ Shortage diagnostics
→ Correction
→ Publication
→ My Schedule
→ Staff utility
→ Closing
```

No narration is required.

Prefer a clean recording of the real UI over artificial animation or marketing effects.

If reliable video recording is not currently supported, do not force a fragile video stack. Produce the screenshot workflow and report the smallest safe option for video separately.

## Repeatable command

Prefer one project-supported command for regeneration, for example:

```text
scripts\portfolio-demo.cmd
```

or the closest existing script convention.

It should, where safely possible:

1. verify prerequisites;
2. verify the correct demo/acceptance environment;
3. start or reuse local preview;
4. execute deterministic browser capture;
5. save screenshots/video;
6. print output paths;
7. cleanly exit without destructive repository/database operations.

Do not require the user to manually find PIDs or manage several terminals when existing scripts can be reused.

## Portfolio handoff

Do not directly publish secrets or raw application source into `uwms-portfolio`.

At the end, provide a manifest mapping each generated asset to the portfolio slot it should fill:

```text
Candidate Review -> portfolio hero
Planning Workspace -> manager workflow
Shortage -> diagnostics
My Schedule -> staff experience
My Schedule utility -> staff utility showcase
```

## Verification

Return:

A. existing tooling reused
B. current routes used
C. safe demo data used
D. screenshots generated
E. video generated, or why intentionally omitted
F. one command to regenerate assets
G. privacy/security checks performed
H. utilities actually demonstrated
I. any requested capability omitted because the current build did not prove it
J. files changed

Do not commit unless explicitly authorized.
