# UWMS — Enterprise Workforce Management & Scheduling System

UWMS (Unified Workforce Management System) is a web-based workforce planning and scheduling system for organizations that operate shift-based work.

The project started from real operational problems observed in care work, while the product and domain are intentionally designed to remain industry-neutral rather than hard-coded for one type of facility.

> **Portfolio status:** Portfolio Release 1.0 now has its full showcase scope, including My Schedule. The remaining gates are actual screenshots, repeatable demo capture, security review and public release.

## Problem

A real roster may need to consider staffing demand, professions and qualifications, worker scheduling terms, weekday and holiday eligibility, requested days off, requested shifts, paid leave, absence, night-shift continuation, consecutive work, working-time constraints and staffing shortages.

UWMS prioritizes hard constraints and surfaces honest shortages instead of violating rules simply to make a schedule look fully staffed.

## Core Principles

- Coverage before Schedule
- Policy before Decision
- Workspace before Publish
- Revision, Never Replace
- Explain Every Decision
- Best Feasible Planning
- Honest Scheduling
- Human Final Decision Maker

## End-to-End Workflow

```text
Organization / Facility
        ↓
Workforce
        ↓
Profession / Qualification
        ↓
Shift Templates
        ↓
Staffing Demand
        ↓
Scheduling Terms
        ↓
Requests / Leave
        ↓
Generation Readiness
        ↓
Candidate Generation
        ↓
Candidate Review / Correction
        ↓
Publication
        ↓
My Schedule
```

## Staff Experience — My Schedule

My Schedule is now an official Portfolio Release 1.0 showcase target.

The portfolio will capture the current implementation as evidence rather than describing unverified staff-side capabilities. The demo will show the actual Staff schedule experience and the utilities that are available in the current accepted build.

## Tech Stack

**Backend:** Java 21, Spring Boot 3, Maven, PostgreSQL, JPA/JDBC, Flyway, REST, OpenAPI/Swagger.

**Frontend:** React, TypeScript, Vite, responsive web / PWA-oriented UI.

**Testing:** JUnit 5, Mockito, Testcontainers, frontend automated tests, integration tests and manual browser acceptance.

## Portfolio Demo

The Release 1.0 demo is designed as two connected stories:

1. **Manager Operations** — setup, staffing demand, worker conditions, requests/leave, readiness, generation, Candidate Review, shortage analysis, correction and publication.
2. **Staff Experience** — My Schedule and the Staff-facing utilities actually available in the current build.

See [Portfolio Web Preview](docs/index.html), [docs/showcase-plan.md](docs/showcase-plan.md), [demo/demo-scenario.md](demo/demo-scenario.md) and [demo/CODEX_CAPTURE_PROMPT.md](demo/CODEX_CAPTURE_PROMPT.md).
