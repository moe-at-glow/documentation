# Write Architecture Decision Record

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P3-003 |
| **Owner** | Tech Lead |
| **Accountable** | Tech Lead |
| **SLA** | 3 business days |
| **Escalation** | Project Sponsor (scope issues), Product Owner (priority conflicts) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Architecture decision identified requiring formal record (see ADR Standard for trigger criteria)
- [ ] Context information available (requirements, constraints, team capabilities)
- [ ] Requirements driving the decision documented with IDs (BR/SWR)

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| No clear decision trigger criteria met | STOP. Document informally in ADD instead. | Tech Lead |
| Requirements driving the decision not yet baselined | STOP. Complete requirements baselining first. | Product Owner |
| Key technical stakeholders unavailable for evaluation | STOP. Reschedule when stakeholders available. | Tech Lead |

---

## PROCEDURE

### Step 1: Confirm ADR Is Required

| Action | Owner | SLA |
|--------|-------|-----|
| Evaluate decision against trigger criteria below | Tech Lead | 30 min |

- [ ] Selecting a technology (database, framework, library, cloud service)
- [ ] Choosing an architecture pattern (monolith, microservices, event-driven)
- [ ] Choosing an integration approach (REST, messaging, shared DB)
- [ ] Making a significant trade-off (consistency vs. availability, speed vs. accuracy)
- [ ] Deviating from an established standard or convention

> **IF** one or more criteria met **THEN** proceed to Step 2
> **ELSE** document decision informally in ADD; stop here

### Step 2: Assign ADR Number

| Action | Owner | SLA |
|--------|-------|-----|
| Check existing ADRs in `architecture/decisions/` | Tech Lead | 10 min |
| Take next sequential number | Tech Lead | 5 min |
| Create file: `architecture/decisions/NNN-short-description.md` | Tech Lead | 5 min |

- [ ] Existing ADR numbers checked
- [ ] Next sequential number assigned
- [ ] File created with correct naming convention (e.g., `003-use-redis-for-caching.md`)

### Step 3: Write Context Section

| Action | Owner | SLA |
|--------|-------|-----|
| Document the problem being solved | Tech Lead | 30 min |
| Reference specific BR/SWR IDs driving this decision | Tech Lead | 15 min |
| Document constraints (budget, timeline, team skills, infrastructure, regulations) | Tech Lead | 15 min |
| Document what changed to trigger this decision now | Tech Lead | 15 min |

- [ ] Problem stated with specifics (not vague)
- [ ] Requirement IDs referenced
- [ ] Constraints documented
- [ ] Trigger for decision documented

### Step 4: Research Alternatives

| Action | Owner | SLA |
|--------|-------|-----|
| Identify at least 2-3 viable alternatives | Tech Lead | 2 hours |
| Document for each: name/version, strengths, weaknesses, team experience, licensing, community/support | Tech Lead | 2 hours |

- [ ] Minimum 2-3 alternatives documented
- [ ] Each alternative has name and version
- [ ] Strengths and weaknesses assessed for project-specific use case
- [ ] Team experience level noted per alternative
- [ ] Licensing model documented per alternative
- [ ] Community/support status documented per alternative

### Step 5: Evaluate Trade-Offs

| Action | Owner | SLA |
|--------|-------|-----|
| Create comparison matrix with weighted criteria | Tech Lead | 1 hour |

| Criterion | Weight | Option A | Option B | Option C |
|-----------|--------|----------|----------|----------|
| Meets requirements | High | | | |
| Team expertise | High | | | |
| Performance | Medium | | | |
| Operational complexity | Medium | | | |
| Licensing cost | Low | | | |
| Community support | Medium | | | |

- [ ] All criteria listed and weighted
- [ ] All alternatives scored against each criterion
- [ ] Matrix completed

> **IF** no clear winner emerges **THEN** add project-specific criteria or adjust weights; re-evaluate
> **ELSE IF** two options score equally **THEN** prioritize team expertise and operational complexity as tiebreakers
> **ELSE** proceed with highest-scoring option

### Step 6: State the Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Write decision statement: "We will use [X] for [purpose]." | Tech Lead | 15 min |

- [ ] Decision is specific enough to implement
- [ ] Decision is traceable to context and requirements
- [ ] Decision is justifiable based on evaluation matrix

### Step 7: Document Consequences

| Action | Owner | SLA |
|--------|-------|-----|
| List positive consequences (benefits gained) | Tech Lead | 15 min |
| List negative consequences (trade-offs accepted) | Tech Lead | 15 min |
| List risks with mitigations | Tech Lead | 30 min |

- [ ] Positive consequences documented
- [ ] Negative consequences documented (trade-offs accepted)
- [ ] Risks documented with specific mitigations

### Step 8: Submit for Review and Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Set ADR status to Proposed | Tech Lead | 5 min |
| Request review from at least one peer (architect or senior developer) | Tech Lead | 1 business day for review |
| Address reviewer feedback | Tech Lead | 4 hours |
| Change status to Accepted (Tech Lead or System Architect) | Tech Lead | Upon approval |

- [ ] ADR status set to Proposed
- [ ] Peer review requested
- [ ] Peer review completed
- [ ] Feedback addressed
- [ ] Status changed to Accepted

> **IF** reviewer raises fundamental objections **THEN** return to Step 4 and re-evaluate alternatives
> **ELSE IF** reviewer suggests minor improvements **THEN** incorporate and proceed
> **ELSE** proceed to Step 9

### Step 9: Communicate the Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Reference ADR in Architecture Description Document | Tech Lead | 1 hour |
| Announce decision to project team | Tech Lead | 1 day |
| Update any affected documentation | Tech Lead | 1 day |

- [ ] ADR referenced in ADD
- [ ] Decision announced to project team
- [ ] Affected documentation updated

---

## EXIT CRITERIA

- [ ] ADR created with sequential number and correct file naming
- [ ] Context, alternatives, trade-offs, decision, and consequences fully documented
- [ ] Comparison matrix completed with at least 2-3 alternatives
- [ ] Peer review completed
- [ ] ADR status set to Accepted
- [ ] ADR referenced in ADD
- [ ] Decision communicated to project team

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Architecture Decision Record | [ADR Template](../templates/architecture-decision-record.md) | `architecture/decisions/` |
| Updated ADD (ADR reference added) | [ADD Template](../templates/architecture-description-document.md) | `architecture/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| ADR Standard | Standard | [../standards/architecture-decision-records-standard.md](../standards/architecture-decision-records-standard.md) |
| Architecture Description Standard | Standard | [../standards/architecture-description-standard.md](../standards/architecture-description-standard.md) |
| System Decomposition Standard | Standard | [../standards/system-decomposition-standard.md](../standards/system-decomposition-standard.md) |
| ADR Template | Template | [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md) |
| ADD Template | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
| Create Architecture Description | Runbook | [create-architecture-description.md](create-architecture-description.md) |
| Conduct Architecture Review | Runbook | [conduct-architecture-review.md](conduct-architecture-review.md) |
