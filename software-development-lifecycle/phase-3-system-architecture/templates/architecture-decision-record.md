# Architecture Decision Record

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-001 |
| **When to Use** | Recording any architecture-significant decision (technology, pattern, integration) |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect |
| **SLA** | 2 business days per ADR |
| **Runbook** | [Write Architecture Decision Record](../runbooks/write-architecture-decision-record.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Evaluation Matrix optional; Alternatives Considered reduced to 1 alternative
> **IF** medium project (3-5 devs) **THEN** Minimum 2 alternatives; Evaluation Matrix recommended
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] ADR-XXX: [Title of Decision]

### [ ] Status

[Proposed | Accepted | Deprecated | Superseded by ADR-XXX]

### [ ] Date

YYYY-MM-DD

### [ ] Context

- What problem are you solving?
- What requirements drive this decision? (Reference specific SWR/SYS/BR IDs.)
- What constraints exist? (Budget, timeline, team skills, infrastructure, regulations.)
- What has changed that triggers this decision now?

### [ ] Decision

"We will use [X] for [purpose]."

### [ ] Consequences

#### [ ] Positive

- [Benefit 1: what the team gains from this decision]
- [Benefit 2]
- [Benefit 3]

#### [ ] Negative

- [Trade-off 1: what is given up or accepted as a cost]
- [Trade-off 2]

#### [ ] Risks

- [Risk 1 and mitigation approach]
- [Risk 2 and mitigation approach]

### [ ] Alternatives Considered

#### [ ] [Alternative 1 Name]

- **Description:** [What it is]
- **Pros:** [Advantages for our use case]
- **Cons:** [Disadvantages for our use case]
- **Why rejected:** [Specific reason this was not chosen]

#### [ ] [Alternative 2 Name]

- **Description:** [What it is]
- **Pros:** [Advantages for our use case]
- **Cons:** [Disadvantages for our use case]
- **Why rejected:** [Specific reason this was not chosen]

#### [ ] [Alternative 3 Name] (optional)

- **Description:** [What it is]
- **Pros:** [Advantages for our use case]
- **Cons:** [Disadvantages for our use case]
- **Why rejected:** [Specific reason this was not chosen]

### [ ] Evaluation Matrix (optional, for technology choices)

| Criterion | Weight | [Option A] | [Option B] | [Option C] |
|-----------|--------|-----------|-----------|-----------|
| Requirements Fit | 5 | | | |
| Team Expertise | 4 | | | |
| Maturity | 4 | | | |
| Operational Complexity | 3 | | | |
| Performance | 3 | | | |
| **Weighted Total** | | | | |

### [ ] Related Documents

- Requirements: [SWR-XXX, SYS-XXX]
- Architecture: [ADD section reference]
- Supersedes: [ADR-XXX, if applicable]

---

## COMPLETION CHECKLIST

- [ ] ADR ID assigned and title filled in
- [ ] Status set to Proposed
- [ ] Context describes the problem with requirement references
- [ ] Decision is specific and implementable
- [ ] Positive and negative consequences listed
- [ ] Risks identified with mitigations
- [ ] At least 1 alternative considered (2+ for medium/large projects)
- [ ] Evaluation Matrix completed (if technology choice)
- [ ] Related documents linked
- [ ] Reviewed by System Architect

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description-document.md](architecture-description-document.md) | ADRs are listed in ADD Section 12 |
| Component Diagram | [component-diagram.md](component-diagram.md) | Decisions may drive component boundaries |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Decisions may affect external integrations |
| Software Requirements Specification | Phase 2 SRS | Requirements referenced in Context |
| Runbook | [Write Architecture Decision Record](../runbooks/write-architecture-decision-record.md) | Step-by-step procedure |
