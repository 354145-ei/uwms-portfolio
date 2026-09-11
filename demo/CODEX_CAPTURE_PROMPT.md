# Codex Task — UWMS Portfolio Capture

## Goal

Create a repeatable, evidence-based portfolio capture workflow for the current UWMS implementation.

This is **not** a redesign task and **not** a feature-development task.

Do not invent missing functionality or change accepted business semantics just to improve the portfolio.

## Evidence-first discovery

Before changing anything, inspect the current repository and report:

- supported local-preview/startup flow;
- current browser/E2E automation tooling;
- whether Playwright/Cypress/equivalent already exists;
- safe demo/acceptance data setup;
- authentication/bootstrap for Manager and Staff views;
- screenshot/video capabilities already available;
- authoritative routes for Planning, Candidate Review, Publication, and My Schedule.

Reuse existing tooling. Do not add a second browser automation framework if one already exists.

## Safety

Use only fictional/anonymized demo data.

Never expose real employee/resident/patient data, passwords, tokens, client secrets, private keys, real DB credentials, private handoff documents, raw AI/Codex transcripts, DB dumps, protected historical development data, or unnecessary private filesystem paths.

Before capture, prove the environment is the intended safe demo/acceptance environment. If environment identity cannot be proven, stop rather than guessing.

## Screenshot capture

Capture the current implementation of the strongest recruiter-facing screens.

Target assets:

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

Candidate Review should remain the primary Manager-side hero screenshot when it is still the strongest accepted view.

My Schedule is a required Staff-side showcase target.

Use a consistent desktop viewport. If the existing My Schedule implementation is meaningfully responsive and the repository already supports mobile capture, also produce one mobile My Schedule screenshot.

Do not capture browser developer tools.

## Short video

If the existing browser automation can reliably record video, generate **one very short portfolio demo**.

Target duration: **60–90 seconds**.
Hard maximum: **2 minutes**.

Prefer about 60 seconds if the story can be shown cleanly.

Suggested sequence:

```text
0:00–0:05  UWMS opening
0:05–0:15  Planning / key input or readiness
0:15–0:35  Candidate Generation / Candidate Review
0:35–0:48  Shortage diagnostics / correction
0:48–0:55  Publication
0:55–1:15  My Schedule + one Staff utility
1:15–1:20  Closing / tech stack
```

The exact timing may shift, but keep the whole video concise.

Do not try to demonstrate every UWMS feature in the video. Screenshots and documentation will cover the details.

No narration is required.

Prefer:

- direct navigation;
- short transitions;
- no artificial waiting;
- no marketing animation;
- the real accepted UWMS UI.

If video recording is not reliably supported by existing tooling, do not introduce a fragile recording stack. Produce the screenshot workflow and report the smallest safe video option separately.

## My Schedule

Capture the current implementation exactly as it exists.

Prefer demo data that makes the UI understandable, such as one assigned work day and, when naturally available, a Night → 明 sequence.

Show one useful Staff utility that is actually implemented. Do not fabricate states or add UI only for the portfolio.

## Repeatable command

Prefer one project-supported command such as:

```text
scripts\portfolio-demo.cmd
```

or the closest existing convention.

Where safely possible it should:

1. verify prerequisites;
2. verify the safe demo/acceptance environment;
3. start or reuse local preview;
4. execute deterministic browser capture;
5. save screenshots/video;
6. print output paths;
7. exit without destructive repository/database operations.

## Portfolio handoff

Provide a manifest mapping generated assets to portfolio slots, for example:

```text
Candidate Review -> Manager hero
Planning Workspace -> Manager workflow
Shortage -> Diagnostics
My Schedule -> Staff hero
My Schedule utility -> Staff utility
Video -> Short product overview
```

## Verification

Return:

A. existing tooling reused
B. routes used
C. safe demo data used
D. screenshots generated
E. video generated, or why omitted
F. final video duration
G. one command to regenerate assets
H. privacy/security checks
I. utilities actually demonstrated
J. omitted capability not proven by current build
K. files changed

Do not commit unless explicitly authorized.
