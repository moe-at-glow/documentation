# RACI Matrix -- Requirements Engineering

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P2-001 |
| **Use When** | Determining who is responsible, accountable, consulted, or informed for a requirements engineering activity |
| **Last Updated** | 2026-03-04 |

---

## Legend

| Code | Meaning |
|------|---------|
| R | **Responsible** -- Does the work |
| A | **Accountable** -- Owns the outcome, has final authority |
| C | **Consulted** -- Provides input before the work is done |
| I | **Informed** -- Notified after the work is done |

---

## Matrix

| Activity | Project Sponsor | Product Owner | Business Analyst | Tech Lead | Developer | QA Lead | Domain Expert |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Stakeholder Analysis | I | A | R | C | -- | -- | C |
| Business Requirements Elicitation | C | A | R | C | -- | -- | R |
| Requirements Workshop Facilitation | I | C | R/A | C | -- | -- | R |
| BRD Authoring | -- | A | R | C | -- | I | C |
| Requirements Decomposition (STK/SYS/SWR) | -- | I | R | R/A | C | C | C |
| SRS Authoring | -- | I | R | A | C | C | -- |
| Requirements Review | I | R | R | R | C | R | C |
| Requirements Validation | I | A | R | R | -- | R | C |
| Traceability Matrix Maintenance | -- | I | R/A | C | I | C | -- |
| Change Request Processing | I | A | R | C | I | C | -- |
| Baseline Approval | A | R | I | R | I | R | -- |

---

## Role Definitions

| Role | Focus Area |
|------|-----------|
| Project Sponsor | Approves business case and baseline. Resolves escalations. Final authority on scope. |
| Product Owner | Defines business priorities. Accepts requirements. Decides on change requests. |
| Business Analyst | Facilitates elicitation. Authors BRD and SRS. Maintains RTM. Coordinates reviews. |
| Tech Lead | Reviews technical feasibility. Decomposes system/software requirements. Approves SRS. |
| Developer | Provides implementation perspective during decomposition and review. |
| QA Lead | Reviews testability. Defines test approach. Participates in validation. |
| Domain Expert | Provides subject matter knowledge during elicitation, workshops, and reviews. |

---

## DECISION TREE

### Who Owns This Activity?

```
IF activity involves stakeholder identification or elicitation
    THEN Business Analyst is R, Product Owner is A
    IF domain knowledge is needed
        THEN Domain Expert is also R

ELSE IF activity involves document authoring (BRD)
    THEN Business Analyst is R, Product Owner is A

ELSE IF activity involves technical decomposition or SRS authoring
    THEN Tech Lead is A
    IF implementation detail is needed
        THEN Developer is C

ELSE IF activity involves review or validation
    THEN multiple roles are R
    IF gate approval is required
        THEN Project Sponsor is A

ELSE IF activity involves change requests
    THEN Business Analyst is R, Product Owner is A
    IF baseline re-approval is needed
        THEN Project Sponsor is A

ELSE IF activity involves baseline approval
    THEN Project Sponsor is A, Product Owner is R
```

### Escalation Path

```
IF disagreement on requirement priority
    THEN escalate to Product Owner (A for elicitation/change requests)

IF disagreement on technical feasibility
    THEN escalate to Tech Lead (A for decomposition/SRS)

IF disagreement on scope impact
    THEN escalate to Project Sponsor (A for baseline approval)
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Conduct Stakeholder Analysis | Runbook | ../runbooks/conduct-stakeholder-analysis.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
| Change Request Form | Template | ../templates/change-request-form.md |
| Requirements Artifacts Checklist | Reference | ./requirements-artifacts-checklist.md |
| Glossary | Reference | ./glossary.md |
