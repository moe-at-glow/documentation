# Develop Business Case

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P1-002 |
| **Owner** | Business Analyst |
| **Accountable** | Project Sponsor |
| **SLA** | 10 business days |
| **Escalation** | Project Sponsor |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Business Needs Analysis completed and approved (RB-P1-001)
- [ ] Problem statement validated by Project Sponsor
- [ ] Business impact data available (quantitative or qualitative)
- [ ] Key stakeholders identified and accessible for consultation

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Business value cannot be substantiated with available data | STOP. Request additional data or commission feasibility study | Project Sponsor |
| Strategic priorities shift making business need obsolete | STOP. Document change and close business case | Project Sponsor |
| Regulatory or legal impediment discovered | STOP. Engage Legal/Compliance team and pause until cleared | Project Sponsor |

---

## PROCEDURE

### Step 1: Define Scope Boundaries

| Action | Owner | SLA |
|--------|-------|-----|
| Establish clear in-scope and out-of-scope boundaries for the proposed solution | Business Analyst | 1 business day |

- [ ] In-scope items listed (features, processes, systems, user groups)
- [ ] Out-of-scope items explicitly listed with rationale
- [ ] Scope boundaries reviewed with Product Owner
- [ ] Assumptions and constraints documented

> **IF** scope boundaries are disputed among stakeholders **THEN** escalate to Product Owner for resolution within 1 business day
> **ELSE** proceed with agreed scope boundaries

### Step 2: Assess Business Value

| Action | Owner | SLA |
|--------|-------|-----|
| Identify and assess qualitative business value across relevant value categories | Business Analyst | 2 business days |

- [ ] Efficiency gains identified (process automation, cycle time reduction, resource optimization)
- [ ] Risk reduction benefits identified (compliance, security, operational stability)
- [ ] Productivity improvements identified (team capacity, quality improvement, knowledge access)
- [ ] Compliance benefits identified where applicable (regulatory alignment, audit readiness)
- [ ] User experience improvements identified where applicable (usability, accessibility, self-service)
- [ ] Impact level assigned per value area (High / Medium / Low)
- [ ] Current state and expected improvement documented per value area
- [ ] Value realization timeline defined (when value begins, ramp period, steady state)
- [ ] All assumptions documented with confidence levels

> **IF** no meaningful value areas can be identified **THEN** recommend no-go and escalate to Project Sponsor
> **ELSE** proceed with documented business value assessment

### Step 3: Assess Risks

| Action | Owner | SLA |
|--------|-------|-----|
| Identify and evaluate risks that could impact project success or business case assumptions | Business Analyst | 1 business day |

- [ ] Technical risks identified (technology maturity, integration complexity, skill gaps)
- [ ] Business risks identified (market change, regulatory change, stakeholder turnover)
- [ ] Delivery risks identified (timeline overrun, scope expansion, resource turnover)
- [ ] Operational risks identified (adoption, change management, support capacity)
- [ ] Each risk scored by probability (High/Medium/Low) and impact (High/Medium/Low)
- [ ] Mitigation strategies defined for High and Critical risks
- [ ] Risk register created

> **IF** any risk scores as High probability AND High impact **THEN** escalate to Project Sponsor before proceeding
> **ELSE** document risk register and proceed

### Step 4: Define Success Metrics and KPIs

| Action | Owner | SLA |
|--------|-------|-----|
| Establish measurable success criteria and key performance indicators for the initiative | Business Analyst | 1 business day |

- [ ] Primary KPIs defined (minimum 3, maximum 7)
- [ ] Each KPI includes: metric name, baseline value, target value, measurement method, measurement frequency
- [ ] Leading indicators identified (early signals of success or failure)
- [ ] Lagging indicators identified (outcome measures)
- [ ] KPI ownership assigned per metric
- [ ] Success criteria reviewed with Product Owner

> **IF** baseline data unavailable for any KPI **THEN** define baseline measurement plan and timeline
> **ELSE** document current baselines with data source

### Step 5: Draft Business Case Document

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all analysis into the formal business case document using the approved template | Business Analyst | 1 business day |

- [ ] Executive summary drafted (max 1 page)
- [ ] Problem statement included from RB-P1-001
- [ ] Scope boundaries documented
- [ ] Business value assessment documented with assumptions
- [ ] Risk assessment included
- [ ] Success metrics and KPIs included
- [ ] Recommendation stated (Proceed / Proceed with conditions / Do not proceed)
- [ ] Document formatted per business case template

> **IF** business case recommends "Do not proceed" **THEN** document rationale and present to Project Sponsor for final decision
> **ELSE** proceed to stakeholder review

### Step 6: Review with Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| Circulate draft business case to key stakeholders for review and feedback | Product Owner | 2 business days |

- [ ] Business case distributed to: Product Owner, Tech Lead, Domain Expert
- [ ] Review period communicated (minimum 2 business days)
- [ ] Feedback collected and consolidated
- [ ] Conflicts or disagreements in feedback identified
- [ ] Revisions applied to business case based on feedback
- [ ] Change log updated with revision summary

> **IF** stakeholder feedback introduces material changes to value assessment **THEN** re-execute Step 2 as needed
> **ELSE** incorporate feedback and proceed to sponsor approval

### Step 7: Obtain Sponsor Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Present final business case to Project Sponsor for formal approval decision | Business Analyst | 1 business day |

- [ ] Approval meeting scheduled with Project Sponsor
- [ ] Business case presented with executive summary, business value assessment, and recommendation
- [ ] Questions and concerns addressed
- [ ] Sponsor decision recorded (Approved / Approved with conditions / Rejected / Deferred)
- [ ] Approval signature or formal written confirmation obtained
- [ ] Decision communicated to all consulted and informed stakeholders

> **IF** sponsor approves with conditions **THEN** document conditions, assign owners, and set deadlines for condition resolution
> **ELSE IF** sponsor rejects **THEN** document rejection rationale, communicate to stakeholders, and close
> **ELSE IF** sponsor defers **THEN** document deferral criteria and schedule re-evaluation date
> **ELSE** proceed to exit criteria

---

## EXIT CRITERIA

- [ ] Business case document completed per template
- [ ] Business value assessment completed with documented assumptions
- [ ] Risk assessment completed with mitigation strategies for high risks
- [ ] Success metrics and KPIs defined with baselines and targets
- [ ] Business case approved by Project Sponsor (signature or written confirmation)
- [ ] Approval decision communicated to all stakeholders
- [ ] Business case stored in designated repository

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Business Case Document | [Business Case Template](../templates/business-case-template.md) | `project-repo/phase-1/business-case/` |
| Business Value Assessment | [Business Value Assessment Reference](../references/business-value-assessment-reference.md) | `project-repo/phase-1/business-case/` |
| Risk Register | [Risk Register Template](../templates/risk-register-template.md) | `project-repo/phase-1/risk-register/` |
| KPI Definition Sheet | [KPI Template](../templates/kpi-definition-template.md) | `project-repo/phase-1/kpis/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Needs Analysis | Runbook | [RB-P1-001](./conduct-business-needs-analysis.md) |
| Project Charter Creation | Runbook | [RB-P1-003](./create-project-charter.md) |
| Initial Stakeholder Identification | Runbook | [RB-P1-004](./conduct-initial-stakeholder-identification.md) |
| Business Case Template | Template | [../templates/business-case-template.md](../templates/business-case-template.md) |
| Phase 1 Standards | Standard | [../standards/phase-1-standards.md](../standards/phase-1-standards.md) |
