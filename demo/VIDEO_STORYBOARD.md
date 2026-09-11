# UWMS Portfolio Video Storyboard

Target duration: **60–90 seconds**. Absolute maximum: **2 minutes**.

The video is a quick product overview, not a complete tutorial. Detailed technical explanation belongs in the README, screenshots, architecture notes and engineering decisions.

## Sequence

### 0:00–0:05 — Opening
Show UWMS branding and the main Planning entry point.

On-screen caption:

> UWMS — Enterprise Workforce Management & Scheduling System

### 0:05–0:15 — Planning / Readiness
Show the Planning Workspace and briefly reveal one useful planning utility such as Generation Readiness.

On-screen caption:

> Staffing demand + worker conditions + requests + leave

Do not dwell on form entry.

### 0:15–0:35 — Candidate Review
This is the main manager-side showcase.

Show the roster clearly. Prefer a prepared Candidate that makes the layout easy to understand.

Where naturally visible in the current build, show Night / 明 and schedule statuses.

On-screen caption:

> Generate → Review → Human decision

### 0:35–0:48 — Shortage / Correction
Open 人員不足 or the strongest shortage diagnostic view, then briefly show the supported correction experience.

On-screen caption:

> Shortages are surfaced, not hidden by breaking HARD constraints

Do not spend time editing several assignments. One representative action is enough.

### 0:48–0:55 — Publish
Show the publication action or resulting published state.

On-screen caption:

> Candidate → Official Published Schedule

### 0:55–1:15 — My Schedule
Switch to the Staff-facing experience.

Show:
- My Schedule main view;
- one selected work day / detail if supported;
- one useful Staff-side utility or request entry point;
- Night → 明 only if the prepared demo data presents it naturally.

On-screen caption:

> Staff experience — current effective official schedule

### 1:15–1:20 — Closing
Show UWMS name + tech stack or the portfolio landing page.

On-screen caption:

> Java 21 · Spring Boot 3 · PostgreSQL · React · TypeScript

If the story is already clear at ~60 seconds, end there. Do not stretch the video to fill 90 seconds.

## Recording Rules

- Use the real current UWMS implementation.
- Use only fictional/anonymized demo data.
- No developer tools in frame.
- No terminal unless required for a very brief opening/closing proof; UI is the priority.
- Avoid long loading/waiting scenes.
- Avoid excessive mouse movement.
- Prefer clean cuts between major areas when necessary.
- Do not fabricate UI states or capabilities.
- Do not redesign the application for the video.
- No narration is required.
- Background music is unnecessary.
- Captions should be short and professional.

## Portfolio Role

The video is supplementary evidence. Recruiters should still be able to understand the project without watching it.

Primary evidence remains:

1. README
2. Hero screenshots
3. Architecture
4. Engineering decisions
5. Short video demo
