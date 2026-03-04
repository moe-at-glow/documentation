# Project Charter Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P1-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Project Sponsor |
| **Verification Method** | Phase 1 Gate Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project **THEN** Simplified charter; scope statement, key constraints, core roles (Sponsor, PO) required; formal scale determination optional
> **IF** medium project **THEN** Standard charter; full scope definition, all constraint categories, all core roles, formal scale determination required
> **IF** large project **THEN** Full compliance; all sections, all constraint categories with mitigation strategies, all roles with backup assignments, formal scale determination with justification

---

## COMPLIANCE REQUIREMENTS

### Scope Definition Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Charter MUST contain an explicit In-Scope section | All projects | [ ] In-Scope section present | Reject at gate review; return for revision |
| 2 | Charter MUST contain an explicit Out-of-Scope section | All projects | [ ] Out-of-Scope section present | Reject at gate review; return for revision |
| 3 | In-Scope section MUST list specific deliverables or capabilities | All projects | [ ] Specific deliverables enumerated | Return for revision |
| 4 | Out-of-Scope section MUST list at minimum 3 explicitly excluded items | Medium/Large | [ ] >= 3 out-of-scope items documented | Return for revision |
| 5 | Scope boundaries MUST be stated in unambiguous, testable terms | Medium/Large | [ ] Scope items are verifiable | Return for revision |
| 6 | Scope change process MUST be defined in the charter | Large | [ ] Scope change process documented | Return for revision |

### Constraint Documentation Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 7 | Charter MUST document timeline constraints with target dates | All projects | [ ] Timeline constraint documented with dates | Reject at gate review; return for revision |
| 8 | Charter MUST document technology constraints (platform, language, infrastructure) | Medium/Large | [ ] Technology constraints documented | Reject at gate review; return for revision |
| 9 | Charter MUST document regulatory constraints (applicable regulations, compliance requirements) | Medium/Large | [ ] Regulatory constraints documented or explicitly stated as none | Reject at gate review; return for revision |
| 10 | Charter MUST document staffing constraints (team availability, skill gaps) | Medium/Large | [ ] Staffing constraints documented | Return for revision |
| 11 | Each constraint MUST include impact assessment if constraint is violated | Large | [ ] Impact assessment documented per constraint | Return for revision |
| 12 | Each constraint MUST include a mitigation strategy | Large | [ ] Mitigation strategy documented per constraint | Return for revision |

### Role Assignment Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 13 | Project Sponsor MUST be a named individual with title and department | All projects | [ ] Sponsor identified by name, title, department | Reject at gate review; cannot proceed |
| 14 | Product Owner MUST be a named individual with title and department | All projects | [ ] Product Owner identified by name, title, department | Reject at gate review; cannot proceed |
| 15 | Business Analyst MUST be a named individual with title and department | Medium/Large | [ ] BA identified by name, title, department | Reject at gate review; return for revision |
| 16 | Technical Lead MUST be a named individual with title and department | Medium/Large | [ ] Tech Lead identified by name, title, department | Reject at gate review; return for revision |
| 17 | Each named role MUST have documented responsibilities | Medium/Large | [ ] Responsibilities listed per role | Return for revision |
| 18 | Each named role MUST have documented decision authority | Large | [ ] Decision authority defined per role | Return for revision |
| 19 | Backup/delegate MUST be assigned for each core role | Large | [ ] Backup individual named per core role | Return for revision |
| 20 | RACI matrix MUST be included for key project activities | Large | [ ] RACI matrix present | Return for revision |

### Project Scale Determination Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 21 | Project scale MUST be formally determined as Small, Medium, or Large | Medium/Large | [ ] Scale determination documented | Reject at gate review; return for revision |
| 22 | Small: 1-2 developers AND estimated effort <= 500 person-hours AND single team AND low regulatory impact | All projects | [ ] Small criteria applied correctly if classified as Small | Escalate to Sponsor for reclassification |
| 23 | Medium: 3-5 developers OR estimated effort 500-5000 person-hours OR 2-3 teams OR moderate regulatory impact | All projects | [ ] Medium criteria applied correctly if classified as Medium | Escalate to Sponsor for reclassification |
| 24 | Large: 6+ developers OR estimated effort > 5000 person-hours OR 4+ teams OR high regulatory impact | All projects | [ ] Large criteria applied correctly if classified as Large | Escalate to Sponsor for reclassification |
| 25 | Scale determination MUST include the data points used for classification | Medium/Large | [ ] Classification data points documented | Return for revision |
| 26 | Scale determination MUST include written justification when borderline | Medium/Large | [ ] Justification provided if project falls near boundary | Return for revision |
| 27 | Scale determination MUST be approved by Project Sponsor | Medium/Large | [ ] Sponsor approval on scale determination recorded | Cannot proceed to Phase 1 gate |

### Charter Approval

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Charter MUST be approved by Project Sponsor | All projects | [ ] Sponsor sign-off recorded | Cannot proceed to Phase 1 gate |
| 29 | Charter MUST be approved by Product Owner | All projects | [ ] Product Owner sign-off recorded | Cannot proceed to Phase 1 gate |
| 30 | Charter MUST be approved by Technical Lead | Medium/Large | [ ] Tech Lead sign-off recorded | Cannot proceed to Phase 1 gate |
| 31 | All approvals MUST include date, name, and role of approver | All projects | [ ] Approval metadata complete | Return for revision |

---

## COMPLIANCE CHECKLIST

- [ ] In-Scope section present with specific deliverables enumerated
- [ ] Out-of-Scope section present with >= 3 excluded items (medium/large)
- [ ] Scope items stated in unambiguous, testable terms (medium/large)
- [ ] Scope change process defined (large)
- [ ] Timeline constraint documented with target dates
- [ ] Technology constraints documented (medium/large)
- [ ] Regulatory constraints documented or explicitly stated as none (medium/large)
- [ ] Staffing constraints documented (medium/large)
- [ ] Constraint impact assessments documented (large)
- [ ] Constraint mitigation strategies documented (large)
- [ ] Project Sponsor named with title and department
- [ ] Product Owner named with title and department
- [ ] Business Analyst named with title and department (medium/large)
- [ ] Technical Lead named with title and department (medium/large)
- [ ] Responsibilities documented per role (medium/large)
- [ ] Decision authority documented per role (large)
- [ ] Backup/delegate assigned per core role (large)
- [ ] RACI matrix included (large)
- [ ] Project scale formally determined (medium/large)
- [ ] Scale classification criteria correctly applied
- [ ] Classification data points documented (medium/large)
- [ ] Borderline justification provided if applicable (medium/large)
- [ ] Scale determination approved by Sponsor (medium/large)
- [ ] Project Sponsor approval recorded with date, name, role
- [ ] Product Owner approval recorded with date, name, role
- [ ] Technical Lead approval recorded with date, name, role (medium/large)

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Project Charter Development Runbook | Runbook | [../runbooks/project-charter-runbook.md](../runbooks/project-charter-runbook.md) |
| Project Charter Template | Template | [../templates/project-charter-template.md](../templates/project-charter-template.md) |
| RACI Matrix Template | Template | [../templates/raci-matrix-template.md](../templates/raci-matrix-template.md) |
| Business Case Standard | Standard | [business-case-standard.md](business-case-standard.md) |
| Stakeholder Management Standard | Standard | [stakeholder-management-standard.md](stakeholder-management-standard.md) |
