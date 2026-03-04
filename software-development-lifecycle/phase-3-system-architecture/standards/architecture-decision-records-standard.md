# Architecture Decision Records Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P3-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Architecture Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** ADRs required for technology and infrastructure decisions only; informal notes acceptable for minor pattern choices
> **IF** medium project (3-5 devs) **THEN** ADRs required for all criteria listed below; peer review optional
> **IF** large project (6+ devs) **THEN** Full compliance required including peer review and formal approval

---

## COMPLIANCE REQUIREMENTS

### When an ADR Is Required

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | ADR required for technology choices (e.g., database, language, runtime) | All projects | [ ] ADR exists for each technology choice | Block architecture review |
| 2 | ADR required for architecture pattern choices (e.g., monolith vs microservices) | All projects | [ ] ADR exists for pattern decisions | Block architecture review |
| 3 | ADR required for integration approach decisions (e.g., MQTT vs HTTP) | All projects | [ ] ADR exists for integration decisions | Block architecture review |
| 4 | ADR required for framework or library selections | All projects | [ ] ADR exists for framework/library choices | Block architecture review |
| 5 | ADR required for infrastructure decisions (e.g., cloud provider) | All projects | [ ] ADR exists for infrastructure decisions | Block architecture review |
| 6 | ADR required for security mechanism decisions (e.g., JWT vs sessions) | All projects | [ ] ADR exists for security decisions | Block architecture review |
| 7 | ADR required for data storage approach decisions | All projects | [ ] ADR exists for storage decisions | Block architecture review |
| 8 | ADR required for trade-off decisions (e.g., consistency vs availability) | All projects | [ ] ADR exists for trade-off decisions | Block architecture review |
| 9 | ADR required for protocol or format choices (e.g., JSON vs Protobuf) | All projects | [ ] ADR exists for protocol decisions | Block architecture review |

### ADR Format

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 10 | ADR must include Status field (Proposed / Accepted / Deprecated / Superseded by ADR-XXX) | All ADRs | [ ] Status field present and valid | Rework required |
| 11 | ADR must include Date field (YYYY-MM-DD) | All ADRs | [ ] Date field present and formatted correctly | Rework required |
| 12 | ADR must include Context section (situation, forces, constraints, requirement IDs) | All ADRs | [ ] Context section present with specifics | Rework required |
| 13 | ADR must include Decision section (clear statement: "We will use [X] for [Y]") | All ADRs | [ ] Decision stated concisely | Rework required |
| 14 | ADR must include Consequences section with Positive, Negative, and Risks subsections | All ADRs | [ ] All three subsections present | Rework required |
| 15 | ADR must include Alternatives Considered section with description, pros, cons, rejection reason per alternative | All ADRs | [ ] At least one alternative documented with all fields | Rework required |

### ADR Numbering and Storage

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 16 | ADR numbers follow format ADR-XXX, assigned sequentially | All ADRs | [ ] Sequential numbering verified | Rework required |
| 17 | ADR numbers are never reused, even if deprecated | All ADRs | [ ] No reused numbers | Rework required |
| 18 | ADR files stored in architecture/decisions/ within the relevant topic directory | All ADRs | [ ] File location correct | Rework required |
| 19 | File naming follows pattern: XXX-short-description.md (e.g., 001-use-mqtt-for-iot-telemetry.md) | All ADRs | [ ] File naming convention followed | Rework required |

### ADR Lifecycle

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 20 | ADR status transitions follow: Proposed -> Accepted -> Deprecated or Superseded | All ADRs | [ ] Status transitions valid | Rework required |
| 21 | Deprecated ADRs include deprecation reason and date | Deprecated ADRs | [ ] Deprecation metadata present | Rework required |
| 22 | Superseded ADRs include "Superseded by ADR-XXX" reference | Superseded ADRs | [ ] Supersession reference present | Rework required |

### Roles and Approvals

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 23 | ADR authored by System Architect or Tech Lead | All ADRs | [ ] Author role verified | Rework required |
| 24 | ADR reviewed by a peer (senior developer or architect) | All ADRs | [ ] Peer review documented | Block acceptance |
| 25 | ADR accepted by Tech Lead (for Architect's ADRs) or System Architect (for Tech Lead's ADRs) | All ADRs | [ ] Approval documented | ADR remains in Proposed status |
| 26 | ADR deprecation approved by Tech Lead | Deprecated ADRs | [ ] Tech Lead approval documented | Deprecation rejected |

---

## COMPLIANCE CHECKLIST

- [ ] ADR written for every technology, pattern, integration, framework, infrastructure, security, storage, trade-off, and protocol decision
- [ ] Each ADR contains: Status, Date, Context (with requirement IDs), Decision, Consequences (positive/negative/risks), Alternatives Considered
- [ ] ADR numbering is sequential (ADR-XXX) with no reuse
- [ ] ADR files stored in architecture/decisions/ with naming pattern XXX-short-description.md
- [ ] Status transitions follow valid lifecycle (Proposed -> Accepted -> Deprecated/Superseded)
- [ ] Deprecated ADRs have deprecation reason and date
- [ ] Superseded ADRs reference the replacing ADR
- [ ] Each ADR authored by System Architect or Tech Lead
- [ ] Each ADR peer-reviewed
- [ ] Each ADR formally accepted by appropriate approver

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Write Architecture Decision Record | Runbook | [../runbooks/write-architecture-decision-record.md](../runbooks/write-architecture-decision-record.md) |
| Conduct Architecture Review | Runbook | [../runbooks/conduct-architecture-review.md](../runbooks/conduct-architecture-review.md) |
| Architecture Decision Record | Template | [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md) |
