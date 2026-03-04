# Stakeholder Analysis

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-SHA |
| **When to Use** | Identify, classify, and plan engagement for all project stakeholders |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **SLA** | 3 business days from project kickoff |
| **Runbook** | [Conduct Stakeholder Analysis](../runbooks/conduct-stakeholder-analysis.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 2 (Power/Interest Grid) and 3 (Communication Plan) are optional; inline stakeholder notes in the BRD may suffice.
> **IF** medium project (3-5 devs) **THEN** All sections required; Communication Plan may be simplified to key stakeholders only.
> **IF** large project (6+ devs) **THEN** Full template required.

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Project | [Project Name] |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Version | 1.0 |

---

## [ ] 1. Stakeholder Register

| ID | Name | Role / Title | Organization / Department | Contact | Influence | Interest | Classification |
|----|------|-------------|--------------------------|---------|-----------|----------|----------------|
| SH-001 | [Name] | [Role] | [Dept/Company] | [Email] | High/Med/Low | High/Med/Low | [See grid below] |
| SH-002 | | | | | | | |
| SH-003 | | | | | | | |
| SH-004 | | | | | | | |
| SH-005 | | | | | | | |

---

## [ ] 2. Power/Interest Grid

```
                        INTEREST
              Low                    High
         +--------------------+--------------------+
         |                    |                    |
   High  |   KEEP SATISFIED   |  MANAGE CLOSELY   |
         |                    |                    |
P        +--------------------+--------------------+
O        |                    |                    |
W  Low   |   MONITOR          |  KEEP INFORMED    |
E        |                    |                    |
R        +--------------------+--------------------+
```

### [ ] Stakeholder Placement

| Classification | Stakeholders |
|---------------|-------------|
| Manage Closely (High Power, High Interest) | [SH-001, SH-003, ...] |
| Keep Satisfied (High Power, Low Interest) | [SH-005, ...] |
| Keep Informed (Low Power, High Interest) | [SH-002, ...] |
| Monitor (Low Power, Low Interest) | [SH-004, ...] |

---

## [ ] 3. Communication Plan

| Stakeholder Group | Communication Method | Frequency | Content | Owner | Notes |
|-------------------|---------------------|-----------|---------|-------|-------|
| Manage Closely | 1:1 Meeting | Weekly | Status, risks, decisions | [Name] | |
| Keep Satisfied | Executive Summary | Monthly | Key milestones, budget | [Name] | |
| Keep Informed | Status Report / Email | Bi-weekly | Progress, upcoming changes | [Name] | |
| Monitor | Newsletter / Announcement | Quarterly | Major milestones only | [Name] | |

---

## [ ] 4. Stakeholder Concerns and Expectations

| ID | Stakeholder | Key Concerns | Expectations | Potential Risks | Mitigation |
|----|-------------|-------------|-------------|----------------|------------|
| SH-001 | [Name] | [What worries them] | [What they expect from the project] | [Risk if not managed] | [How to mitigate] |
| SH-002 | | | | | |
| SH-003 | | | | | |

---

## [ ] 5. Sign-Off

| Name | Role | Date |
|------|------|------|
| [Name] | Product Owner | |
| [Name] | Project Sponsor | |

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
| Producing Runbook | [Conduct Stakeholder Analysis](../runbooks/conduct-stakeholder-analysis.md) |
| Business Requirements Document | [BRD Template](business-requirements-document.md) |
| Change Request Form | [Change Request Form](change-request-form.md) |
