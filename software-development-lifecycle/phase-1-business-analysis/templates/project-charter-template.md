# Project Charter

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-002 |
| **When to Use** | To formally authorize a project by defining objectives, scope, constraints, roles, and governance |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **Approver** | Project Sponsor |
| **SLA** | 5 business days |
| **Runbook** | [Create Project Charter](../runbooks/create-project-charter.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Project Name, Sponsor, Objectives, High-Level Scope, Key Roles, Project Scale, Success Criteria, Authorization required only
> **IF** medium project (3-5 devs) **THEN** All sections except Communication Plan (use informal channels)
> **IF** large project (6+ devs) **THEN** Full template required

---

### [ ] Project Name

| Field | Value |
|-------|-------|
| **Project Name** | _[Enter project name]_ |
| **Project ID** | _[Enter project identifier]_ |
| **Version** | _[e.g., 1.0]_ |
| **Date** | _[YYYY-MM-DD]_ |

---

### [ ] Project Sponsor

| Field | Value |
|-------|-------|
| **Name** | _[Sponsor name]_ |
| **Title** | _[Sponsor title]_ |
| **Department** | _[Department]_ |
| **Contact** | _[Email / Phone]_ |

---

### [ ] Product Owner

| Field | Value |
|-------|-------|
| **Name** | _[Product Owner name]_ |
| **Title** | _[Title]_ |
| **Department** | _[Department]_ |
| **Contact** | _[Email / Phone]_ |

---

### [ ] Business Analyst

| Field | Value |
|-------|-------|
| **Name** | _[Business Analyst name]_ |
| **Title** | _[Title]_ |
| **Department** | _[Department]_ |
| **Contact** | _[Email / Phone]_ |

---

### [ ] Project Objectives

| # | Objective | Measurable Outcome | Priority |
|---|-----------|-------------------|----------|
| 1 | _[Objective description]_ | _[How success is measured]_ | _[Must Have / Should Have / Nice to Have]_ |
| 2 | _[Objective description]_ | _[How success is measured]_ | _[Must Have / Should Have / Nice to Have]_ |
| 3 | _[Objective description]_ | _[How success is measured]_ | _[Must Have / Should Have / Nice to Have]_ |

---

### [ ] High-Level Scope

**In-Scope:**

| # | Item | Description |
|---|------|-------------|
| 1 | _[Item]_ | _[Description]_ |
| 2 | _[Item]_ | _[Description]_ |
| 3 | _[Item]_ | _[Description]_ |

**Out-of-Scope:**

| # | Item | Rationale |
|---|------|-----------|
| 1 | _[Item]_ | _[Why excluded]_ |
| 2 | _[Item]_ | _[Why excluded]_ |
| 3 | _[Item]_ | _[Why excluded]_ |

---

### [ ] Constraints

| Constraint Type | Description | Impact |
|----------------|-------------|--------|
| **Timeline** | _[Hard deadlines, regulatory dates, market windows]_ | _[Impact if missed]_ |
| **Technology** | _[Required platforms, languages, integrations, standards]_ | _[Impact on design]_ |
| **Regulatory** | _[Compliance requirements, data residency, certifications]_ | _[Impact on scope]_ |
| **Staffing** | _[Team availability, skill gaps, shared resources]_ | _[Impact on delivery]_ |

---

### [ ] Assumptions

| # | Assumption | Impact if Invalid | Validation Method |
|---|-----------|-------------------|-------------------|
| 1 | _[Assumption description]_ | _[What happens if wrong]_ | _[How to validate]_ |
| 2 | _[Assumption description]_ | _[What happens if wrong]_ | _[How to validate]_ |
| 3 | _[Assumption description]_ | _[What happens if wrong]_ | _[How to validate]_ |
| 4 | _[Assumption description]_ | _[What happens if wrong]_ | _[How to validate]_ |

---

### [ ] High-Level Milestones

| # | Milestone | Target Date | Exit Criteria |
|---|-----------|-------------|---------------|
| 1 | Phase 1: Business Analysis Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |
| 2 | Phase 2: Requirements Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |
| 3 | Phase 3: Design Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |
| 4 | Phase 4: Development Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |
| 5 | Phase 5: Testing Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |
| 6 | Phase 6: Deployment Complete | _[YYYY-MM-DD]_ | _[Criteria]_ |

---

### [ ] Key Roles and Responsibilities

| Role | Name | Responsibilities | Availability |
|------|------|-----------------|--------------|
| Project Sponsor | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| Product Owner | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| Business Analyst | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| Tech Lead | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| QA Lead | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| DevOps Lead | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |
| _[Additional Role]_ | _[Name]_ | _[Key responsibilities]_ | _[% allocation]_ |

---

### [ ] Communication Plan

| Audience | Method | Frequency | Content | Owner |
|----------|--------|-----------|---------|-------|
| Project Team | _[Stand-up / Slack]_ | _[Daily]_ | _[Progress, blockers]_ | _[Name]_ |
| Stakeholders | _[Status Report / Email]_ | _[Weekly]_ | _[Milestones, risks, decisions]_ | _[Name]_ |
| Sponsor | _[Steering Committee]_ | _[Bi-weekly / Monthly]_ | _[Timeline, escalations, decisions]_ | _[Name]_ |
| Leadership | _[Executive Summary]_ | _[Monthly]_ | _[High-level status, value delivery]_ | _[Name]_ |

**Escalation Path:**

| Level | Escalation Trigger | Escalate To | Response SLA |
|-------|-------------------|-------------|--------------|
| 1 | _[Trigger]_ | _[Role/Name]_ | _[Timeframe]_ |
| 2 | _[Trigger]_ | _[Role/Name]_ | _[Timeframe]_ |
| 3 | _[Trigger]_ | _[Role/Name]_ | _[Timeframe]_ |

---

### [ ] Project Scale

| Field | Value |
|-------|-------|
| **Team Size** | _[Number of developers]_ |
| **Classification** | _[Small (1-2 devs) / Medium (3-5 devs) / Large (6+ devs)]_ |
| **Estimated Duration** | _[Weeks / Months]_ |
| **Estimated Effort** | _[Person-days / Person-months]_ |

**Scaling Implications per SDLC Framework:**

| Area | Small | Medium | Large |
|------|-------|--------|-------|
| Documentation | Lightweight | Standard | Comprehensive |
| Reviews | Peer review | Formal review | Review board |
| Testing | Unit + integration | + E2E | + Performance + Security |
| Governance | Minimal gates | Standard gates | Full gate reviews |

---

### [ ] Success Criteria

| # | Criterion | Metric | Target | Measurement Method |
|---|----------|--------|--------|--------------------|
| 1 | _[Criterion description]_ | _[Metric name]_ | _[Target value]_ | _[How measured]_ |
| 2 | _[Criterion description]_ | _[Metric name]_ | _[Target value]_ | _[How measured]_ |
| 3 | _[Criterion description]_ | _[Metric name]_ | _[Target value]_ | _[How measured]_ |

---

### [ ] Authorization

| Field | Value |
|-------|-------|
| **Sponsor Name** | _[Name]_ |
| **Sponsor Signature** | _[Signature]_ |
| **Date** | _[YYYY-MM-DD]_ |
| **Decision** | _[Authorized / Not Authorized / Deferred]_ |

**Conditions of Authorization:**

_[Enter any conditions or limitations placed on the authorization]_

**Distribution List:**

| # | Name | Role | Date Distributed |
|---|------|------|-----------------|
| 1 | _[Name]_ | _[Role]_ | _[YYYY-MM-DD]_ |
| 2 | _[Name]_ | _[Role]_ | _[YYYY-MM-DD]_ |
| 3 | _[Name]_ | _[Role]_ | _[YYYY-MM-DD]_ |

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Project objectives are measurable
- [ ] Scope boundaries clearly defined
- [ ] All constraints identified and documented
- [ ] Assumptions validated where possible
- [ ] Key roles assigned with confirmed availability
- [ ] Project scale classification confirmed
- [ ] Reviewed by Product Owner
- [ ] Approved by Project Sponsor

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Project Charter | Runbook | [../runbooks/create-project-charter.md](../runbooks/create-project-charter.md) |
| Business Case | Template | [business-case-template.md](business-case-template.md) |
| Stakeholder Register | Template | [stakeholder-register-template.md](stakeholder-register-template.md) |
