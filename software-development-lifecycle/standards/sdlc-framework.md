# SDLC Framework Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P2-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead / Project Sponsor |
| **Verification Method** | Phase gate reviews, artifact audit |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Reduced artifacts per scaling table below; user stories may replace formal BRD
> **IF** medium project (3-5 devs) **THEN** All artifacts required; streamlined formats permitted
> **IF** large project (6+ devs) **THEN** Full compliance required; no reductions without written sponsor + tech lead approval

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

**Entry/Exit Checklist:**

- [ ] Business need or opportunity identified by stakeholder
- [ ] Business case approved with defined scope
- [ ] Project charter created and signed
- [ ] Stakeholder register completed
- [ ] Phase gate review conducted and decision recorded

### Phase 2: Requirements Engineering

| Attribute | Detail |
|-----------|--------|
| Purpose | Elicit, analyze, specify, validate, and manage requirements |
| Entry Criteria | Approved business case and identified stakeholders |
| Exit Criteria | Baselined requirements with traceability and stakeholder sign-off |
| Required Artifacts | BRD, SRS, Requirements Traceability Matrix, Validation Report |
| Phase Gate | Requirements baseline review and approval |

**Entry/Exit Checklist:**

- [ ] Approved business case and identified stakeholders available
- [ ] BRD completed and reviewed
- [ ] SRS completed and reviewed
- [ ] RTM created with forward traceability from BR to SWR
- [ ] Requirements validated through walkthroughs/inspections
- [ ] Validation report produced
- [ ] Stakeholder sign-off obtained
- [ ] Requirements baselined; change control activated

### Phase 3: System Architecture

| Attribute | Detail |
|-----------|--------|
| Purpose | Define system structure, components, interfaces, and deployment topology |
| Entry Criteria | Baselined requirements |
| Exit Criteria | Approved architecture document with viewpoints per ISO 42010 |
| Required Artifacts | Architecture Description Document, System Context Diagram, Component Diagram, Deployment Diagram, ADRs |
| Phase Gate | Architecture review board approval |

**Entry/Exit Checklist:**

- [ ] Baselined requirements available as input
- [ ] Architecture Description Document produced with ISO 42010 viewpoints
- [ ] System Context Diagram completed
- [ ] Component Diagram completed
- [ ] Deployment Diagram completed
- [ ] ADRs recorded for all significant decisions
- [ ] Architecture review board approval obtained

### Phase 4: Design

| Attribute | Detail |
|-----------|--------|
| Purpose | Detail component-level design, data models, and API contracts |
| Entry Criteria | Approved architecture |
| Exit Criteria | Design documents reviewed and approved by tech lead |
| Required Artifacts | Detailed Design Document, Data Model, API Specifications, UI Wireframes |
| Phase Gate | Design review and tech lead sign-off |

**Entry/Exit Checklist:**

- [ ] Approved architecture available as input
- [ ] Detailed Design Document produced per component
- [ ] Data model specified (entities, attributes, relationships, constraints)
- [ ] API specifications completed (OpenAPI or equivalent)
- [ ] UI wireframes produced for user-facing components
- [ ] RTM updated with design-level mappings
- [ ] Tech lead sign-off obtained

### Phase 5: Development

| Attribute | Detail |
|-----------|--------|
| Purpose | Implement software components according to design |
| Entry Criteria | Approved design documents |
| Exit Criteria | Code complete, unit tests passing, code reviewed |
| Required Artifacts | Source Code, Unit Tests, Code Review Records |
| Phase Gate | Code review approval, unit test coverage threshold met |

**Entry/Exit Checklist:**

- [ ] Approved design documents available as input
- [ ] All planned components code complete
- [ ] Unit tests written and passing
- [ ] Unit test coverage meets minimum 80% for business logic
- [ ] All code peer reviewed and approved
- [ ] Code review records retained

### Phase 6: Testing

| Attribute | Detail |
|-----------|--------|
| Purpose | Verify implementation against requirements, validate fitness for purpose |
| Entry Criteria | Code complete, unit tests passing |
| Exit Criteria | All test cases executed, defects resolved or accepted |
| Required Artifacts | Test Plan, Test Cases, Test Results, Defect Reports |
| Phase Gate | Test completion report approval, release readiness review |

**Entry/Exit Checklist:**

- [ ] Code complete and unit tests passing
- [ ] Test plan defined (strategy, scope, environments, resources)
- [ ] Test cases derived from SRS and linked via RTM
- [ ] Integration, system, regression, and UAT tests executed
- [ ] All critical/high-severity defects resolved
- [ ] Medium/low defects deferred only with product owner acceptance
- [ ] Test completion report produced with release readiness recommendation

### Phase 7: Deployment

| Attribute | Detail |
|-----------|--------|
| Purpose | Release software to production environment |
| Entry Criteria | Testing complete, deployment plan approved |
| Exit Criteria | Software running in production, smoke tests passed |
| Required Artifacts | Deployment Plan, Release Notes, Rollback Plan |
| Phase Gate | Go/no-go decision, post-deployment verification |

**Entry/Exit Checklist:**

- [ ] Testing complete and deployment plan approved
- [ ] Deployment plan specifies steps, owners, config, data migration, timing
- [ ] Rollback plan documented
- [ ] Release notes produced (features, fixes, known issues, user actions)
- [ ] Go/no-go decision made by Product Owner, Tech Lead, QA Lead, Ops Lead
- [ ] Post-deployment smoke tests and monitoring checks passed

### Phase 8: Operations

| Attribute | Detail |
|-----------|--------|
| Purpose | Monitor, maintain, and support software in production |
| Entry Criteria | Successful deployment |
| Exit Criteria | Ongoing (until decommission) |
| Required Artifacts | Operations Runbook, Monitoring Dashboard, Incident Reports |
| Phase Gate | Quarterly operations review |

**Entry/Exit Checklist:**

- [ ] Successful deployment confirmed
- [ ] Operations runbook documented (startup/shutdown, backup/restore, scaling, incident response)
- [ ] Monitoring dashboard configured (availability, response time, error rates, resource utilization)
- [ ] Incident management process active
- [ ] Quarterly operations review scheduled

---

## Artifacts Summary

| Phase | Artifact | Description | Owner |
|-------|----------|-------------|-------|
| 1 - Business Analysis | Business Case | Justification for the project including cost-benefit analysis, risk assessment, and strategic alignment | Business Analyst |
| 1 - Business Analysis | Project Charter | Formal authorization of the project with high-level scope, objectives, and constraints | Project Sponsor |
| 1 - Business Analysis | Stakeholder Register | Identification of all stakeholders with their interests, influence, and communication needs | Business Analyst |
| 2 - Requirements Engineering | Business Requirements Document (BRD) | Business-level requirements describing what the organization needs | Business Analyst |
| 2 - Requirements Engineering | Software Requirements Specification (SRS) | Detailed functional and non-functional requirements for the software system | Business Analyst |
| 2 - Requirements Engineering | Requirements Traceability Matrix (RTM) | Bidirectional mapping from business needs through requirements, design, code, and tests | Business Analyst |
| 2 - Requirements Engineering | Validation Report | Results of requirements validation activities (walkthroughs, inspections, reviews) | Business Analyst |
| 3 - System Architecture | Architecture Description Document | System structure, viewpoints, and technology selections per ISO 42010 | Tech Lead |
| 3 - System Architecture | System Context Diagram | Boundary of the system and its interactions with external actors | Tech Lead |
| 3 - System Architecture | Component Diagram | Internal modules/services and their interfaces | Tech Lead |
| 3 - System Architecture | Deployment Diagram | Infrastructure, hosting, and network topology | Tech Lead |
| 3 - System Architecture | Architecture Decision Records (ADRs) | Recorded decisions with context, options, trade-offs, and rationale | Tech Lead |
| 4 - Design | Detailed Design Document | Component-level specifications including internal structure and behavior | Developer / Tech Lead |
| 4 - Design | Data Model | Entities, attributes, relationships, and constraints | Developer / Tech Lead |
| 4 - Design | API Specifications | Endpoint definitions, request/response formats, error codes, authentication | Developer / Tech Lead |
| 4 - Design | UI Wireframes | Layout, navigation, and interaction flows for user-facing components | Developer / Tech Lead |
| 5 - Development | Source Code | Implemented software components in version control | Developer |
| 5 - Development | Unit Tests | Automated tests verifying component-level correctness | Developer |
| 5 - Development | Code Review Records | Documentation of peer review feedback and approval | Developer |
| 6 - Testing | Test Plan | Testing strategy, scope, environments, and resource assignments | QA Lead |
| 6 - Testing | Test Cases | Step-by-step test procedures linked to requirements | QA Lead |
| 6 - Testing | Test Results | Execution outcomes for all test cases | QA Lead |
| 6 - Testing | Defect Reports | Logged defects with severity, priority, and resolution status | QA Lead |
| 7 - Deployment | Deployment Plan | Step-by-step deployment procedure with environment configuration | Tech Lead |
| 7 - Deployment | Release Notes | Summary of changes, known issues, and user actions required | Tech Lead |
| 7 - Deployment | Rollback Plan | Procedure for reverting to the previous state if deployment fails | Tech Lead |
| 8 - Operations | Operations Runbook | Standard operating procedures for the production system | Operations Lead |
| 8 - Operations | Monitoring Dashboard | Real-time system health metrics and alerting configuration | Operations Lead |
| 8 - Operations | Incident Reports | Documentation of incidents including root cause and resolution | Operations Lead |

---

## Phase Dependencies

| Source Phase | Artifact | Consumed By |
|-------------|----------|-------------|
| 1 - Business Analysis | Business Case | Phase 2 (scope and context for requirements) |
| 1 - Business Analysis | Stakeholder Register | Phase 2 (elicitation planning), Phase 6 (UAT participants) |
| 2 - Requirements Engineering | BRD | Phase 3 (architecture drivers), Phase 6 (UAT criteria) |
| 2 - Requirements Engineering | SRS | Phase 3 (architecture inputs), Phase 4 (design inputs), Phase 5 (implementation guidance), Phase 6 (test case derivation) |
| 2 - Requirements Engineering | RTM | Phase 4 (design traceability), Phase 5 (code traceability), Phase 6 (test traceability) |
| 3 - System Architecture | Architecture Description | Phase 4 (design constraints), Phase 5 (technology stack), Phase 7 (deployment topology) |
| 3 - System Architecture | ADRs | Phase 4 (design rationale), Phase 5 (implementation decisions) |
| 4 - Design | Detailed Design Document | Phase 5 (implementation specifications) |
| 4 - Design | Data Model | Phase 5 (database implementation), Phase 7 (data migration) |
| 4 - Design | API Specifications | Phase 5 (API implementation), Phase 6 (API testing) |
| 5 - Development | Source Code | Phase 6 (system under test), Phase 7 (deployment package) |
| 5 - Development | Unit Tests | Phase 6 (test baseline) |
| 6 - Testing | Test Results | Phase 7 (go/no-go input) |
| 6 - Testing | Defect Reports | Phase 5 (fixes), Phase 7 (known issues for release notes) |
| 7 - Deployment | Release Notes | Phase 8 (operations context) |
| 7 - Deployment | Rollback Plan | Phase 8 (incident response) |

---

## Scaling the Framework

### Small Projects (1-2 Developers)

| Phase | Minimum Requirements |
|-------|---------------------|
| 1 - Business Analysis | A brief written problem statement (may be a Jira epic description) and verbal sponsor approval. Formal business case not required. |
| 2 - Requirements Engineering | Requirements may be captured as user stories with acceptance criteria directly in the backlog. A formal BRD is not required. An SRS section or equivalent covering key functional and non-functional requirements is required. |
| 3 - System Architecture | If the project modifies existing architecture, an ADR documenting the change is required. If the project operates within existing architecture, no architecture artifacts are needed. |
| 4 - Design | Design may be documented in the ticket or as inline code comments. A formal Detailed Design Document is not required for changes scoped to a single component. |
| 5 - Development | Code review by at least one peer is required. Unit tests are required. |
| 6 - Testing | Manual testing with documented results is acceptable. A formal test plan is not required. |
| 7 - Deployment | Standard deployment pipeline is sufficient. Release notes are required. |
| 8 - Operations | Updates to existing operations runbook if applicable. |

### Medium Projects (3-5 Developers)

| Phase | Minimum Requirements |
|-------|---------------------|
| 1 - Business Analysis | Business case document required. Stakeholder register required. Project charter may be informal. |
| 2 - Requirements Engineering | BRD and SRS required. RTM required. Validation may be conducted as a single review session rather than multiple rounds. |
| 3 - System Architecture | Architecture Description Document required. At least System Context and Component diagrams required. ADRs required for all significant decisions. |
| 4 - Design | Detailed Design Document required for new components. Data model and API specifications required. UI wireframes required for new user-facing features. |
| 5 - Development | Code review required. Unit tests required with minimum 80% coverage for business logic. |
| 6 - Testing | Test plan required. Test cases required and linked to requirements. Defect tracking required. |
| 7 - Deployment | Deployment plan and rollback plan required. Release notes required. |
| 8 - Operations | Operations runbook update required. Monitoring dashboard update required. |

### Large Projects (6+ Developers)

| Phase | Minimum Requirements |
|-------|---------------------|
| All Phases | Full compliance with all artifacts, phase gates, and review procedures as defined in this standard. No reductions or substitutions permitted without written approval from the project sponsor and tech lead. |

---

## Minimum Compliance Requirements

- [ ] 1. **Traceability** -- Traceable link from business need to implementation (Jira epic chain for small; formal RTM for medium/large)
- [ ] 2. **Code review** -- All production code peer reviewed before merging
- [ ] 3. **Testing** -- All production code has automated unit tests; integration/system testing required for multi-component changes
- [ ] 4. **Change control** -- Changes to established requirements documented and approved by product owner
- [ ] 5. **Deployment safety** -- Every production deployment has a rollback plan

### Compliance Exceptions

- [ ] Exception documented with rationale
- [ ] Written approval from tech lead and project sponsor obtained
- [ ] Exception recorded in project ADR log

---

## Project Kickoff Checklist

| Item | Description | Responsible |
|------|-------------|-------------|
| Sponsor identified | A named project sponsor who has budget authority and will approve the business case | Department head |
| Product owner assigned | A named product owner who will define priorities and accept deliverables | Project sponsor |
| Business analyst assigned | A named business analyst who will lead requirements elicitation | Resource manager |
| Initial problem statement | A written description of the business need or opportunity (may be informal) | Project sponsor |
| Project scale determined | An initial assessment of project scale (small, medium, large) to determine compliance level | Tech lead |
| Repository created | A version control repository for the project, following GlowPowerRental naming conventions | Tech lead |
| Communication channel established | A dedicated team channel (e.g., Slack, Teams) for project communication | Business analyst |
| Access to this framework | All team members have read access to this SDLC documentation repository | Tech lead |
| Kickoff meeting scheduled | A meeting to walk the team through the framework, roles, and timeline | Business analyst |

---

## Gate Review Procedure

1. **Preparation.** The phase lead assembles all required artifacts and distributes them to gate reviewers at least two business days before the review meeting.

2. **Review meeting.** Gate reviewers evaluate the artifacts against the exit criteria defined in the phase table above. The meeting follows this agenda:
   - Phase lead presents a summary of work completed and artifacts produced.
   - Reviewers raise questions, concerns, and deficiencies.
   - Each exit criterion is evaluated as Met, Partially Met, or Not Met.

3. **Decision.** The gate decision is one of:
   - **Proceed** -- All exit criteria are Met. The project advances to the next phase.
   - **Conditional proceed** -- Minor items remain open but do not block the next phase. A punch list is created with owners and due dates.
   - **Rework** -- One or more exit criteria are Not Met. The project remains in the current phase until the issues are resolved and a follow-up review is conducted.
   - **Stop** -- Fundamental issues have been identified that call the project viability into question. The project sponsor must make a go/no-go decision.

4. **Documentation.** The gate review decision, attendees, and any action items are recorded in the project log. For medium and large projects, a formal gate review record is filed.

### Gate Reviewers by Phase

| Phase Gate | Required Reviewers |
|------------|--------------------|
| Phase 1 exit | Project Sponsor, Product Owner |
| Phase 2 exit | Product Owner, Business Analyst, Tech Lead, Domain Expert(s) |
| Phase 3 exit | Tech Lead, Product Owner, QA Lead (architecture review board for large projects) |
| Phase 4 exit | Tech Lead, Developer(s) assigned to implementation |
| Phase 5 exit | Tech Lead, QA Lead |
| Phase 6 exit | Product Owner, Tech Lead, QA Lead |
| Phase 7 exit | Product Owner, Tech Lead, QA Lead, Operations Lead |
| Phase 8 reviews | Tech Lead, Operations Lead, Product Owner (quarterly) |

---

## Roles and Responsibilities

| Role | Primary Responsibilities |
|------|-------------------------|
| Project Sponsor | Approves business case, funds project, resolves escalations, makes go/no-go decisions at major gates |
| Product Owner | Defines business requirements, prioritizes backlog, accepts deliverables, participates in UAT |
| Business Analyst | Elicits and documents requirements, facilitates stakeholder communication, maintains the RTM |
| Tech Lead | Owns architecture and design decisions, reviews code, mentors developers, approves technical artifacts |
| Developer | Implements code, writes unit tests, participates in code reviews, contributes to design documentation |
| QA Lead | Defines test strategy, manages test execution, reports quality metrics, manages defect tracking |
| Domain Expert | Provides subject matter expertise during elicitation, validation, and UAT |
| Operations Lead | Manages production environment, responds to incidents, maintains operations documentation |

### RACI Matrix

| Activity | Project Sponsor | Product Owner | Business Analyst | Tech Lead | Developer | QA Lead | Domain Expert | Operations Lead |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **Phase 1: Business Analysis** | | | | | | | | |
| Define business case | C | R | R | C | I | I | C | I |
| Approve business case | A | C | I | I | I | I | I | I |
| Identify stakeholders | I | R | R | C | I | I | C | C |
| Create project charter | A | C | R | C | I | I | I | I |
| **Phase 2: Requirements Engineering** | | | | | | | | |
| Elicit requirements | I | C | R | C | I | I | R | C |
| Analyze and classify requirements | I | C | R | C | I | C | C | I |
| Write BRD | I | A | R | C | I | I | C | I |
| Write SRS | I | C | R | R | C | C | C | I |
| Build RTM | I | I | R | C | I | C | I | I |
| Validate requirements | I | A | R | C | I | C | R | I |
| Baseline requirements | A | R | R | C | I | I | C | I |
| **Phase 3: System Architecture** | | | | | | | | |
| Define system architecture | I | C | C | A/R | C | C | I | C |
| Create architecture diagrams | I | I | I | R | C | I | I | C |
| Write ADRs | I | I | I | A/R | C | I | I | C |
| Architecture review | I | C | I | A | C | C | I | C |
| **Phase 4: Design** | | | | | | | | |
| Detailed component design | I | I | I | A | R | I | I | I |
| Data model design | I | I | I | A | R | I | I | I |
| API specification | I | I | I | A | R | C | I | I |
| UI wireframes | I | C | C | A | R | I | C | I |
| Design review | I | I | I | A | R | C | I | I |
| **Phase 5: Development** | | | | | | | | |
| Implement code | I | I | I | C | A/R | I | I | I |
| Write unit tests | I | I | I | C | A/R | I | I | I |
| Conduct code reviews | I | I | I | A | R | I | I | I |
| **Phase 6: Testing** | | | | | | | | |
| Write test plan | I | C | I | C | I | A/R | I | I |
| Write test cases | I | I | C | I | I | A/R | I | I |
| Execute tests | I | I | I | I | C | A/R | I | I |
| Manage defects | I | C | I | C | R | A | I | I |
| Conduct UAT | I | A/R | C | I | C | R | R | I |
| Release readiness review | C | A | I | R | I | R | I | C |
| **Phase 7: Deployment** | | | | | | | | |
| Create deployment plan | I | I | I | A/R | C | I | I | C |
| Execute deployment | I | I | I | R | C | I | I | C |
| Go/no-go decision | A | R | I | R | I | R | I | C |
| Post-deployment verification | I | I | I | C | C | R | I | R |
| **Phase 8: Operations** | | | | | | | | |
| Monitor production | I | I | I | C | I | I | I | A/R |
| Incident response | I | I | I | C | C | I | I | A/R |
| Maintain operations runbook | I | I | I | C | I | I | I | A/R |
| Quarterly operations review | I | C | I | R | I | I | I | A/R |

---

## Agile Execution Mapping

| Sprint Activity | SDLC Phase Mapping | Notes |
|-----------------|-------------------|-------|
| Sprint 0 (project kickoff) | Phase 1 + Phase 2 start | Establish business case, begin stakeholder analysis and initial requirements elicitation. Sprint 0 typically produces the business case, stakeholder register, and an initial set of epics/user stories. |
| Backlog refinement | Phase 2 (ongoing) | Refinement sessions are an elicitation and analysis activity. New requirements and changes are processed through the requirements change control process. |
| Architecture spike | Phase 3 | Time-boxed investigation to resolve architectural uncertainty. Produces ADRs and updates to the architecture description. |
| Technical story | Phase 4 | Design work captured as a technical story. Must produce or update design artifacts (data model, API spec, etc.) before implementation stories can begin. |
| Implementation story | Phase 5 | Code + unit tests for a specific feature or component. Must reference the design artifacts. Code review is required before the story is "done." |
| Testing within sprint | Phase 6 | Integration and regression tests executed within the sprint. Defects logged and triaged. |
| Sprint review / demo | Phase gate equivalent | The sprint review serves as an incremental phase gate. Stakeholders review working software and provide feedback. |
| Release sprint | Phase 7 | Deployment activities, release notes, and go/no-go review. |

### Agile Execution Rules

- [ ] 1. Artifacts are still required -- produced incrementally across sprints; all must exist before relevant phase gate
- [ ] 2. Phase gates are still required -- may be conducted as part of sprint reviews or as separate milestone meetings
- [ ] 3. Change control applies to baselined items -- changes go through formal change request process; product owner approves; RTM updated
- [ ] 4. Definition of Done incorporates framework requirements -- code reviewed, unit tests passing, design docs updated, RTM updated, test cases passing
- [ ] 5. Retrospectives feed process improvement -- improvements proposed through ADR process

---

## ISO 12207 Process Mapping

| ISO 12207 Process | GlowPowerRental Phase(s) | Specific Activities |
|-------------------|--------------------------|---------------------|
| Stakeholder Needs and Requirements Definition | Phase 1 (Business Analysis), Phase 2 (Requirements Engineering) | Business case development, stakeholder analysis, elicitation workshops, BRD creation |
| System/Software Requirements Definition | Phase 2 (Requirements Engineering) | Requirements analysis, classification, SRS creation, RTM creation, requirements validation |
| Architecture Definition | Phase 3 (System Architecture) | Architecture description, viewpoint definition, technology selection, ADR creation |
| Design Definition | Phase 4 (Design) | Component design, data modeling, API specification, UI wireframing |
| Implementation | Phase 5 (Development) | Coding, unit testing, code review |
| Integration | Phase 5 (Development), Phase 6 (Testing) | Component integration during development, integration testing during testing phase |
| Verification | Phase 6 (Testing) | Test planning, test case execution, defect tracking, test result analysis |
| Validation | Phase 6 (Testing) | User acceptance testing, stakeholder review of working software |
| Transition | Phase 7 (Deployment) | Deployment planning, environment configuration, release execution, post-deployment verification |
| Operation | Phase 8 (Operations) | System monitoring, incident response, routine maintenance |
| Maintenance | Phase 8 (Operations) | Patch management, performance tuning, minor enhancements (major enhancements re-enter at Phase 1) |
| Disposal | Phase 8 (Operations) | System decommissioning when end-of-life is reached (follows a separate decommission checklist) |
| Project Planning | Spans all phases | Sprint planning, resource allocation, timeline management |
| Project Assessment and Control | Spans all phases | Gate reviews, sprint reviews, status reporting, risk management |
| Decision Management | Phase 3 (System Architecture), all phases | ADRs in Phase 3; gate review decisions across all phases |
| Risk Management | Spans all phases | Risk identification in Phase 1, technical risk in Phase 3, quality risk in Phase 6, operational risk in Phase 8 |
| Configuration Management | Spans all phases | Version control, artifact management, baseline control, change tracking |
| Quality Assurance | Spans all phases | Standards compliance, artifact quality reviews, test coverage analysis |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Classification Standard | Standard | ../standards/requirements-classification.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| Conduct Stakeholder Analysis | Runbook | ../runbooks/conduct-stakeholder-analysis.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
