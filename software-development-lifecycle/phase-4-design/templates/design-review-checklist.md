# Design Review Checklist

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-004 |
| **When to Use** | Conducting design review for each component before implementation |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 1 business day per component review |
| **Runbook** | ../runbooks/conduct-design-review.md |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** SOLID Principles section optional; self-review acceptable
> **IF** medium project (3-5 devs) **THEN** All sections required; peer review required
> **IF** large project (6+ devs) **THEN** Full template required; dedicated review meeting required

---

## [ ] Component: [Component Name]
## [ ] Reviewer: [Name]
## [ ] Date: YYYY-MM-DD

---

## [ ] Architecture Adherence

| Check | Pass | Notes |
|-------|:----:|-------|
| Component responsibility matches ADD | [ ] | |
| Component boundaries match architecture | [ ] | |
| Technology choices align with ADRs | [ ] | |
| Interfaces match architecture contracts | [ ] | |
| Data ownership respects component boundaries | [ ] | |

---

## [ ] API Design (if applicable)

| Check | Pass | Notes |
|-------|:----:|-------|
| URL structure follows API standard | [ ] | |
| HTTP methods used correctly | [ ] | |
| Request/response schemas fully defined | [ ] | |
| All error responses documented | [ ] | |
| Pagination implemented for list endpoints | [ ] | |
| Authentication requirements specified | [ ] | |
| Idempotency addressed for write operations | [ ] | |
| snake_case used for JSON fields | [ ] | |

---

## [ ] Data Model (if applicable)

| Check | Pass | Notes |
|-------|:----:|-------|
| Naming follows database standard | [ ] | |
| Required columns present (id, timestamps) | [ ] | |
| Foreign keys and constraints defined | [ ] | |
| Indexes support identified query patterns | [ ] | |
| Normalization verified (3NF minimum) | [ ] | |
| Denormalization documented with rationale | [ ] | |
| Migration scripts structured | [ ] | |

---

## [ ] Business Logic

| Check | Pass | Notes |
|-------|:----:|-------|
| All assigned requirements addressed | [ ] | |
| Algorithms clearly specified | [ ] | |
| Edge cases identified and handled | [ ] | |
| Business rules match SRS acceptance criteria | [ ] | |

---

## [ ] Error Handling

| Check | Pass | Notes |
|-------|:----:|-------|
| All error scenarios identified | [ ] | |
| Error responses follow standard format | [ ] | |
| Recovery/retry strategy defined where applicable | [ ] | |
| No sensitive data in error messages | [ ] | |

---

## [ ] Security

| Check | Pass | Notes |
|-------|:----:|-------|
| Input validation defined at boundaries | [ ] | |
| Authorization checks for each endpoint | [ ] | |
| SQL injection prevention (parameterized queries) | [ ] | |
| Sensitive data not logged | [ ] | |
| No secrets hardcoded | [ ] | |

---

## [ ] Testability

| Check | Pass | Notes |
|-------|:----:|-------|
| Dependencies injectable (can be mocked) | [ ] | |
| Public methods have clear inputs and outputs | [ ] | |
| Acceptance criteria are testable | [ ] | |
| Edge cases can be unit tested | [ ] | |

---

## [ ] SOLID Principles

| Check | Pass | Notes |
|-------|:----:|-------|
| Single Responsibility: each module has one reason to change | [ ] | |
| Open/Closed: extensible without modification | [ ] | |
| Interface Segregation: no forced dependencies on unused methods | [ ] | |
| Dependency Inversion: depends on abstractions for externals | [ ] | |

---

## [ ] Traceability

| Check | Pass | Notes |
|-------|:----:|-------|
| Every design element traces to a requirement | [ ] | |
| No orphan design elements (no requirement source) | [ ] | |
| RTM updated with design references | [ ] | |

---

## [ ] Decision

| Decision | Criteria |
|----------|---------|
| [ ] Approved | All checks pass |
| [ ] Approved with conditions | Minor issues; list below |
| [ ] Rework required | Blocking issues; list below |

---

## [ ] Findings

| ID | Severity | Description | Action Required |
|----|----------|-------------|----------------|
| 1 | Blocker/Concern/Observation | [Finding] | [Action] |

---

## COMPLETION CHECKLIST

- [ ] Component name, reviewer, and date filled in
- [ ] Architecture Adherence section reviewed
- [ ] API Design section reviewed (if applicable)
- [ ] Data Model section reviewed (if applicable)
- [ ] Business Logic section reviewed
- [ ] Error Handling section reviewed
- [ ] Security section reviewed
- [ ] Testability section reviewed
- [ ] SOLID Principles section reviewed
- [ ] Traceability section reviewed
- [ ] Decision recorded (Approved / Approved with conditions / Rework required)
- [ ] All findings logged with severity and required actions
- [ ] Review outcome communicated to component author

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Document under review | ./detailed-design-document.md |
| API Specification | API contracts under review | ./api-specification.md |
| Data Model Document | Data model under review | ./data-model-document.md |
| Conduct Design Review Runbook | Step-by-step procedure | ../runbooks/conduct-design-review.md |
| Architecture Description Document | Reference architecture for adherence checks | ../architecture-description-document.md |
| Software Requirements Specification | Source requirements for traceability checks | ../../phase-2-requirements-engineering/templates/software-requirements-specification.md |
