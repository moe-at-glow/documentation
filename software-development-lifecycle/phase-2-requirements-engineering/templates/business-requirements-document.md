# Business Requirements Document (BRD)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-BRD |
| **When to Use** | Capture and formalize business needs before deriving software requirements |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **SLA** | 5 business days from stakeholder interviews complete |
| **Runbook** | [Extract Business Requirements](../runbooks/extract-business-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 6 (Business Rules), 8 (Dependencies), and 9 (Glossary) are optional. Stakeholder Summary may be inline (skip separate Stakeholder Analysis).
> **IF** medium project (3-5 devs) **THEN** All sections required; Glossary optional if domain is well-understood.
> **IF** large project (6+ devs) **THEN** Full template required.

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Document Title | [Project Name] -- Business Requirements Document |
| Version | 1.0 |
| Status | Draft / Under Review / Approved / Baselined |
| Author | [Name] |
| Date Created | YYYY-MM-DD |
| Last Updated | YYYY-MM-DD |

### [ ] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | YYYY-MM-DD | [Name] | Initial draft |
| | | | |

### [ ] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| [Name] | Project Sponsor | | |
| [Name] | Product Owner | | |
| [Name] | Tech Lead | | |

---

## [ ] 1. Executive Summary

<!-- 2-3 paragraphs: business need, proposed solution, expected outcomes -->

[Executive summary here]

---

## [ ] 2. Business Objectives

| ID | Objective | Success Metric | Target |
|----|-----------|---------------|--------|
| OBJ-001 | [Objective description] | [How success is measured] | [Target value] |
| OBJ-002 | | | |
| OBJ-003 | | | |

---

## [ ] 3. Project Scope

### [ ] In Scope

| Item | Description |
|------|-------------|
| [Feature/capability] | [Brief description] |
| | |

### [ ] Out of Scope

| Item | Reason |
|------|--------|
| [Feature/capability] | [Why it is excluded] |
| | |

---

## [ ] 4. Stakeholder Summary

<!-- Brief summary here; link to full Stakeholder Analysis for details -->

| ID | Name | Role | Interest Level | Influence Level | Key Concerns |
|----|------|------|---------------|-----------------|-------------|
| SH-001 | [Name] | [Role] | High/Medium/Low | High/Medium/Low | [Primary concerns] |
| | | | | | |

Full stakeholder analysis: [Link to Stakeholder Analysis document]

---

## [ ] 5. Business Requirements

<!-- Use MoSCoW priority: M=Must, S=Should, C=Could, W=Won't -->

| ID | Title | Description | Priority | Source | Rationale | Acceptance Criteria | Status |
|----|-------|-------------|----------|--------|-----------|-------------------|--------|
| BR-001 | [Short name] | The business shall [capability] | M/S/C/W | [Stakeholder/document] | [Why this is needed] | [Measurable conditions] | Draft |
| BR-002 | | | | | | | |
| BR-003 | | | | | | | |

---

## [ ] 6. Business Rules

| Rule ID | Description | Source | Affected Requirements |
|---------|-------------|--------|----------------------|
| RULE-001 | [Business rule statement] | [Policy/regulation/stakeholder] | BR-XXX, BR-XXX |
| | | | |

---

## [ ] 7. Assumptions and Constraints

### [ ] Assumptions

| ID | Assumption | Impact if Wrong |
|----|-----------|-----------------|
| ASM-001 | [Assumption statement] | [What happens if this assumption is invalid] |
| | | |

### [ ] Constraints

| ID | Constraint | Type | Impact |
|----|-----------|------|--------|
| CON-001 | [Constraint statement] | Schedule/Technical/Regulatory | [How it limits the project] |
| | | | |

---

## [ ] 8. Dependencies

| ID | Dependency | Type | Owner | Status |
|----|-----------|------|-------|--------|
| DEP-001 | [What is depended upon] | Internal/External | [Who owns it] | Open/Resolved |
| | | | | |

---

## [ ] 9. Glossary

| Term | Definition |
|------|-----------|
| [Term] | [Definition specific to this project] |
| | |

---

## [ ] 10. Approval Sign-Off

| Name | Role | Decision (Approve/Reject) | Comments | Date |
|------|------|--------------------------|----------|------|
| | Project Sponsor | | | |
| | Product Owner | | | |
| | Tech Lead | | | |

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Reviewed by Product Owner
- [ ] Approved by Project Sponsor
- [ ] Stored in project SharePoint / repository
- [ ] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Extract Business Requirements](../runbooks/extract-business-requirements.md) |
| Stakeholder Analysis | [Stakeholder Analysis Template](stakeholder-analysis-template.md) |
| Software Requirements Specification | [SRS Template](software-requirements-specification.md) |
| Requirements Traceability Matrix | [RTM Template](requirements-traceability-matrix.md) |
