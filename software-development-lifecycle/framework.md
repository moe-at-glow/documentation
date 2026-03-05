# SDLC Framework

| Field | Value |
|-------|-------|
| **Owner** | Tech Lead |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead / Project Sponsor |
| **Verification Method** | Phase gate reviews, artifact audit |
| **Last Verified** | 2026-03-05 |

---

## 1. Purpose

This framework defines the software development lifecycle for engineering projects. It provides a four-phase model with clear gate criteria, role assignments, and scaling rules so that teams deliver working software with appropriate governance. The framework is operational -- follow it as written, scale it per the sizing table, and skip nothing without documented approval.

---

## 2. Framework Overview

| Phase | Name | Scope |
|-------|------|-------|
| 1 | **Define** | Identify business need, validate opportunity, elicit and baseline requirements, build stakeholder alignment |
| 2 | **Design** | Define system architecture, record ADRs, detail component design, specify data models and API contracts |
| 3 | **Build & Verify** | Implement code, write unit tests, execute integration/system/UAT testing, track and resolve defects |
| 4 | **Ship & Run** | Deploy to production, verify release, monitor operations, manage incidents, maintain runbooks |

Phase details: [phases/1-define.md](phases/1-define.md) | [phases/2-design.md](phases/2-design.md) | [phases/3-build-and-verify.md](phases/3-build-and-verify.md) | [phases/4-ship-and-run.md](phases/4-ship-and-run.md)

---

## 3. Roles and Responsibilities

Engineering teams operate with a core roster of 4 developers, 1 QA engineer, 1 business analyst, and 1 part-time product owner.

| Role | Primary Responsibilities |
|------|-------------------------|
| Product Owner (part-time) | Defines business requirements, prioritizes backlog, accepts deliverables, participates in UAT, makes go/no-go decisions |
| Business Analyst | Elicits and documents requirements, facilitates stakeholder communication, maintains the RTM |
| Tech Lead | Owns architecture and design decisions, reviews code, mentors developers, approves technical artifacts |
| Developer (x4) | Implements code, writes unit tests, participates in code reviews, contributes to design documentation |
| QA Engineer | Defines test strategy, manages test execution, reports quality metrics, manages defect tracking |
| Project Sponsor | Approves business case, resolves escalations, makes go/no-go decisions at major gates |

---

## 4. RACI Matrix

R = Responsible, A = Accountable, C = Consulted, I = Informed.

| Activity | Sponsor | PO | BA | Tech Lead | Dev | QA |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|
| **Phase 1 -- Define** | | | | | | |
| Define business case / problem statement | C | R | R | C | I | I |
| Approve business case | A | C | I | I | I | I |
| Identify stakeholders | I | R | R | C | I | I |
| Elicit and document requirements (BRD/SRS) | I | A | R | C | I | C |
| Build requirements traceability matrix | I | I | R | C | I | C |
| Validate and baseline requirements | A | R | R | C | I | I |
| **Phase 2 -- Design** | | | | | | |
| Define system architecture | I | C | C | A/R | C | C |
| Create architecture diagrams (.puml) | I | I | I | R | C | I |
| Write ADRs | I | I | I | A/R | C | I |
| Detail component design / data model / API spec | I | I | I | A | R | C |
| Design review | I | I | I | A | R | C |
| **Phase 3 -- Build & Verify** | | | | | | |
| Implement code | I | I | I | C | A/R | I |
| Write unit tests | I | I | I | C | A/R | I |
| Conduct code reviews | I | I | I | A | R | I |
| Write and execute test plan / test cases | I | C | I | C | C | A/R |
| Manage defects | I | C | I | C | R | A |
| Conduct UAT | I | A/R | C | I | C | R |
| Release readiness review | C | A | I | R | I | R |
| **Phase 4 -- Ship & Run** | | | | | | |
| Create deployment plan / rollback plan | I | I | I | A/R | C | I |
| Go/no-go decision | A | R | I | R | I | R |
| Execute deployment | I | I | I | R | C | I |
| Post-deployment verification | I | I | I | C | C | R |
| Monitor production / incident response | I | I | I | C | C | I |
| Maintain operations runbook | I | I | I | C | I | I |

---

## 5. Phase Gate Process

Every phase ends with a gate review. The pattern is the same for all four gates.

### Gate Review Procedure

1. **Preparation.** The phase lead assembles all required artifacts and distributes them to gate reviewers at least two business days before the review.
2. **Review meeting.** Reviewers evaluate artifacts against the exit criteria defined in the phase document. Each criterion is rated Met, Partially Met, or Not Met.
3. **Decision.** One of:
   - **Proceed** -- all exit criteria Met.
   - **Conditional proceed** -- minor items remain; punch list created with owners and due dates.
   - **Rework** -- one or more criteria Not Met; project stays in current phase until resolved.
   - **Stop** -- fundamental issues; sponsor makes go/no-go decision.
4. **Documentation.** Gate decision, attendees, and action items recorded in the project log.

### Gate Reviewers

| Gate | Required Reviewers |
|------|--------------------|
| Define exit | Project Sponsor, Product Owner, Business Analyst, Tech Lead |
| Design exit | Tech Lead, Product Owner, QA Engineer, Developer(s) assigned to build |
| Build & Verify exit | Product Owner, Tech Lead, QA Engineer |
| Ship & Run reviews | Tech Lead, QA Engineer, Product Owner (quarterly) |

### Entry / Exit Criteria Summary

| Gate | Entry Criteria | Exit Criteria |
|------|---------------|---------------|
| Define | Business need identified by stakeholder | Approved business case, baselined requirements with stakeholder sign-off, RTM created |
| Design | Baselined requirements | Approved architecture document with ADRs, detailed design reviewed by tech lead, API specs and data model complete |
| Build & Verify | Approved design documents | Code complete, unit tests passing (>=80% business logic coverage), all tests executed, critical/high defects resolved, release readiness approved |
| Ship & Run | Testing complete, deployment plan approved | Software running in production, smoke tests passed, monitoring active, runbook updated |

---

## 6. Project Sizing

| Size | Duration | Team |
|------|----------|------|
| **Small** | < 2 weeks | 1-2 developers |
| **Medium** | 2-8 weeks | 3-5 developers |
| **Large** | 8+ weeks | Full team or multiple teams |

---

## 7. Scaling Guide

### Small Projects (< 2 weeks)

| Phase | What You Can Skip or Simplify |
|-------|-------------------------------|
| Define | Brief written problem statement (Jira epic description is fine). User stories with acceptance criteria replace formal BRD. Verbal sponsor approval acceptable. |
| Design | ADR required only if modifying existing architecture. Design documented in ticket or inline code comments for single-component changes. |
| Build & Verify | Code review by at least one peer required. Unit tests required. Manual testing with documented results acceptable; formal test plan not required. |
| Ship & Run | Standard deployment pipeline sufficient. Release notes required. Update existing runbook if applicable. |

### Medium Projects (2-8 weeks)

| Phase | Minimum Requirements |
|-------|---------------------|
| Define | Business case and stakeholder register required. BRD, SRS, and RTM required. Validation may be a single review session. |
| Design | Architecture Description Document required. System Context and Component diagrams required. ADRs for all significant decisions. Detailed design, data model, and API specs required for new components. |
| Build & Verify | Code review and unit tests with >=80% business logic coverage required. Test plan, linked test cases, and defect tracking required. |
| Ship & Run | Deployment plan, rollback plan, and release notes required. Runbook and monitoring dashboard updates required. |

### Large Projects (8+ weeks)

Full compliance with all artifacts, phase gates, and review procedures. No reductions without written approval from the project sponsor and tech lead.

### Minimum Compliance (All Sizes)

These five rules apply regardless of project size:

1. **Traceability** -- traceable link from business need to implementation (Jira epic chain for small; formal RTM for medium/large).
2. **Code review** -- all production code peer reviewed before merging.
3. **Testing** -- all production code has automated unit tests; integration/system testing for multi-component changes.
4. **Change control** -- changes to baselined requirements documented and approved by product owner.
5. **Deployment safety** -- every production deployment has a rollback plan.

### Compliance Exceptions

Any exception requires: documented rationale, written approval from tech lead and project sponsor, and a record in the project ADR log.

---

## 8. Artifact Overview

For the full artifact checklist with descriptions, owners, and phase mappings, see [references/artifacts-checklist.md](references/artifacts-checklist.md).

Summary by phase:

| Phase | Key Artifacts |
|-------|--------------|
| Define | Business Case, Project Charter, Stakeholder Register, BRD, SRS, RTM, Validation Report |
| Design | Architecture Description, ADRs, System Context / Component / Deployment / Sequence / ERD / State diagrams (.puml), Detailed Design Document, Data Model, API Specifications, UI Wireframes |
| Build & Verify | Source Code, Unit Tests, Code Review Records, Test Plan, Test Cases, Test Results, Defect Reports |
| Ship & Run | Deployment Plan, Rollback Plan, Release Notes, Operations Runbook, Monitoring Dashboard Config, Incident Reports |

---

## 9. Diagramming Rules

**PlantUML** is the mandatory diagramming tool. All diagrams are committed as `.puml` source files in the `diagrams/` directory. See [diagrams/](diagrams/) for templates and examples.

| # | Rule |
|---|------|
| 1 | All diagrams stored as `.puml` source files in `diagrams/` |
| 2 | Filenames use kebab-case (e.g., `system-context.puml`) |
| 3 | Every `.puml` file includes `@startuml` / `@enduml` |
| 4 | Diagrams committed to version control alongside documentation |
| 5 | Diagrams updated when architecture or design changes |

### Required Diagrams by Phase and Size

| Diagram | Define | Design | Small | Medium | Large |
|---------|:------:|:------:|:-----:|:------:|:-----:|
| System Context | -- | Required | Required | Required | Required |
| Component | -- | Required | Optional | Required | Required |
| Deployment | -- | Required | Optional | Required | Required |
| Sequence (top 3 workflows) | -- | Required | Optional | Required | Required |
| ERD | -- | Required | Required | Required | Required |
| State (key entities) | -- | Required | Optional | Required | Required |
| Class | -- | Required | Optional | Required | Required |
| API Flow | -- | Required | Optional | Required | Required |
| Data Flow | -- | Required | Optional | Required | Required |
| [Project Journey](diagrams/project-journey.puml) | Overview | Overview | Overview | Overview | Overview |
| [Artifact Flow](diagrams/artifact-flow.puml) | Overview | Overview | Overview | Overview | Overview |

---

## 10. Document Metadata Standard

Every document in this repository must include a metadata table at the top of the file.

| Field | Description | Example |
|-------|-------------|---------|
| **Owner** | The role responsible for keeping the document current | Tech Lead |
| **Last Verified** | Date the document was last reviewed for accuracy (YYYY-MM-DD) | 2026-03-05 |
| **Compliance Level** | Mandatory, Recommended, or Reference | Mandatory |
| **Enforced By** | Role(s) who enforce compliance | Tech Lead / Project Sponsor |
| **Verification Method** | How compliance is checked | Phase gate reviews, artifact audit |

Documents must be re-verified at least quarterly or whenever the content they describe changes, whichever comes first.

---

## Cross-References

| Document | Type | Path |
|----------|------|------|
| Define Phase | Phase Guide | [phases/1-define.md](phases/1-define.md) |
| Design Phase | Phase Guide | [phases/2-design.md](phases/2-design.md) |
| Build & Verify Phase | Phase Guide | [phases/3-build-and-verify.md](phases/3-build-and-verify.md) |
| Ship & Run Phase | Phase Guide | [phases/4-ship-and-run.md](phases/4-ship-and-run.md) |
| Requirements Engineering Standard | Standard | [standards/requirements.md](standards/requirements.md) |
| Requirements Classification Standard | Standard | [standards/requirements.md](standards/requirements.md) |
| Requirements Traceability Standard | Standard | [standards/requirements.md](standards/requirements.md) |
| Conduct Stakeholder Analysis | Runbook | [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| Extract Business Requirements | Runbook | [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| Derive Software Requirements | Runbook | [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| Validate Requirements | Runbook | [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| Manage Requirements Changes | Runbook | [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| Artifacts Checklist | Reference | [references/artifacts-checklist.md](references/artifacts-checklist.md) |
| Diagram Templates | Diagrams | [diagrams/](diagrams/) |
