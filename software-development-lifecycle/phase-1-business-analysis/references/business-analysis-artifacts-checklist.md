# Business Analysis Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P1-001 |
| **Use When** | Determining which Phase 1 artifacts are required for a project and verifying completeness before Phase 1 gate review |
| **Last Updated** | 2026-03-04 |

---

## ARTIFACT REGISTER

| Artifact | Description | Owner | Format | Required | Approval Authority |
|----------|-------------|-------|--------|----------|--------------------|
| Business Case | Justification for the project including problem, proposed solution, business value assessment, and strategic alignment | Business Analyst | Document (Markdown/PDF) | Yes | Project Sponsor |
| Project Charter | Formal authorization defining scope, objectives, constraints, assumptions, and high-level timeline | Product Owner | Document (Markdown/PDF) | Yes | Project Sponsor |
| Stakeholder Register | Catalog of all identified stakeholders with roles, influence, interest, communication preferences, and engagement strategy | Business Analyst | Spreadsheet/Table | Yes | Product Owner |
| Problem Statement | Concise description of the business problem: who is affected, what the problem is, and the measurable impact | Business Analyst | Document (Markdown/PDF) | Yes | Product Owner |
| Business Value Assessment | Qualitative impact analysis including value categories, impact levels, efficiency metrics, and value realization timeline | Business Analyst | Document (Markdown/PDF) | Conditional (see decision tree) | Project Sponsor |

---

## ARTIFACT DETAIL -- FORMAT AND CONTENT

| Artifact | Required Sections | Minimum Length | Review Cycle |
|----------|-------------------|----------------|--------------|
| Business Case | Problem Statement, Proposed Solution, Strategic Alignment, Business Value Assessment, Risk Summary, Recommendation | 3-5 pages | 1 review before gate |
| Project Charter | Purpose, Scope, Objectives, Constraints, Assumptions, Stakeholders, High-Level Timeline, Approval Signatures | 2-3 pages | 1 review before gate |
| Stakeholder Register | Name, Role, Organization, Influence (H/M/L), Interest (H/M/L), Communication Preference, Engagement Level | 1 entry per stakeholder | Updated continuously |
| Problem Statement | Who, What Problem, What Impact, Current State, Desired State, Measurable Gap | 0.5-1 page | 1 review by Product Owner |
| Business Value Assessment | Value Categories, Impact Assessment, Efficiency Metrics, Value Realization Timeline (if applicable), Assumptions | 2-4 pages | 1 review before gate |

---

## COMPLETION CHECKLIST

### Business Case
- [ ] Problem statement included and validated
- [ ] Proposed solution(s) described with rationale
- [ ] Strategic alignment to organizational goals documented
- [ ] Business value assessment included (or cross-referenced to standalone assessment)
- [ ] Key risks identified with preliminary mitigation
- [ ] Recommendation stated with supporting evidence
- [ ] Project Sponsor approval obtained

### Project Charter
- [ ] Project purpose and justification stated
- [ ] Scope defined (in-scope and out-of-scope)
- [ ] SMART objectives defined
- [ ] Constraints and assumptions documented
- [ ] High-level timeline with milestones established
- [ ] Key stakeholders listed
- [ ] Project Sponsor signature obtained

### Stakeholder Register
- [ ] All known stakeholders identified
- [ ] Influence and interest levels assessed for each stakeholder
- [ ] Communication preferences documented
- [ ] Engagement strategy defined per stakeholder
- [ ] Register reviewed by Product Owner

### Problem Statement
- [ ] Follows format: [Who] experiences [what problem] resulting in [what impact]
- [ ] Current state described
- [ ] Desired future state described
- [ ] Measurable gap between current and desired state defined
- [ ] Reviewed and confirmed by Product Owner

### Business Value Assessment
- [ ] At least two value categories assessed (efficiency gains, risk reduction, productivity, compliance, user experience)
- [ ] Impact levels assigned per value area (High / Medium / Low)
- [ ] Current state and expected improvement documented per value area
- [ ] Efficiency metrics documented where applicable
- [ ] Value realization timeline defined (medium/large projects)
- [ ] All assumptions documented
- [ ] Project Sponsor approval obtained

### Phase 1 Gate Readiness
- [ ] All required artifacts produced per project scale
- [ ] All artifacts reviewed by designated approval authority
- [ ] All approval signatures obtained
- [ ] Artifacts stored in designated repository
- [ ] Phase 1 gate review scheduled

---

## DECISION TREE

### Is This Artifact Required for My Project Size?

```
IF project scale is SMALL (1-2 developers)
    THEN required artifacts:
        - Business Case: YES (streamlined format, 1-2 pages)
        - Project Charter: YES (streamlined format, 1 page)
        - Stakeholder Register: YES (simplified, key stakeholders only)
        - Problem Statement: YES (included in Business Case, not standalone)
        - Business Value Assessment: NO (summary in Business Case is sufficient)

ELSE IF project scale is MEDIUM (3-5 developers)
    THEN required artifacts:
        - Business Case: YES (full format)
        - Project Charter: YES (full format)
        - Stakeholder Register: YES (full format)
        - Problem Statement: YES (standalone document)
        - Business Value Assessment: YES (standard depth)

ELSE IF project scale is LARGE (6+ developers)
    THEN required artifacts:
        - Business Case: YES (full format with executive summary)
        - Project Charter: YES (full format)
        - Stakeholder Register: YES (full format with engagement plan)
        - Problem Statement: YES (standalone document)
        - Business Value Assessment: YES (full depth with comprehensive impact analysis)
```

### Is the Phase 1 Gate Ready?

```
IF all required artifacts for project scale are produced
    AND all artifacts reviewed by designated approval authority
    AND all approval signatures obtained
    THEN Phase 1 gate is READY
ELSE
    THEN identify missing/unapproved artifacts → complete before scheduling gate review
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Business Needs Analysis | Runbook | ../runbooks/conduct-business-needs-analysis.md |
| Business Case Development | Runbook | ../runbooks/develop-business-case.md |
| Project Charter Creation | Runbook | ../runbooks/create-project-charter.md |
| Initial Stakeholder Identification | Runbook | ../runbooks/conduct-initial-stakeholder-identification.md |
| Business Value Assessment Reference | Reference | ./business-value-assessment-reference.md |
| Business Analysis RACI Matrix | Reference | ./business-analysis-raci-matrix.md |
| SDLC Framework Standard | Standard | ../../standards/sdlc-framework.md |
| Phase 1 Standards | Standard | ../standards/phase-1-standards.md |
| Stakeholder Analysis Template | Template | ../../phase-2-requirements-engineering/templates/stakeholder-analysis-template.md |
| Glossary | Reference | ../../phase-2-requirements-engineering/references/glossary.md |
