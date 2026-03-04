# RACI Matrix -- Business Analysis

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P1-002 |
| **Use When** | Determining who is responsible, accountable, consulted, or informed for a Phase 1 business analysis activity |
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

| Activity | Project Sponsor | Product Owner | Business Analyst | Tech Lead | Developer | QA Lead | Domain Expert | Operations Lead |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Business needs identification | C | A | R | C | -- | -- | R | C |
| Problem statement definition | I | A | R | C | -- | -- | C | -- |
| Business case development | A | C | R | C | -- | -- | C | C |
| Risk assessment | C | C | R | R | -- | C | C | R |
| Project charter creation | A | R | R | C | -- | -- | -- | I |
| Stakeholder identification | I | A | R | C | -- | -- | C | C |
| Project scale determination | A | R | C | R | -- | -- | -- | C |
| Phase 1 gate review | A | R | R | R | I | I | I | I |

---

## Role Definitions

| Role | Focus Area |
|------|-----------|
| Project Sponsor | Approves business case and project charter. Resolves escalations. Final authority on project go/no-go. |
| Product Owner | Defines business priorities. Validates problem statement. Co-authors project charter. Decides project scale. |
| Business Analyst | Conducts needs analysis. Authors business case. Identifies stakeholders. Facilitates gate review preparation. |
| Tech Lead | Provides technical feasibility input. Assesses technical risks. Advises on project scale from technical perspective. |
| Developer | Informed of Phase 1 outcomes. No active Phase 1 role. |
| QA Lead | Consulted on risk assessment (testability, quality risks). Informed of Phase 1 outcomes. |
| Domain Expert | Provides subject matter knowledge during needs identification and problem definition. |
| Operations Lead | Provides operational impact input. Consulted on operational risks and infrastructure implications. |

---

## DECISION TREE

### Who Owns This Activity?

```
IF activity involves identifying or analyzing business needs
    THEN Business Analyst is R, Product Owner is A
    IF domain knowledge is needed
        THEN Domain Expert is also R
    IF operational impact assessment is needed
        THEN Operations Lead is C

ELSE IF activity involves problem statement or business case authoring
    THEN Business Analyst is R
    IF business case
        THEN Project Sponsor is A
    ELSE IF problem statement
        THEN Product Owner is A

ELSE IF activity involves risk assessment
    THEN Business Analyst is R, Tech Lead is R
    IF operational risks are relevant
        THEN Operations Lead is R
    IF quality or testability risks are relevant
        THEN QA Lead is C

ELSE IF activity involves project charter creation
    THEN Product Owner is R, Business Analyst is R, Project Sponsor is A

ELSE IF activity involves stakeholder identification
    THEN Business Analyst is R, Product Owner is A
    IF organizational knowledge is needed
        THEN Domain Expert is C

ELSE IF activity involves project scale determination
    THEN Product Owner is R, Tech Lead is R, Project Sponsor is A

ELSE IF activity involves gate review
    THEN Project Sponsor is A
    AND Product Owner, Business Analyst, Tech Lead are R (presenters/reviewers)
    AND Developer, QA Lead, Domain Expert, Operations Lead are I
```

### Escalation Path

```
IF disagreement on business need validity or priority
    THEN escalate to Product Owner (A for needs identification)

IF disagreement on business case justification
    THEN escalate to Project Sponsor (A for business case)

IF disagreement on technical feasibility or technical risk assessment
    THEN escalate to Tech Lead (R for risk assessment)
    IF unresolved
        THEN escalate to Project Sponsor

IF disagreement on project scale classification
    THEN escalate to Project Sponsor (A for scale determination)

IF disagreement on project go/no-go at gate review
    THEN Project Sponsor has final authority (A for gate review)

IF any role is unavailable for >3 business days
    THEN escalate to Product Owner for reassignment
    IF Product Owner is unavailable
        THEN escalate to Project Sponsor
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Business Needs Analysis | Runbook | ../runbooks/conduct-business-needs-analysis.md |
| Business Case Development | Runbook | ../runbooks/develop-business-case.md |
| Project Charter Creation | Runbook | ../runbooks/create-project-charter.md |
| Initial Stakeholder Identification | Runbook | ../runbooks/conduct-initial-stakeholder-identification.md |
| Business Analysis Artifacts Checklist | Reference | ./business-analysis-artifacts-checklist.md |
| Business Value Assessment Reference | Reference | ./business-value-assessment-reference.md |
| RACI Matrix -- Requirements Engineering | Reference | ../../phase-2-requirements-engineering/references/raci-matrix.md |
| SDLC Framework Standard | Standard | ../../standards/sdlc-framework.md |
| Phase 1 Standards | Standard | ../standards/phase-1-standards.md |
| Glossary | Reference | ../../phase-2-requirements-engineering/references/glossary.md |
