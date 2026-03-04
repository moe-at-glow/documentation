# Business Analysis Overview -- Training Material

| Field | Value |
|-------|-------|
| **Type** | Training / Educational |
| **Phase** | Phase 1 -- Business Analysis |
| **Last Updated** | 2026-03-04 |

---

## What Is Business Analysis?

Business analysis is the discipline of identifying business needs, defining problems, and evaluating solutions to drive organizational change. In the context of software development, business analysis ensures that technology investments are grounded in real business problems, supported by evidence, and aligned with strategic goals.

Business analysis is not about jumping to a solution. It is about understanding the "why" before the "what" -- ensuring that the organization invests in the right problem before committing resources to build anything.

---

## Why Phase 1 Matters

Phase 1 is the foundation of the entire Software Development Lifecycle. Every subsequent phase -- requirements, design, development, testing, deployment, and operations -- depends on the clarity and quality of Phase 1 outputs.

When Phase 1 is done well:
- The project solves a real, validated business problem.
- Stakeholders are aligned on objectives and success criteria.
- Financial and resource commitments are based on sound analysis.
- Risks are identified early when they are cheapest to address.
- The project charter provides a clear mandate for Phase 2 and beyond.

When Phase 1 is skipped or rushed:
- Teams build solutions to the wrong problem.
- Scope expands uncontrollably because the boundary was never defined.
- Costs overrun because estimates lacked rigor.
- Projects lose sponsorship because value was never clearly articulated.
- Downstream phases inherit ambiguity that compounds into rework and delay.

---

## How Phase 1 Fits in the SDLC

Phase 1 is the entry point of the SDLC. It begins when a business need is identified and concludes when a project charter is approved by governance.

**Position in the lifecycle:**

```
Phase 1: Business Analysis
    |
    v
Phase 2: Requirements & Planning
    |
    v
Phase 3: Design & Architecture
    |
    v
Phase 4: Development & Build
    |
    v
Phase 5: Testing & Quality Assurance
    |
    v
Phase 6: Deployment & Release
    |
    v
Phase 7: Operations & Maintenance
```

Phase 1 feeds directly into Phase 2 (Requirements & Planning). The approved project charter, business case, and problem statement become the primary inputs for requirements elicitation and project planning.

---

## Key Activities in Phase 1

### 1. Business Need Identification
The process starts with recognizing that a business need exists. Needs can originate from strategic planning, operational incidents, regulatory changes, customer feedback, market shifts, or technology obsolescence. The goal is to capture the need in a clear, outcome-oriented statement.

### 2. Stakeholder Identification and Engagement
Identifying who is affected by, interested in, or able to influence the outcome is critical. Stakeholder mapping ensures that the right voices are heard during analysis and that no key perspective is overlooked. Early engagement builds buy-in and reduces the risk of late-stage objections.

### 3. Problem Definition
The business need is refined into a precise problem statement. A good problem statement quantifies the impact, identifies who is affected, and avoids prescribing a solution. This step often involves current-state analysis, data gathering, and stakeholder interviews.

### 4. Business Case Development
The business case evaluates multiple options for addressing the problem, including the "do nothing" option. Each option is assessed for strategic alignment, financial viability, technical feasibility, risk profile, and resource availability. The business case recommends an option and provides the evidence to support that recommendation.

### 5. Risk Assessment
Each option in the business case is evaluated for risks -- technical, financial, organizational, regulatory, and operational. Risks are rated for likelihood and impact, and mitigation strategies are proposed. This assessment informs the governance decision.

### 6. Project Charter Creation
The project charter formalizes the decision to proceed. It defines the project's objectives, scope boundary, high-level timeline, budget envelope, key stakeholders, authority structure, and success criteria. The charter is the authorization to move into Phase 2.

---

## Artifacts Produced in Phase 1

| Artifact | Purpose |
|----------|---------|
| Business Need Statement | Documents the originating need and its strategic context |
| Stakeholder Register | Lists all identified stakeholders, their interests, and influence levels |
| Problem Statement | Defines the specific problem to be solved, with quantified impact |
| Business Case | Evaluates options, presents cost-benefit analysis, and recommends an approach |
| Risk Assessment | Documents risks per option with likelihood, impact, and mitigation plans |
| Project Charter | Authorizes the project with defined scope, budget, timeline, and governance |

---

## Roles Involved in Phase 1

| Role | Responsibility |
|------|---------------|
| Business Owner / Sponsor | Owns the business need; provides funding authority; approves the charter |
| Business Analyst | Facilitates analysis activities; develops the problem statement and business case |
| Stakeholders | Provide input on needs, constraints, and priorities |
| Finance Representative | Reviews and validates financial projections and cost estimates |
| Technical Lead / Architect | Assesses technical feasibility of proposed options |
| Risk / Compliance Officer | Reviews risk assessment and regulatory implications |
| Governance Board | Approves or rejects the project charter; authorizes transition to Phase 2 |

---

## How Phase 1 Feeds Phase 2

The outputs of Phase 1 become the inputs to Phase 2 (Requirements & Planning):

| Phase 1 Output | Phase 2 Input |
|----------------|---------------|
| Approved Problem Statement | Basis for requirements elicitation scope |
| Approved Business Case (selected option) | Constraints, assumptions, and context for requirements |
| Stakeholder Register | Starting point for requirements workshops and interviews |
| Project Charter (scope, budget, timeline) | Boundaries for project planning and resource allocation |
| Risk Assessment | Input to risk management plan and contingency planning |
| Success Criteria | Basis for acceptance criteria and test strategy |

---

## Alignment with ISO/IEC/IEEE 12207

Phase 1 aligns with the **Stakeholder Needs and Requirements Definition Process** described in ISO/IEC/IEEE 12207:2017 (Systems and software engineering -- Software life cycle processes). Specifically:

- **6.4.1 -- Stakeholder Needs and Requirements Definition Process**: This process identifies stakeholders, elicits their needs, and transforms those needs into a set of stakeholder requirements that can serve as the basis for the system requirements. Phase 1 activities -- stakeholder identification, problem definition, and business case development -- map directly to this process.

- **Purpose**: To define the stakeholder requirements for a system that can provide the capabilities needed by users and other stakeholders in a defined environment.

- **Outcomes**: Stakeholder needs are identified; constraints on a system solution are identified; stakeholder requirements are defined; traceability from stakeholder requirements back to stakeholders is established.

Organizations adopting ISO 12207 can use Phase 1 activities and artifacts to satisfy the stakeholder needs and requirements definition process requirements.

---

## Summary

Phase 1 is where discipline begins. By investing time in understanding the business need, defining the problem precisely, evaluating options rigorously, and formalizing authorization through a project charter, organizations set themselves up for successful delivery in later phases. Skipping or rushing Phase 1 is the single most common root cause of project failure.

---

## Related Quick References

| Document | Reference ID | Link |
|----------|-------------|------|
| Common Business Analysis Pitfalls | QR-P1-001 | [../common-business-analysis-pitfalls.md](../common-business-analysis-pitfalls.md) |
| From Business Need to Project Charter | QR-P1-002 | [../from-business-need-to-project-charter.md](../from-business-need-to-project-charter.md) |
| Business Case Evaluation Criteria | QR-P1-003 | [../business-case-evaluation-criteria.md](../business-case-evaluation-criteria.md) |
