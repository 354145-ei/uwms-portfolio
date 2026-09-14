# Architecture Overview

## System Shape

```text
┌──────────────────────────────────┐
│ React / TypeScript / Vite        │
│ Manager + Staff-facing Web UI    │
└────────────────┬─────────────────┘
                 │ REST
                 ▼
┌──────────────────────────────────┐
│ Java 21 / Spring Boot 3          │
│                                  │
│ Workforce                        │
│ Planning                         │
│ Scheduling Terms                 │
│ Staffing Demand                  │
│ Candidate                        │
│ Publication                      │
│ Authorization                    │
└────────────────┬─────────────────┘
                 │
                 ▼
┌──────────────────────────────────┐
│ PostgreSQL                       │
│ Flyway-managed schema history    │
└──────────────────────────────────┘
```

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
```

## Architectural Themes Demonstrated

### Multi-tenant thinking
Business data is tenant-scoped, with Facility acting as an operational boundary.

### Backend-authoritative rules
Important authorization, validation and scheduling rules are not delegated only to frontend visibility.

### Effective-dated business rules
Long-lived worker conditions are modeled separately from one-off planning requests.

### Retained planning evidence
Candidate and Publication lifecycles are treated as retained operational history rather than one mutable schedule.

### Cross-date scheduling semantics
Night work may cross date boundaries. The next-day `明` state is treated as continuation/reservation, not an unrelated second shift.

## Portfolio Note

This diagram is intentionally conceptual. The public portfolio should explain the architecture without exposing private development-only configuration, credentials, local environment details or internal handoff material.
