# Stakeholder Register

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-003 |
| **When to Use** | To identify, classify, and plan communication for all project stakeholders |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **SLA** | 3 business days |
| **Runbook** | [Conduct Initial Stakeholder Identification](../runbooks/conduct-initial-stakeholder-identification.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Stakeholder Register table required; Communication Plan table optional
> **IF** medium project (3-5 devs) **THEN** Both tables required; simplified Communication Plan (combine stakeholder groups)
> **IF** large project (6+ devs) **THEN** Full template required with detailed per-group communication plan

---

### [ ] Project Information

| Field | Value |
|-------|-------|
| **Project Name** | _[Enter project name]_ |
| **Date** | _[YYYY-MM-DD]_ |
| **Author** | _[Name, Role]_ |
| **Version** | _[e.g., 1.0]_ |

---

### [ ] Stakeholder Register

| ID | Name | Role / Title | Organization | Category | Power Level | Interest Level | Classification | Key Concerns | Communication Preference | Contact |
|----|------|-------------|--------------|----------|-------------|----------------|----------------|--------------|--------------------------|---------|
| SH-001 | _[Name]_ | _[Role/Title]_ | _[Org/Dept]_ | _[Internal/External]_ | _[High/Medium/Low]_ | _[High/Medium/Low]_ | _[Manage Closely/Keep Satisfied/Keep Informed/Monitor]_ | _[Primary concerns]_ | _[Email/Meeting/Report/Slack]_ | _[Email/Phone]_ |
| SH-002 | _[Name]_ | _[Role/Title]_ | _[Org/Dept]_ | _[Internal/External]_ | _[High/Medium/Low]_ | _[High/Medium/Low]_ | _[Manage Closely/Keep Satisfied/Keep Informed/Monitor]_ | _[Primary concerns]_ | _[Email/Meeting/Report/Slack]_ | _[Email/Phone]_ |
| SH-003 | _[Name]_ | _[Role/Title]_ | _[Org/Dept]_ | _[Internal/External]_ | _[High/Medium/Low]_ | _[High/Medium/Low]_ | _[Manage Closely/Keep Satisfied/Keep Informed/Monitor]_ | _[Primary concerns]_ | _[Email/Meeting/Report/Slack]_ | _[Email/Phone]_ |
| SH-004 | _[Name]_ | _[Role/Title]_ | _[Org/Dept]_ | _[Internal/External]_ | _[High/Medium/Low]_ | _[High/Medium/Low]_ | _[Manage Closely/Keep Satisfied/Keep Informed/Monitor]_ | _[Primary concerns]_ | _[Email/Meeting/Report/Slack]_ | _[Email/Phone]_ |
| SH-005 | _[Name]_ | _[Role/Title]_ | _[Org/Dept]_ | _[Internal/External]_ | _[High/Medium/Low]_ | _[High/Medium/Low]_ | _[Manage Closely/Keep Satisfied/Keep Informed/Monitor]_ | _[Primary concerns]_ | _[Email/Meeting/Report/Slack]_ | _[Email/Phone]_ |

**Power/Interest Classification Matrix:**

| | Low Interest | High Interest |
|---|-------------|---------------|
| **High Power** | Keep Satisfied | Manage Closely |
| **Low Power** | Monitor | Keep Informed |

---

### [ ] Communication Plan

| Stakeholder Group | Method | Frequency | Content | Owner |
|-------------------|--------|-----------|---------|-------|
| Manage Closely (High Power / High Interest) | _[1:1 Meeting / Steering Committee]_ | _[Weekly / Bi-weekly]_ | _[Detailed status, decisions, risks]_ | _[Name]_ |
| Keep Satisfied (High Power / Low Interest) | _[Executive Summary / Email]_ | _[Bi-weekly / Monthly]_ | _[High-level status, milestone progress, escalations]_ | _[Name]_ |
| Keep Informed (Low Power / High Interest) | _[Status Report / Newsletter]_ | _[Weekly / Bi-weekly]_ | _[Progress updates, upcoming changes, impact assessment]_ | _[Name]_ |
| Monitor (Low Power / Low Interest) | _[Email / Dashboard]_ | _[Monthly / As needed]_ | _[Major milestones, project-wide announcements]_ | _[Name]_ |

---

### [ ] Stakeholder Change Log

| Date | Stakeholder ID | Change Description | Updated By |
|------|---------------|-------------------|------------|
| _[YYYY-MM-DD]_ | _[SH-XXX]_ | _[What changed and why]_ | _[Name]_ |
| _[YYYY-MM-DD]_ | _[SH-XXX]_ | _[What changed and why]_ | _[Name]_ |

---

## COMPLETION CHECKLIST

- [ ] All known stakeholders identified and registered
- [ ] Power and interest levels assessed for each stakeholder
- [ ] Classifications assigned using Power/Interest matrix
- [ ] Key concerns documented for each stakeholder
- [ ] Communication preferences captured
- [ ] Communication plan defined for each stakeholder group
- [ ] Reviewed by Product Owner

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Initial Stakeholder Identification | Runbook | [../runbooks/conduct-initial-stakeholder-identification.md](../runbooks/conduct-initial-stakeholder-identification.md) |
| Business Case | Template | [business-case-template.md](business-case-template.md) |
| Project Charter | Template | [project-charter-template.md](project-charter-template.md) |
