# Architecture Overview

This page presents the UWMS architecture at portfolio level. Development-only configuration, credentials and private environment details are intentionally excluded.

---

## System Shape

```text
┌────────────────────────────────────┐
│ React / TypeScript / Vite          │
│ Manager + Staff-facing Web UI      │
└─────────────────┬──────────────────┘
                  │ REST API
                  ▼
┌────────────────────────────────────┐
│ Java 21 / Spring Boot 3            │
│                                    │
│ Workforce                          │
│ Planning                           │
│ Scheduling Terms                   │
│ Staffing Demand                    │
│ Candidate                          │
│ Publication                        │
│ Authorization                      │
│ Timefold-based Optimization        │
└─────────────────┬──────────────────┘
                  │
                  ▼
┌────────────────────────────────────┐
│ PostgreSQL                         │
│ Flyway-managed schema history      │
└────────────────────────────────────┘

Authentication / Identity
        └── Keycloak + OpenID Connect
```

---

## Planning Flow

```text
Facility
   ↓
Planning Workspace
   ↓
Staffing Demand + Workforce Scope
   ↓
Scheduling Terms
   ↓
Approved Requests / Leave
   ↓
Constraint Projection / Readiness
   ↓
Candidate Generation
   ↓
Candidate Review
   ↓
Human Correction
   ↓
Publication
   ↓
My Schedule
```

The generated result is not automatically treated as the official roster. UWMS separates **Candidate → human review/correction → Publication** so automation remains subordinate to an explicit business decision.

---

## Architectural Themes

### Tenant and Facility boundaries
Business data is tenant-aware, while Facility acts as an important operational and scheduling boundary. Authorization is not based only on frontend visibility; backend access checks matter as well.

### Backend-authoritative validation
The UI may provide early feedback, but important authorization and scheduling decisions are validated again at backend lifecycle boundaries.

### Long-lived conditions vs one-off requests
Recurring worker conditions such as weekday or night eligibility are modeled separately from date-specific requests, leave and exceptions.

### Staffing Demand before assignment
The system first defines how many workers are required for a date, shift and profession. Candidate generation then tries to satisfy that demand rather than simply filling a calendar from worker availability.

### Optimization separated from final validation
Timefold Solver searches for a feasible Candidate. Important lifecycle operations such as persistence, correction and publication do not rely on solver output alone; business HARD rules are revalidated by the backend.

### Retained historical evidence
Worker settings can change over time. Historical Candidates and Publications therefore should not silently change just because today's configuration is different. UWMS treats retained scheduling evidence and current configuration as separate concerns.

### Cross-date duty semantics
Night work may cross a date boundary. The next-day continuation is treated as part of the same duty rather than an unrelated second shift so work-day counts, night counts and consecutive-work semantics remain meaningful.

---

## Technology by Layer

| Layer | Technology | Role |
| --- | --- | --- |
| Web UI | React / TypeScript / Vite | Manager and staff-facing screens |
| API / Domain | Java 21 / Spring Boot 3 | Business logic, authorization, validation and REST API |
| Optimization | Timefold Solver | Candidate schedule search |
| Database | PostgreSQL | Business and historical data |
| Migration | Flyway | Schema history |
| Identity | Keycloak / OIDC | Authentication foundation |
| Test | JUnit 5 / Mockito / Testcontainers | Unit, integration and database verification |

---

## Portfolio Note

This architecture description is intentionally conceptual. The public portfolio should demonstrate engineering decisions without exposing credentials, private operational data, database dumps, local-only configuration, private handoff material or raw AI-development transcripts.

日本語版: [architecture.md](architecture.md)
