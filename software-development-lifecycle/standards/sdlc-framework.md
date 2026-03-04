# SDLC Framework Standard

GlowPowerRental software development lifecycle framework aligned with ISO/IEC/IEEE 12207.

---

## Lifecycle Phases

### Phase 1: Business Analysis

| Attribute | Detail |
|-----------|--------|
| Purpose | Identify and validate business needs, opportunities, and constraints |
| Entry Criteria | Business need or opportunity identified by stakeholder |
| Exit Criteria | Approved business case with defined scope |
| Required Artifacts | Business Case, Project Charter, Stakeholder Register |
| Phase Gate | Business case review and approval by project sponsor |

### Phase 2: Requirements Engineering

| Attribute | Detail |
|-----------|--------|
| Purpose | Elicit, analyze, specify, validate, and manage requirements |
| Entry Criteria | Approved business case and identified stakeholders |
| Exit Criteria | Baselined requirements with traceability and stakeholder sign-off |
| Required Artifacts | BRD, SRS, Requirements Traceability Matrix, Validation Report |
| Phase Gate | Requirements baseline review and approval |

### Phase 3: System Architecture

| Attribute | Detail |
|-----------|--------|
| Purpose | Define system structure, components, interfaces, and deployment topology |
| Entry Criteria | Baselined requirements |
| Exit Criteria | Approved architecture document with viewpoints per ISO 42010 |
| Required Artifacts | Architecture Description Document, System Context Diagram, Component Diagram, Deployment Diagram, ADRs |
| Phase Gate | Architecture review board approval |

### Phase 4: Design

| Attribute | Detail |
|-----------|--------|
| Purpose | Detail component-level design, data models, and API contracts |
| Entry Criteria | Approved architecture |
| Exit Criteria | Design documents reviewed and approved by tech lead |
| Required Artifacts | Detailed Design Document, Data Model, API Specifications, UI Wireframes |
| Phase Gate | Design review and tech lead sign-off |

### Phase 5: Development

| Attribute | Detail |
|-----------|--------|
| Purpose | Implement software components according to design |
| Entry Criteria | Approved design documents |
| Exit Criteria | Code complete, unit tests passing, code reviewed |
| Required Artifacts | Source Code, Unit Tests, Code Review Records |
| Phase Gate | Code review approval, unit test coverage threshold met |

### Phase 6: Testing

| Attribute | Detail |
|-----------|--------|
| Purpose | Verify implementation against requirements, validate fitness for purpose |
| Entry Criteria | Code complete, unit tests passing |
| Exit Criteria | All test cases executed, defects resolved or accepted |
| Required Artifacts | Test Plan, Test Cases, Test Results, Defect Reports |
| Phase Gate | Test completion report approval, release readiness review |

### Phase 7: Deployment

| Attribute | Detail |
|-----------|--------|
| Purpose | Release software to production environment |
| Entry Criteria | Testing complete, deployment plan approved |
| Exit Criteria | Software running in production, smoke tests passed |
| Required Artifacts | Deployment Plan, Release Notes, Rollback Plan |
| Phase Gate | Go/no-go decision, post-deployment verification |

### Phase 8: Operations

| Attribute | Detail |
|-----------|--------|
| Purpose | Monitor, maintain, and support software in production |
| Entry Criteria | Successful deployment |
| Exit Criteria | Ongoing (until decommission) |
| Required Artifacts | Operations Runbook, Monitoring Dashboard, Incident Reports |
| Phase Gate | Quarterly operations review |

---

## Roles and Responsibilities

| Role | Primary Responsibilities |
|------|-------------------------|
| Project Sponsor | Approves business case, funds project, resolves escalations |
| Product Owner | Defines business requirements, prioritizes backlog, accepts deliverables |
| Business Analyst | Elicits and documents requirements, facilitates stakeholder communication |
| Tech Lead | Owns architecture and design decisions, reviews code, mentors developers |
| Developer | Implements code, writes unit tests, participates in code reviews |
| QA Lead | Defines test strategy, manages test execution, reports quality metrics |
| Domain Expert | Provides subject matter expertise during elicitation and validation |

---

## Agile Execution Within This Framework

This SDLC framework defines **what** must be done. Agile practices define **how** work is executed within each phase.

| SDLC Concept | Agile Practice |
|--------------|----------------|
| Phase gate reviews | Sprint reviews and demos |
| Requirements specification | User stories with acceptance criteria |
| Design documentation | Architecture spikes and technical stories |
| Testing phase | Continuous testing within sprints |
| Change management | Backlog refinement and sprint planning |

Phases are not strictly sequential. In Agile execution:

- Requirements, design, and development may overlap within sprints.
- Phase gate artifacts are still required but may be produced incrementally.
- The requirements baseline is updated through formal change control regardless of sprint cadence.

---

## ISO 12207 Process Mapping

| ISO 12207 Process | GlowPowerRental Phase |
|-------------------|-----------------------|
| Stakeholder Needs and Requirements Definition | Business Analysis, Requirements Engineering |
| System/Software Requirements Definition | Requirements Engineering |
| Architecture Definition | System Architecture |
| Design Definition | Design |
| Implementation | Development |
| Integration | Development, Testing |
| Verification | Testing |
| Validation | Testing |
| Transition | Deployment |
| Operation | Operations |
| Maintenance | Operations |
