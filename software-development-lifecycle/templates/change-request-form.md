# Change Request Form

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-CRF |
| **When to Use** | Propose a change to baselined requirements, scope, or design |
| **Owner** | Requestor (any role) |
| **Reviewer** | Change Control Board (Product Owner + Tech Lead) |
| **SLA** | 3 business days for initial review; 5 business days for impact analysis |
| **Runbook** | [Manage Requirements Changes](../runbooks/manage-requirements-changes.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Cost Impact and Technical Impact sections are optional. Impact Analysis may be a single summary paragraph.
> **IF** medium project (3-5 devs) **THEN** All sections required; Cost Impact may omit line-item breakdown.
> **IF** large project (6+ devs) **THEN** Full template required.

---

## [ ] Change Request

| Field | Value |
|-------|-------|
| Change Request ID | CR-XXX |
| Date Submitted | YYYY-MM-DD |
| Requestor | [Name, Role] |
| Project | [Project Name] |
| Priority | Critical / High / Medium / Low |
| Status | Submitted / Under Review / Approved / Rejected / Deferred / Closed |

---

## [ ] Affected Requirements

| Requirement ID | Current Description | Proposed Change |
|---------------|-------------------|-----------------|
| [BR/SWR-XXX] | [Current requirement text] | [What changes] |
| | | |

---

## [ ] Change Description

<!-- Be specific: what is added, modified, or removed -->

[Change description here]

---

## [ ] Justification / Business Reason

<!-- Reference business objectives, stakeholder feedback, regulatory changes, or defects -->

[Justification here]

---

## [ ] Impact Analysis

### [ ] Scope Impact

| Aspect | Impact | Details |
|--------|--------|---------|
| New requirements | [Count] | [List new requirement IDs if known] |
| Modified requirements | [Count] | [List affected requirement IDs] |
| Removed requirements | [Count] | [List affected requirement IDs] |
| New features | [Yes/No] | [Description] |
| Overall scope | Increase / Decrease / Neutral | [Summary] |

### [ ] Schedule Impact

| Aspect | Impact | Details |
|--------|--------|---------|
| Estimated effort | [Person-days] | [Breakdown by role if needed] |
| Affected sprints | [Sprint numbers] | |
| Delivery date impact | No change / Delayed by [duration] | |

### [ ] Cost Impact

| Aspect | Impact | Details |
|--------|--------|---------|
| Development cost | [Amount or effort] | |
| Infrastructure cost | [Amount] | |
| Licensing cost | [Amount] | |
| Total estimated cost | [Amount] | |

### [ ] Risk Impact

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk description] | High/Med/Low | High/Med/Low | [Mitigation plan] |
| | | | |

### [ ] Technical Impact

| Aspect | Impact | Details |
|--------|--------|---------|
| Architecture changes | Yes / No | [Description] |
| Database changes | Yes / No | [Description] |
| Integration changes | Yes / No | [Description] |
| Infrastructure changes | Yes / No | [Description] |

---

## [ ] Affected Artifacts

| Artifact | Change Required |
|----------|----------------|
| BRD | [Yes/No -- description] |
| SRS | [Yes/No -- description] |
| RTM | [Yes/No -- description] |
| Design documents | [Yes/No -- description] |
| Test cases | [Yes/No -- description] |
| User documentation | [Yes/No -- description] |

---

## [ ] Decision

| Field | Value |
|-------|-------|
| Decision | Approve / Reject / Defer |
| Decision Date | YYYY-MM-DD |
| Decision Authority | [Name(s) and role(s)] |

### [ ] Rationale

[Explain why this decision was made]

### [ ] Conditions (if applicable)

[Any conditions attached to the approval, e.g., "Approved for Phase 2 only"]

---

## [ ] Implementation Notes

| Field | Value |
|-------|-------|
| Target Release / Sprint | [Release or sprint number] |
| Assigned To | [Name] |
| Implementation Date | YYYY-MM-DD |
| Verified By | [Name] |
| Verification Date | YYYY-MM-DD |

---

## [ ] Sign-Off

| Name | Role | Decision | Date |
|------|------|----------|------|
| [Name] | Product Owner | | |
| [Name] | Tech Lead | | |
| [Name] | QA Lead | | |
| [Name] | Project Sponsor (if high impact) | | |

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Impact analysis completed
- [ ] Reviewed by Change Control Board (Product Owner + Tech Lead)
- [ ] Approved by Decision Authority
- [ ] Stored in project SharePoint / repository
- [ ] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Manage Requirements Changes](../runbooks/manage-requirements-changes.md) |
| Business Requirements Document | [BRD Template](business-requirements-document.md) |
| Software Requirements Specification | [SRS Template](software-requirements-specification.md) |
| Requirements Traceability Matrix | [RTM Template](requirements-traceability-matrix.md) |
