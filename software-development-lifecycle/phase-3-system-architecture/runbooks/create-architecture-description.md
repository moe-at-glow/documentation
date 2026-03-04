# Create Architecture Description

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P3-001 |
| **Owner** | Tech Lead |
| **Accountable** | Tech Lead |
| **SLA** | 10 business days |
| **Escalation** | Project Sponsor (scope issues), Product Owner (priority conflicts) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] BRD and SRS baselined (Phase 2 complete)
- [ ] Requirements Traceability Matrix populated
- [ ] System Architect and Tech Lead assigned
- [ ] Access to stakeholder register and communication plan granted

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| BRD or SRS not baselined | STOP. Complete Phase 2 first. | Product Owner |
| RTM has unresolved gaps | STOP. Resolve traceability gaps with BA. | Tech Lead |
| System Architect unavailable | STOP. Reassign or defer. | Project Sponsor |

---

## PROCEDURE

### Step 1: Review Baselined Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| Read BRD and list all business objectives | Tech Lead | 2 hours |
| Read SRS and list all software requirements by category (functional, non-functional, interface, data) | Tech Lead | 4 hours |
| Review RTM and confirm all BRs trace to SWRs | Tech Lead | 2 hours |
| Identify all external system interfaces mentioned in requirements | Tech Lead | 1 hour |
| Identify all user types and roles | Tech Lead | 1 hour |

- [ ] All business objectives listed
- [ ] All software requirements categorized
- [ ] All BRs trace to SWRs in RTM
- [ ] All external interfaces identified
- [ ] All user types and roles identified

### Step 2: Identify Architecture-Significant Requirements (ASRs)

| Action | Owner | SLA |
|--------|-------|-----|
| Filter requirements against ASR categories below | Tech Lead | 4 hours |
| Mark each ASR in the RTM | Tech Lead | 1 hour |

| ASR Category | Identification Criteria |
|-------------|------------------------|
| High-impact functional requirements | Features that define the system's core behavior |
| Quality attribute requirements | Non-functional requirements with measurable targets |
| System interface requirements | Integrations with external systems |
| Constraint requirements | Technology, regulatory, or infrastructure constraints |
| High-risk requirements | Features with significant technical uncertainty |

- [ ] ASR categories evaluated against all requirements
- [ ] 15-30 ASRs identified (typical range)
- [ ] Each ASR marked in RTM

> **IF** fewer than 15 ASRs identified **THEN** re-examine quality attribute and interface requirements for missed items
> **ELSE IF** more than 30 ASRs identified **THEN** re-evaluate; likely over-classifying non-architectural requirements
> **ELSE** proceed

### Step 3: Map Stakeholder Concerns to Viewpoints

| Action | Owner | SLA |
|--------|-------|-----|
| Review stakeholder register | Tech Lead | 1 hour |
| Map each stakeholder group to architecture concerns and viewpoints | Tech Lead | 2 hours |

| Stakeholder | Concern | Viewpoint |
|------------|---------|-----------|
| Product Owner | Business requirements coverage | System Context, Logical |
| Operations Staff | Daily usage workflows | System Context |
| Tech Lead | Build and maintain feasibility | Logical, Development |
| Infrastructure Engineer | Deployment, scaling | Deployment |
| QA Lead | Independent component testability | Logical, Development |
| Security Officer | Data protection | All viewpoints |

- [ ] All stakeholders mapped to concerns
- [ ] All concerns mapped to viewpoints

### Step 4: Create System Context Diagram

| Action | Owner | SLA |
|--------|-------|-----|
| Draw the system as a single box in the center | Tech Lead | 30 min |
| Identify every external entity (users, external systems, data sources) | Tech Lead | 1 hour |
| Draw each external entity around the system | Tech Lead | 1 hour |
| Draw and label lines with protocol, data direction, and data description | Tech Lead | 2 hours |
| Validate against SRS external interfaces | Tech Lead | 1 hour |

- [ ] System boundary drawn
- [ ] All user types shown (customers, staff, managers)
- [ ] All external systems shown (ERP, payment gateway, notification provider)
- [ ] All external data sources shown (IoT sensors, third-party APIs)
- [ ] Each line labeled with protocol (REST, MQTT, SMTP), direction, and data description
- [ ] Every external interface in SRS appears in diagram

> **IF** an SRS interface is missing from diagram **THEN** add the entity and relationship before proceeding
> **ELSE** proceed

### Step 5: Create Logical/Functional View

| Action | Owner | SLA |
|--------|-------|-----|
| Group related ASRs | Tech Lead | 1 hour |
| Identify components based on business capabilities per System Decomposition Standard | Tech Lead | 4 hours |
| Define name, responsibility, owned data, exposed interface, and dependencies for each component | Tech Lead | 4 hours |
| Draw component diagram with relationships | Tech Lead | 2 hours |
| Label each relationship with integration pattern (sync REST, async event, etc.) | Tech Lead | 1 hour |
| Validate every functional requirement maps to at least one component | Tech Lead | 2 hours |

- [ ] Components named (kebab-case)
- [ ] Each component has one-sentence responsibility
- [ ] Owned data defined per component
- [ ] Exposed interfaces defined per component
- [ ] Dependencies defined per component
- [ ] Integration patterns labeled
- [ ] Every functional requirement in SRS maps to at least one component

> **IF** a functional requirement has no component mapping **THEN** create a new component or extend an existing one
> **ELSE** proceed

### Step 6: Create Process/Runtime View

| Action | Owner | SLA |
|--------|-------|-----|
| Identify top 5 critical runtime scenarios | Tech Lead | 1 hour |
| Draw sequence or data flow diagram for each scenario | Tech Lead | 4 hours |
| Document all scheduled jobs | Tech Lead | 1 hour |

- [ ] 3 most common user workflows diagrammed
- [ ] Most complex async flow diagrammed
- [ ] Most critical batch process diagrammed
- [ ] Each diagram shows components, interaction order, sync/async calls, data transformations, error handling
- [ ] All scheduled jobs documented with trigger time, frequency, components, data processed

### Step 7: Create Deployment View

| Action | Owner | SLA |
|--------|-------|-----|
| List all infrastructure components (servers, databases, brokers, caches, load balancers) | Tech Lead | 1 hour |
| Define network topology (public vs. internal, segments, firewall rules) | Tech Lead | 2 hours |
| Map each software component to deployment target | Tech Lead | 2 hours |
| Document server specs, DB config, broker config, SSL/TLS termination, backup infrastructure | Tech Lead | 2 hours |
| Draw deployment diagram | Tech Lead | 2 hours |

- [ ] All infrastructure components listed
- [ ] Network topology defined
- [ ] Software-to-infrastructure mapping complete
- [ ] Server specifications documented (CPU, RAM, storage)
- [ ] Database configuration documented
- [ ] SSL/TLS termination point documented
- [ ] Backup infrastructure documented
- [ ] Deployment diagram drawn

> **IF** staging differs from production **THEN** document both environments
> **ELSE** document production only

### Step 8: Create Development View

| Action | Owner | SLA |
|--------|-------|-----|
| Define repository structure (monorepo vs. multi-repo) | Tech Lead | 1 hour |
| Document top-level directory organization | Tech Lead | 1 hour |
| Define package/module boundaries mapped to logical components | Tech Lead | 2 hours |
| Document build pipeline stages (lint, test, build, deploy) | Tech Lead | 1 hour |
| Define shared library strategy | Tech Lead | 1 hour |
| Document dependency management approach | Tech Lead | 1 hour |

- [ ] Repository structure defined
- [ ] Directory organization documented
- [ ] Package/module boundaries mapped to logical components
- [ ] Build pipeline stages documented
- [ ] Shared library strategy defined
- [ ] Dependency management approach documented

### Step 9: Document Technology Stack

| Action | Owner | SLA |
|--------|-------|-----|
| Create technology stack table with version, purpose, and rationale for each technology | Tech Lead | 2 hours |
| Identify which technology choices require ADRs | Tech Lead | 1 hour |

- [ ] All technologies listed with version, purpose, rationale
- [ ] ADR-requiring decisions identified

### Step 10: Write Architecture Decision Records

| Action | Owner | SLA |
|--------|-------|-----|
| Write ADR for each significant technology choice per ADR Standard | Tech Lead | 1 day |

Minimum ADRs required:
- [ ] Architecture style (monolith/microservices/modular monolith)
- [ ] Primary programming language and framework
- [ ] Database technology
- [ ] Message broker (if applicable)
- [ ] Authentication mechanism
- [ ] Hosting/infrastructure platform

> **IF** a technology choice is straightforward and uncontested **THEN** write a brief ADR
> **ELSE IF** multiple viable alternatives exist **THEN** write a full ADR with comparison matrix
> **ELSE** document informally in ADD

### Step 11: Conduct Architecture Review

| Action | Owner | SLA |
|--------|-------|-----|
| Execute the Conduct Architecture Review runbook | Tech Lead | 1 day |

- [ ] Architecture review completed per [conduct-architecture-review.md](conduct-architecture-review.md)

### Step 12: Obtain Architecture Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Present final ADD to approval authority | Tech Lead | 2 hours |
| Walk through each viewpoint | Tech Lead | 1 hour |
| Confirm all ASRs addressed | Tech Lead | 30 min |
| Confirm all stakeholder concerns covered | Tech Lead | 30 min |
| Obtain written sign-off from System Architect, Tech Lead, Product Owner | Tech Lead | 1 day |
| Record approved ADD version as baseline | Tech Lead | 30 min |
| Update RTM with architecture references | Tech Lead | 1 hour |

- [ ] System Architect signed off (technical integrity)
- [ ] Tech Lead signed off (implementation feasibility)
- [ ] Product Owner signed off (business alignment)
- [ ] ADD version recorded as approved baseline
- [ ] RTM updated with architecture references

> **IF** sign-off refused **THEN** document objections and return to relevant step
> **ELSE** proceed to baseline

---

## EXIT CRITERIA

- [ ] ADD complete with all five viewpoints (Context, Logical, Process, Deployment, Development)
- [ ] All ASRs addressed in architecture
- [ ] All stakeholder concerns mapped and covered
- [ ] All ADRs written and approved
- [ ] Architecture review conducted with no open blockers
- [ ] Written sign-off obtained from System Architect, Tech Lead, Product Owner
- [ ] RTM updated with architecture references

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Architecture Description Document (ADD) | [ADD Template](../templates/architecture-description-document.md) | `architecture/` |
| Architecture Decision Records (ADRs) | [ADR Template](../templates/architecture-decision-record.md) | `architecture/decisions/` |
| System Context Diagram | [System Context Diagram Template](../templates/system-context-diagram.md) | `architecture/diagrams/` |
| Component Diagram | [Component Diagram Template](../templates/component-diagram.md) | `architecture/diagrams/` |
| Deployment Diagram | -- | `architecture/diagrams/` |
| Sequence Diagrams (top 5 scenarios) | -- | `architecture/diagrams/` |
| Technology Stack Document | -- | `architecture/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Architecture Description Standard | Standard | [../standards/architecture-description-standard.md](../standards/architecture-description-standard.md) |
| ADR Standard | Standard | [../standards/architecture-decision-records-standard.md](../standards/architecture-decision-records-standard.md) |
| System Decomposition Standard | Standard | [../standards/system-decomposition-standard.md](../standards/system-decomposition-standard.md) |
| ADD Template | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
| ADR Template | Template | [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md) |
| System Context Diagram Template | Template | [../templates/system-context-diagram.md](../templates/system-context-diagram.md) |
| Component Diagram Template | Template | [../templates/component-diagram.md](../templates/component-diagram.md) |
| Conduct Architecture Review | Runbook | [conduct-architecture-review.md](conduct-architecture-review.md) |
