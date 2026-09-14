# UWMS — Enterprise Workforce Management & Scheduling System

> A web-based workforce scheduling system that supports the full flow from **planning → Candidate generation → review/correction → Publication → staff self-service** while respecting staffing demand, worker conditions, requests, leave and cross-date shift rules.

UWMS (Unified Workforce Management System) is a personal full-stack project for organizations that operate shift-based work.

The project started from operational problems observed in care work, but the domain is intentionally designed to remain industry-neutral so the same scheduling concepts can be applied to healthcare, retail, hospitality, manufacturing and other shift-based environments.

▶ **[Watch the UWMS Demo on YouTube](https://youtu.be/cms7WxH145w)**

[Portfolio Web](docs/index.html) · [Architecture](docs/architecture_EN.md) · [Engineering Decisions](docs/engineering-decisions_EN.md) · [Demo Scenario](demo/demo-scenario.md) · [日本語](README.md)

---

## Recruiter Snapshot

| Area | Summary |
| --- | --- |
| Project type | Personal full-stack development |
| Product scope | Workforce planning, schedule generation, review/correction, publication and staff schedule viewing |
| Backend | Java 21 / Spring Boot 3 / REST API |
| Frontend | React / TypeScript / Vite |
| Database | PostgreSQL / Flyway |
| Optimization | Timefold Solver |
| Identity | Keycloak / OpenID Connect |
| Verification | JUnit 5 / Mockito / Testcontainers / integration tests / browser acceptance |
| Ownership | Requirements, domain design, DB design, backend, API, frontend, tests, acceptance and documentation |

### About this repository

`uwms-portfolio` is a **portfolio-safe showcase repository**, not a raw export of the private development workspace.

Its purpose is to present the product, architecture, engineering decisions, screenshots and demo material without exposing credentials, local configuration, private handoff documents or real operational data.

---

## Problem

Real workforce scheduling is not just assigning an available employee to an empty slot.

A schedule may need to consider all of the following at the same time:

- staffing demand
- professions and qualifications
- worker scheduling terms
- weekday and public-holiday eligibility
- requested days off and requested shifts
- paid leave and absence
- night shifts and next-day continuation
- consecutive work
- weekly or period-based working-day and working-time limits
- staffing shortages

UWMS follows a simple rule:

> **Do not hide a shortage by silently breaking an important rule.**

The system aims to preserve HARD constraints, surface remaining shortages honestly and keep the manager as the final decision-maker.

---

## End-to-End Workflow

```text
Organization / Facility
        ↓
Workforce / Profession / Qualification / Shift Setup
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

A generated Candidate is intentionally separated from the official Publication lifecycle. The generated result can be reviewed and corrected before it becomes the active roster.

---

## Key Product Areas

### Workforce and Setup
- Organization / Facility-aware administration
- Workforce Member management
- Profession and qualification management
- Separation between Workforce Member and login identity
- Facility-scoped operational access

### Staffing Demand
Demand is modeled as a **minimum required staffing level**, not an exact headcount target.

```text
Required = 3

2 → shortage of 1
3 → satisfied
4 → valid surplus
```

### Scheduling Terms
Long-lived worker conditions are separated from date-specific requests and leave.

Examples include weekday eligibility, holiday eligibility, night-shift eligibility, weekly working-day targets and working-time limits.

### Requests and Leave
- requested day off
- requested shift
- paid leave
- hourly paid leave
- absence

Approved items are projected into planning according to their business meaning.

### Night Shift Continuation
A night shift is modeled as one cross-date duty.

```text
10/01  Night
10/02  Post-night continuation
```

The next-day continuation is not an independent second Shift Template.

### Candidate Generation
Timefold Solver is used to search for a feasible schedule candidate from staffing demand and worker constraints.

The goal is not to produce a visually full roster at any cost, but to create the best feasible result while preserving HARD rules and exposing unresolved shortages.

### Candidate Review / Correction
Managers can inspect the generated result, shortages and diagnostics, then make the final adjustment before publication.

### Publication
The official roster is treated as a lifecycle boundary rather than a mutable table that is silently overwritten. Historical state and revision semantics are part of the design.

### My Schedule
Staff can view the currently active published schedule through the staff-facing experience.

The portfolio intentionally shows only capabilities that have been actually verified in the accepted build.

---

## Engineering Highlights

UWMS goes beyond CRUD by addressing domain and lifecycle concerns such as:

- separating Workforce Member from authentication identity
- separating immutable internal UUIDs from human-facing business codes
- modeling coverage as minimum staffing demand
- refusing to relax HARD rules simply to hide shortages
- modeling Night → next-day continuation as one cross-date duty
- separating Candidate from Publication lifecycle
- preserving historical scheduling evidence
- backend-authoritative authorization and scheduling validation
- cross-period scheduling semantics
- avoiding silent reconstruction of historical decisions from only current configuration

See [Engineering Decisions](docs/engineering-decisions_EN.md).

---

## Architecture

```text
React / TypeScript / Vite
          │
          │ REST API
          ▼
Java 21 / Spring Boot 3
          │
          ├── Workforce
          ├── Planning
          ├── Scheduling Terms
          ├── Staffing Demand
          ├── Candidate
          ├── Publication
          ├── Authorization
          └── Timefold-based Optimization
          │
          ▼
PostgreSQL
          │
          └── Flyway

Authentication / Identity: Keycloak + OIDC
```

See [Architecture](docs/architecture_EN.md).

---

## Development Ownership

As a personal project, I am responsible for:

- problem framing and requirements
- domain modeling
- database design
- backend implementation
- REST API design
- frontend implementation
- scheduling-rule and optimization design
- authentication / authorization design
- database migration design
- automated tests
- manual acceptance verification
- UI / UX improvement
- technical documentation

AI-assisted development tools are used as development support, while requirements, design decisions, acceptance criteria, review and final verification remain developer-controlled.

---

## Portfolio Readiness

- [x] Dedicated portfolio repository
- [x] Japanese README
- [x] English README
- [x] Architecture and engineering-decision documentation
- [x] Portfolio web-page foundation
- [x] Main manager workflow verified
- [x] My Schedule verified
- [x] Fictional demo data used for portfolio verification
- [ ] Final screenshot selection
- [x] Demo video captured and linked on YouTube
- [ ] Final public-security review
- [ ] Public release

Public-release checklist: [SECURITY_REVIEW_CHECKLIST.md](SECURITY_REVIEW_CHECKLIST.md)

> Payroll is intentionally outside the current initial product scope.
