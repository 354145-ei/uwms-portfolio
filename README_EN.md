# UWMS — Enterprise Workforce Management & Scheduling System

UWMS (Unified Workforce Management System) is a web-based workforce planning and scheduling system for organizations that operate shift-based work.

The project started from real operational problems observed in care work, while the product and domain are intentionally designed to remain industry-neutral rather than hard-coded for one type of facility.

> **Portfolio status:** Active development. Portfolio Release 1.0 is being prepared. Proven/current functionality and roadmap items are kept clearly separated.

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

## Manager Workflow

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
```

## Staff Experience — My Schedule

My Schedule is currently being completed for Portfolio Release 1.0. The portfolio will not present unfinished staff features as completed functionality.

The planned visual demo will show the staff-first current effective published schedule, month/week views, selected-day details, Night → next-day continuation, leave/off distinctions and self-service entry points where implemented.

## Tech Stack

**Backend:** Java 21, Spring Boot 3, Maven, PostgreSQL, JPA/JDBC, Flyway, REST, OpenAPI/Swagger.

**Frontend:** React, TypeScript, Vite, responsive web / PWA-oriented UI.

**Testing:** JUnit 5, Mockito, Testcontainers, frontend automated tests, integration tests and manual browser acceptance.

## Portfolio Demo

The Release 1.0 demo is designed as two connected stories:

1. **Manager Operations** — setup, staffing demand, worker conditions, requests/leave, readiness, generation, Candidate Review, shortage analysis, correction and publication.
2. **Staff Experience** — My Schedule and staff-facing utilities after the current My Schedule slice is complete.

See [docs/showcase-plan.md](docs/showcase-plan.md) and [demo/demo-scenario.md](demo/demo-scenario.md).
