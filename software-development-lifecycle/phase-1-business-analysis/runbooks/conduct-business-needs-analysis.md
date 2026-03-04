# Conduct Business Needs Analysis

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P1-001 |
| **Owner** | Business Analyst |
| **Accountable** | Product Owner |
| **SLA** | 5 business days |
| **Escalation** | Project Sponsor |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Business need or opportunity identified by stakeholder
- [ ] Requesting stakeholder identified and available
- [ ] Initial business request submitted (email, ticket, or verbal with written follow-up)

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Requesting stakeholder unavailable for >3 business days | STOP. Reschedule and notify Product Owner | Product Owner |
| Business need duplicates an existing active initiative | STOP. Document overlap and redirect to existing initiative | Product Owner |
| Business need falls outside organizational strategic objectives | STOP. Document misalignment and return to stakeholder | Project Sponsor |
| Insufficient data to quantify business impact after reasonable effort | STOP. Request additional data sources from stakeholder | Project Sponsor |

---

## PROCEDURE

### Step 1: Receive Business Request

| Action | Owner | SLA |
|--------|-------|-----|
| Receive and log incoming business request in project intake system | Business Analyst | 1 business day |

- [ ] Business request logged with unique identifier
- [ ] Requesting stakeholder contact information recorded
- [ ] Initial request description captured verbatim

> **IF** request is informal (verbal or chat) **THEN** document in written form and obtain stakeholder confirmation
> **ELSE** file original written request as-is

### Step 2: Conduct Initial Assessment

| Action | Owner | SLA |
|--------|-------|-----|
| Perform preliminary evaluation of business request for viability and alignment | Business Analyst | 1 business day |

- [ ] Strategic alignment with organizational goals assessed
- [ ] Preliminary feasibility determined (technical, operational)
- [ ] Duplicate or overlapping initiatives checked
- [ ] Initial priority classification assigned (Critical / High / Medium / Low)

> **IF** request duplicates existing initiative **THEN** trigger ABORT: document overlap and redirect
> **ELSE** proceed to Step 3

### Step 3: Interview Key Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| Schedule and conduct structured interviews with key stakeholders | Business Analyst | 2 business days |

- [ ] Interview participants identified (minimum: requester + 1 domain expert)
- [ ] Interview questions prepared using stakeholder interview template
- [ ] Interviews conducted and recorded (notes or transcript)
- [ ] Pain points, goals, and expectations documented per stakeholder

> **IF** stakeholder identifies additional interviewees **THEN** schedule follow-up interviews within SLA
> **ELSE** proceed with current interview data

### Step 4: Analyze Market and Competitive Context

| Action | Owner | SLA |
|--------|-------|-----|
| Research market conditions, competitive landscape, and industry trends relevant to the business need | Business Analyst | 1 business day |

- [ ] Relevant market data gathered (industry reports, competitor analysis, trend data)
- [ ] Competitive positioning impact assessed
- [ ] Regulatory or compliance implications identified
- [ ] Findings documented with source citations

> **IF** business need is internal-only (no market-facing impact) **THEN** document internal operational context instead
> **ELSE** complete full market and competitive analysis

### Step 5: Quantify Business Impact

| Action | Owner | SLA |
|--------|-------|-----|
| Calculate operational impact of addressing (or not addressing) the business need | Business Analyst | 1 business day |



- [ ] Risk exposure assessed (operational, reputational, regulatory, security)
- [ ] Efficiency gains or losses estimated (FTE hours, cycle time, throughput)
- [ ] All estimates documented with assumptions and data sources

> **IF** quantitative data unavailable **THEN** use qualitative assessment with documented rationale and flag for sponsor review
> **ELSE** provide quantitative estimates with confidence ranges

### Step 6: Document Problem Statement

| Action | Owner | SLA |
|--------|-------|-----|
| Draft a clear, concise problem statement synthesizing all analysis findings | Business Analyst | 0.5 business days |

- [ ] Problem statement follows format: [Who] experiences [what problem] resulting in [what impact]
- [ ] Current state described
- [ ] Desired future state described
- [ ] Measurable gap between current and desired state defined
- [ ] Problem statement reviewed by Product Owner

> **IF** Product Owner requests revisions **THEN** revise and resubmit within 1 business day
> **ELSE** proceed to sponsor validation

### Step 7: Validate with Project Sponsor

| Action | Owner | SLA |
|--------|-------|-----|
| Present analysis findings and problem statement to Project Sponsor for validation | Business Analyst | 1 business day |

- [ ] Validation meeting scheduled with Project Sponsor
- [ ] Analysis summary and problem statement presented
- [ ] Sponsor confirms problem statement accuracy
- [ ] Sponsor confirms business need warrants further investigation
- [ ] Validation outcome documented (Approved / Revise / Reject)

> **IF** sponsor requests revisions **THEN** return to relevant step and re-execute within 2 business days
> **ELSE IF** sponsor rejects **THEN** document rejection rationale and close request
> **ELSE** proceed to exit criteria

---

## EXIT CRITERIA

- [ ] Problem statement validated and approved by Project Sponsor
- [ ] Business impact quantified with documented assumptions
- [ ] Stakeholder interviews completed and documented
- [ ] Market/competitive context analyzed and documented
- [ ] All findings consolidated into Business Needs Analysis artifact
- [ ] Analysis artifact stored in designated repository

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Business Needs Analysis | [Business Needs Analysis Template](../templates/business-needs-analysis-template.md) | `project-repo/phase-1/business-needs-analysis/` |
| Stakeholder Interview Notes | [Stakeholder Interview Template](../templates/stakeholder-interview-template.md) | `project-repo/phase-1/interview-notes/` |
| Problem Statement | [Problem Statement Template](../templates/problem-statement-template.md) | `project-repo/phase-1/problem-statement/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Case Development | Runbook | [RB-P1-002](./develop-business-case.md) |
| Project Charter Creation | Runbook | [RB-P1-003](./create-project-charter.md) |
| Initial Stakeholder Identification | Runbook | [RB-P1-004](./conduct-initial-stakeholder-identification.md) |
| Business Needs Analysis Template | Template | [../templates/business-needs-analysis-template.md](../templates/business-needs-analysis-template.md) |
| Phase 1 Standards | Standard | [../standards/phase-1-standards.md](../standards/phase-1-standards.md) |
