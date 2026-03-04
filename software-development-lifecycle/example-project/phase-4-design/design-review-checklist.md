> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Design Review Checklist

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-004 |
| **When to Use** | Conducting design review for each component before implementation |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 1 business day per component review |
| **Runbook** | ../runbooks/conduct-design-review.md |
| **Last Verified** | 2025-10-15 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** SOLID Principles section optional; self-review acceptable
> **IF** medium project (3-5 devs) **THEN** All sections required; peer review required
> **IF** large project (6+ devs) **THEN** Full template required; dedicated review meeting required

**Selected:** Small project (1-2 devs)

---

## [x] Component: Calculation Engine / Project Engine (Power Atlas)
## [x] Reviewer: Mohammad Al-Farsi (Tech Lead)
## [x] Date: 2025-10-15

---

## [x] Architecture Adherence

| Check | Pass | Notes |
|-------|:----:|-------|
| Component responsibility matches ADD | [x] | Calculation Engine handles all power math; Project Engine handles CRUD and status. Clean split. |
| Component boundaries match architecture | [x] | Calculation Engine is stateless and called internally by Project Engine routes. No boundary violations. |
| Technology choices align with ADRs | [x] | Python 3.11, Flask, SQLite as specified in ADR-001 and ADR-003. |
| Interfaces match architecture contracts | [x] | All REST endpoints match the contracts defined in ADD Section 4.2. |
| Data ownership respects component boundaries | [x] | Calculation Engine owns no tables; Project Engine owns projects, folders, project_activity. |

---

## [x] API Design

| Check | Pass | Notes |
|-------|:----:|-------|
| URL structure follows API standard | [x] | All endpoints under `/api/` prefix. Resource-oriented nouns used consistently. |
| HTTP methods used correctly | [x] | GET for reads, POST for creates, PUT for updates, DELETE for archives. |
| Request/response schemas fully defined | [x] | All request bodies and response schemas documented with types and constraints. |
| All error responses documented | [x] | Error codes defined for 400, 401, 403, 404, 409, 422, 429 scenarios. |
| Pagination implemented for list endpoints | [x] | GET /api/projects supports page and per_page with defaults (1, 25). |
| Authentication requirements specified | [x] | Each endpoint states whether JWT is required; public endpoints clearly marked. |
| Idempotency addressed for write operations | [x] | Documented as "Not required" for all write endpoints -- acceptable for v1 with SQLite. |
| snake_case used for JSON fields | [x] | All field names use snake_case consistently. |

---

## [x] Data Model

| Check | Pass | Notes |
|-------|:----:|-------|
| Naming follows database standard | [x] | All table and column names use snake_case. Consistent naming pattern across tables. |
| Required columns present (id, timestamps) | [x] | All tables have primary key and created_at. Most have updated_at where applicable. |
| Foreign keys and constraints defined | [x] | All relationships have FK constraints with appropriate ON DELETE behavior. |
| Indexes support identified query patterns | [x] | Indexes on user_id (projects), project_id (loads), email (users), and composite indexes for critical load queries. |
| Normalization verified (3NF minimum) | [x] | Tables are in 3NF. Denormalization on client_requirements is documented with rationale. |
| Denormalization documented with rationale | [x] | Three denormalization decisions documented: client_requirements fields, project_data JSON, layout_data JSON. |
| Migration scripts structured | [x] | 13 migration files listed in dependency order. |

---

## [x] Business Logic

| Check | Pass | Notes |
|-------|:----:|-------|
| All assigned requirements addressed | [x] | SWR-010 through SWR-012 (calculations), SWR-020 through SWR-024 (project management) all mapped. |
| Algorithms clearly specified | [x] | Step-by-step pseudocode for all calculation methods and project state transitions. |
| Edge cases identified and handled | [x] | Zero amps, unity PF, large amps warning, empty project activation -- all covered. |
| Business rules match SRS acceptance criteria | [x] | Formulas match: single-phase kW = (A x 230 x PF) / 1000, three-phase kW = (A x 400 x sqrt(3) x PF) / 1000. |

---

## [x] Error Handling

| Check | Pass | Notes |
|-------|:----:|-------|
| All error scenarios identified | [x] | Validation errors, not-found, state conflicts, auth failures, and DB errors all listed. |
| Error responses follow standard format | [x] | Consistent `{ error: { code, message, details } }` structure across all endpoints. |
| Recovery/retry strategy defined where applicable | [x] | DB connection failure returns 500 with log; client-side retry is implicit. |
| No sensitive data in error messages | [x] | Password hashes, tokens never exposed. Generic "invalid credentials" for auth failures. |

---

## [x] Security

| Check | Pass | Notes |
|-------|:----:|-------|
| Input validation defined at boundaries | [ ] | **FINDING #1 (Blocker):** Calculation endpoints accept raw numeric inputs from API layer but validation is only in PowerCalculator class. Need explicit validation middleware at the API route level before data reaches the service layer. |
| Authorization checks for each endpoint | [x] | Owner checks on projects/folders. Admin-only on requirement approval. Readonly users blocked from writes. |
| SQL injection prevention (parameterized queries) | [x] | SQLAlchemy ORM used throughout -- all queries are parameterized. |
| Sensitive data not logged | [x] | Password hashes excluded from all log statements. JWT tokens logged only at DEBUG level (disabled in production). |
| No secrets hardcoded | [x] | JWT secret and bcrypt rounds configured via environment variables. |

---

## [x] Testability

| Check | Pass | Notes |
|-------|:----:|-------|
| Dependencies injectable (can be mocked) | [x] | Calculation Engine takes no external dependencies. Project Engine uses SQLAlchemy session that can be replaced with in-memory SQLite for testing. |
| Public methods have clear inputs and outputs | [x] | All PowerCalculator methods have typed inputs and dict outputs. All API endpoints have documented request/response schemas. |
| Acceptance criteria are testable | [x] | Calculation formulas can be verified with known input/output pairs. State machine transitions are deterministic. |
| Edge cases can be unit tested | [x] | Zero values, boundary values, and invalid inputs all have defined behavior that can be asserted. |

---

## [x] SOLID Principles

> Scaling gate: optional for small projects. Included for completeness.

| Check | Pass | Notes |
|-------|:----:|-------|
| Single Responsibility: each module has one reason to change | [x] | Calculation Engine changes only when formulas change. Project Engine changes only when project lifecycle rules change. |
| Open/Closed: extensible without modification | [x] | New load types can be added to the CHECK constraint. New phase types (DC) can be added to convertAmpsToKw dispatcher. |
| Interface Segregation: no forced dependencies on unused methods | [x] | Aggregate methods (calculateTotalLoad, calculateCriticalLoad) are separate from unit conversion methods. |
| Dependency Inversion: depends on abstractions for externals | [x] | Database access via SQLAlchemy ORM abstracts SQLite specifics. |

---

## [x] Traceability

| Check | Pass | Notes |
|-------|:----:|-------|
| Every design element traces to a requirement | [x] | Traceability table in detailed design maps every method/endpoint to an SWR. |
| No orphan design elements (no requirement source) | [x] | All design elements have corresponding SWR references. |
| RTM updated with design references | [x] | RTM cross-reference table added to detailed design document. |

---

## [x] Decision

| Decision | Criteria |
|----------|---------|
| [ ] Approved | All checks pass |
| [x] Approved with conditions | Minor issues; list below |
| [ ] Rework required | Blocking issues; list below |

**Decision: Approved with conditions.** One blocking finding must be resolved before implementation begins. Two suggestions are recommended but non-blocking.

---

## [x] Findings

| ID | Severity | Description | Action Required |
|----|----------|-------------|----------------|
| 1 | **Blocker** | **Input validation missing at API route level for calculation endpoints.** The PowerCalculator class validates inputs internally, but the API route handlers (`POST /api/loads`) pass raw request body values directly to the calculation service without pre-validation. A malformed or malicious request could reach the calculation layer before being caught. Add a Flask request validation decorator or middleware (e.g., using `marshmallow` or `flask-expects-json`) at the route level to validate all numeric inputs (amps, voltage, power_factor, quantity) before they reach the service layer. | Rami Haddad to add request validation middleware to all calculation-related API routes before implementation begins. Target: 2025-10-18. |
| 2 | Suggestion | **Consider adding rate limiting to the public requirements endpoint.** `POST /api/requirements/submit` is unauthenticated. While not a current risk at expected volume, adding a basic rate limit (e.g., 10 requests per minute per IP) would prevent abuse. Flask-Limiter can be added with minimal effort. | Recommended for v1.1. Log as a backlog item. |
| 3 | Suggestion | **Add `updated_at` trigger or application-level update to the loads table.** The loads table has `created_at` but no `updated_at` column. If loads are ever edited (via a future `PUT /api/loads/:id` endpoint), there will be no audit trail of when the load was last modified. Consider adding `updated_at` now to avoid a migration later. | Recommended. Add `updated_at` column to the loads table DDL before implementation. Low effort, high value for future-proofing. |

---

## COMPLETION CHECKLIST

- [x] Component name, reviewer, and date filled in
- [x] Architecture Adherence section reviewed
- [x] API Design section reviewed
- [x] Data Model section reviewed
- [x] Business Logic section reviewed
- [x] Error Handling section reviewed
- [x] Security section reviewed
- [x] Testability section reviewed
- [x] SOLID Principles section reviewed
- [x] Traceability section reviewed
- [x] Decision recorded: **Approved with conditions**
- [x] All findings logged with severity and required actions
- [x] Review outcome communicated to component author (Rami Haddad) on 2025-10-15

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Document under review | ./detailed-design.md |
| API Specification | API contracts under review | ./api-specification.md |
| Data Model Document | Data model under review | ./data-model.md |
| Conduct Design Review Runbook | Step-by-step procedure | ../../../phase-4-design/runbooks/conduct-design-review.md |
| Architecture Description Document | Reference architecture for adherence checks | ../../phase-3-system-architecture/architecture-description-document.md |
| Software Requirements Specification | Source requirements for traceability checks | ../../phase-2-requirements-engineering/software-requirements-specification.md |
