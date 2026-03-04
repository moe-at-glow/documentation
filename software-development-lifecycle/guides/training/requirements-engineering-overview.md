# Requirements Engineering Overview

How the requirements engineering process works at GlowPowerRental.

---

## What Is Requirements Engineering

Requirements engineering is the systematic process of discovering, documenting, and maintaining the requirements for a software system. It bridges the gap between business needs and software implementation.

Done well, it prevents:
- Building the wrong product.
- Discovering missing features late in development.
- Scope creep caused by undocumented assumptions.
- Costly rework from ambiguous specifications.

---

## Position in the SDLC

Requirements Engineering is Phase 2 of GlowPowerRental's 8-phase SDLC:

```
1. Business Analysis        <-- Input: business case, project charter
2. Requirements Engineering <-- YOU ARE HERE
3. System Architecture
4. Design
5. Development
6. Testing
7. Deployment
8. Operations
```

---

## The Requirements Engineering Lifecycle

```
Elicitation --> Analysis --> Specification --> Validation --> Management
    |              |             |                |              |
    v              v             v                v              v
 Gather raw     Organize,    Document in      Confirm        Handle
 needs from     decompose,   formal format    correctness,   changes
 stakeholders   prioritize   (BRD, SRS)       feasibility    after
                                              testability    baseline
```

| Activity | Purpose | Key Technique | Output |
|----------|---------|--------------|--------|
| Elicitation | Discover what stakeholders need | Interviews, workshops, observation | Raw requirements, interview notes |
| Analysis | Organize, decompose, and prioritize | Decomposition, MoSCoW prioritization, conflict resolution | Structured requirements hierarchy |
| Specification | Document requirements formally | Standardized templates, attribute completion | BRD, SRS |
| Validation | Confirm requirements are correct and complete | Reviews, walkthroughs, checklists | Validation report, baselined requirements |
| Management | Control changes after baseline | Change requests, impact analysis, CCB decisions | Updated baseline, change log |

---

## Alignment with ISO/IEC/IEEE 29148

This process implements:

| ISO 29148 Activity | GlowPowerRental Implementation |
|--------------------|-------------------------------|
| Stakeholder requirements definition (Clause 5) | Stakeholder analysis + BRD |
| System requirements analysis (Clause 6) | Requirements decomposition (STK -> SYS) |
| Software requirements specification (Clause 7) | SRS document |
| Requirements information items (Clause 8) | BRD, SRS, RTM |

---

## Requirements Hierarchy

```
+--------------------------------------------------+
|  Business Requirements (BR-XXX)                   |
|  What the business needs to achieve                |
|  Owner: Product Owner                              |
+--------------------------------------------------+
        |
        v
+--------------------------------------------------+
|  Stakeholder Requirements (STK-XXX)               |
|  What stakeholders need the system to do for them  |
|  Owner: Business Analyst                           |
+--------------------------------------------------+
        |
        v
+--------------------------------------------------+
|  System Requirements (SYS-XXX)                     |
|  What the system must do                           |
|  Owner: Business Analyst / Tech Lead               |
+--------------------------------------------------+
        |
        v
+--------------------------------------------------+
|  Software Requirements (SWR-XXX)                   |
|  Specific software behavior and constraints        |
|  Owner: Tech Lead / Developer                      |
+--------------------------------------------------+
```

Each level refines the one above it. Every requirement at a lower level must trace back to a requirement at the level above.

---

## Key Roles

| Role | Responsibilities in Requirements Engineering |
|------|---------------------------------------------|
| Product Owner | Defines business requirements, sets priorities, approves baseline |
| Business Analyst | Facilitates elicitation, writes BRD and SRS, maintains RTM |
| Tech Lead | Reviews feasibility, decomposes system/software requirements |
| Domain Expert | Provides subject matter knowledge during elicitation |
| QA Lead | Reviews testability, defines test approach per requirement |
| Project Sponsor | Approves business case, resolves escalations, signs off on baseline |

---

## Inputs

| Input | Source | Purpose |
|-------|--------|---------|
| Business Case | Business Analysis phase | Defines business objectives and justification |
| Project Charter | Project Sponsor | Defines scope, constraints, success criteria |
| Stakeholder Register | Stakeholder analysis | Identifies who to elicit requirements from |
| Existing System Documentation | Operations / IT | Defines current state and constraints |
| Regulatory Requirements | Legal / Compliance | Defines mandatory compliance requirements |

---

## Outputs

| Output | Description | Consumer |
|--------|-------------|----------|
| Business Requirements Document (BRD) | Formal record of business requirements | All project stakeholders |
| Software Requirements Specification (SRS) | Complete software requirements with acceptance criteria | Architecture, Development, Testing teams |
| Requirements Traceability Matrix (RTM) | Mapping from BR through SWR to test cases | All project phases |
| Validation Report | Evidence that requirements are complete, consistent, feasible, testable | Project Sponsor, CCB |
| Requirements Baseline | Approved, version-controlled set of requirements | Change management |

---

## Common Failure Modes

| Failure Mode | Consequence | Prevention |
|-------------|-------------|------------|
| Skipping stakeholder analysis | Missing requirements from key groups | Always complete stakeholder analysis before elicitation |
| Jumping to solution design during elicitation | Requirements describe implementation, not need | Enforce "what not how" rule in all sessions |
| Not validating with stakeholders | Building features nobody asked for | Mandatory stakeholder review before baseline |
| No change control after baseline | Uncontrolled scope growth | All changes go through CR process |
| Incomplete acceptance criteria | Untestable requirements, subjective quality | Every SWR must have Given/When/Then criteria |
| Single-stakeholder requirements | Biased system that ignores other users | Interview all stakeholder groups identified in analysis |

---

## Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Requirements coverage | 100% of BRs have SWRs | RTM analysis |
| Testability | 100% of SWRs have acceptance criteria | SRS review |
| Stakeholder participation | All Manage Closely stakeholders interviewed | Stakeholder register vs. interview log |
| Defect origin | Less than 10% of production defects trace to requirements | Defect root cause analysis |
| Change request volume | Decreasing trend after baseline | Change log analysis |
| Baseline approval time | Within 2 weeks of draft SRS completion | Project timeline |
