# Requirements Classification Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P2-003 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Business Analyst |
| **Verification Method** | Requirements attribute audit at baseline review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Functional/non-functional and MoSCoW classification required; risk and source classification recommended
> **IF** medium project (3-5 devs) **THEN** All classifications required
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Functional vs Non-Functional Classification

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Every requirement classified as Functional or Non-Functional | All requirements | [ ] Audit classification attribute on every requirement | Requirement blocked from Approved status |
| 2 | Functional: defines what the system must do (behavior, features, operations) | Functional requirements | [ ] Verify description states system behavior | Reclassify or rewrite |
| 3 | Non-Functional: defines how the system must perform (quality attributes, constraints) | Non-functional requirements | [ ] Verify description states quality attribute or constraint | Reclassify or rewrite |

### Non-Functional Requirement Categories

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 4 | Non-functional requirements categorized into: Performance, Security, Usability, Reliability, Scalability, Maintainability, or Compliance | All non-functional requirements | [ ] Verify NFR category attribute is set to valid value | Requirement blocked from Approved status |
| 5 | Performance requirements specify measurable thresholds (response time, throughput, resource usage) | Performance NFRs | [ ] Verify numeric threshold present | Rework with measurable criteria |
| 6 | Security requirements specify authentication, authorization, data protection, or audit controls | Security NFRs | [ ] Verify security control specified | Rework with specific control |
| 7 | Usability requirements specify measurable user experience criteria | Usability NFRs | [ ] Verify measurable UX criterion present | Rework with measurable criteria |
| 8 | Reliability requirements specify availability, fault tolerance, or recoverability targets | Reliability NFRs | [ ] Verify numeric target present | Rework with measurable target |
| 9 | Scalability requirements specify load or growth capacity | Scalability NFRs | [ ] Verify capacity number present | Rework with measurable capacity |
| 10 | Maintainability requirements specify modularity, testability, or modifiability targets | Maintainability NFRs | [ ] Verify measurable target present | Rework with measurable target |
| 11 | Compliance requirements cite specific regulation, law, or contractual obligation | Compliance NFRs | [ ] Verify regulatory reference present | Rework with specific citation |

### Priority Classification (MoSCoW)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 12 | Every requirement assigned MoSCoW priority: Must Have (M), Should Have (S), Could Have (C), or Won't Have (W) | All requirements | [ ] Audit priority attribute on every requirement | Requirement blocked from Approved status |
| 13 | Must Have: essential for release viability; cannot be descoped | M-priority requirements | [ ] Verify business criticality justification | Priority reassessed by Product Owner |
| 14 | Should Have: important but deferrable with Product Owner approval | S-priority requirements | [ ] Verify deferral conditions documented | Priority reassessed by Product Owner |
| 15 | Could Have: included only if time and budget allow | C-priority requirements | [ ] Verify no hard dependency on this requirement | Priority reassessed by Product Owner |
| 16 | Won't Have: explicitly excluded; documented to prevent scope creep | W-priority requirements | [ ] Verify exclusion documented in backlog | Scope creep risk flagged |
| 17 | Distribution guideline: approximately 60% Must Have, 20% Should Have, 20% Could Have | Release scope | [ ] Calculate MoSCoW distribution at baseline | Imbalance flagged to Product Owner for review |

### Risk Classification

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 18 | Every requirement assigned risk level: High, Medium, or Low | All requirements | [ ] Audit risk attribute on every requirement | Requirement blocked from Approved status |
| 19 | High risk: spike or proof of concept required; architecture review mandatory | High-risk requirements | [ ] Verify spike/PoC completed and architecture review conducted | Implementation blocked until spike complete |
| 20 | Medium risk: tech lead review required; mitigation plan identified | Medium-risk requirements | [ ] Verify tech lead review and mitigation plan documented | Implementation blocked until review complete |
| 21 | Low risk: standard development and review process | Low-risk requirements | [ ] Verify standard process followed | N/A |

### Source Classification

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 22 | Every requirement has at least one source classification: Stakeholder, Regulatory, Technical, or Business | All requirements | [ ] Audit source classification attribute | Requirement blocked from Approved status |
| 23 | Stakeholder source: originates from person/group with interest in the system | Stakeholder-sourced | [ ] Verify named stakeholder recorded | Source clarified before approval |
| 24 | Regulatory source: required by law, regulation, or industry standard | Regulatory-sourced | [ ] Verify specific regulation cited | Regulation reference added before approval |
| 25 | Technical source: arises from technical constraints or architecture decisions | Technical-sourced | [ ] Verify technical constraint or ADR referenced | Technical reference added before approval |
| 26 | Business source: derived from business strategy, goals, or market requirements | Business-sourced | [ ] Verify business objective referenced | Business reference added before approval |

---

## COMPLIANCE CHECKLIST

- [ ] Every requirement classified as Functional or Non-Functional
- [ ] Every non-functional requirement assigned a valid NFR category
- [ ] All NFR categories include measurable thresholds or specific citations
- [ ] Every requirement assigned MoSCoW priority (M/S/C/W)
- [ ] MoSCoW distribution reviewed (target: 60% M, 20% S, 20% C)
- [ ] Every requirement assigned risk level (High/Medium/Low)
- [ ] High-risk requirements have completed spikes and architecture reviews
- [ ] Medium-risk requirements have tech lead review and mitigation plans
- [ ] Every requirement has at least one source classification
- [ ] All source classifications include specific references (stakeholder name, regulation, ADR, business objective)

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| SDLC Framework Standard | Standard | ../standards/sdlc-framework.md |
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
