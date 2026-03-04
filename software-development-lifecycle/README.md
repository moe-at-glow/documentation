# Software Development Lifecycle

Central framework for GlowPowerRental software project delivery.

All documents follow the **QRH (Quick Reference Handbook)** format with metadata headers, actionable checklists, and cross-references. Background and educational content lives in `guides/training/` subdirectories.

**Diagramming Standard:** All architecture and design diagrams must be created as **PlantUML** (`.puml`) files. Templates are available in `phase-3-system-architecture/diagrams/` and `phase-4-design/diagrams/`.

---

## Framework Alignment

| Standard | Scope | Role in Framework |
|----------|-------|-------------------|
| ISO/IEC/IEEE 12207 | Software Life Cycle Processes | Defines lifecycle phases and governance |
| ISO/IEC/IEEE 29148 | Requirements Engineering | Defines how requirements are elicited, analyzed, specified, and validated |
| ISO/IEC/IEEE 42010 | Architecture Description | Defines how system architecture is documented |

---

## SDLC Phases

| Phase | Description | Status | Documentation |
|-------|-------------|--------|---------------|
| 1. Business Analysis | Identify business needs and opportunities | **Fully documented** | [Phase 1](phase-1-business-analysis/) |
| 2. Requirements Engineering | Elicit, analyze, specify, and validate requirements | **Fully documented** | [Phase 2](phase-2-requirements-engineering/) |
| 3. System Architecture | Define system structure, components, and interfaces | **Fully documented** | [Phase 3](phase-3-system-architecture/) |
| 4. Design | Detail component design and data models | **Fully documented** | [Phase 4](phase-4-design/) |
| 5. Development | Implement software components | **Fully documented** | [Phase 5](phase-5-development/) |
| 6. Testing | Verify and validate against requirements | **Fully documented** | [Phase 6](phase-6-testing/) |
| 7. Deployment | Release to production environments | Planned | -- |
| 8. Operations | Monitor, maintain, and support | Planned | -- |

---

## Documentation Structure

All documents use the QRH format. Document types serve different operational purposes:

| Looking for... | Go to | Document type |
|----------------|-------|---------------|
| A compliance rule or convention | [standards/](standards/) | Compliance checklists |
| A step-by-step procedure | [runbooks/](runbooks/) | QRH procedure checklists |
| A quick-reference on a topic | [guides/](guides/) | Quick reference cards |
| Background or educational content | `guides/training/` | Training material (not operational) |
| A specific value or fact | [references/](references/) | Decision aids and lookup tables |
| A copy-paste starting point | [templates/](templates/) | Operational templates |
| A design decision and its rationale | [architecture/decisions/](architecture/decisions/) | ADRs |

> **Note:** Each phase's `guides/` directory contains a `training/` subdirectory with overview and educational documents. These provide onboarding context, not operational procedures.

---

## Phase 1: Business Analysis

Full documentation: [Phase 1 README](phase-1-business-analysis/)

Key documents:
- [Business Case Standard](phase-1-business-analysis/standards/business-case-standard.md)
- [Project Charter Standard](phase-1-business-analysis/standards/project-charter-standard.md)
- [Stakeholder Management Standard](phase-1-business-analysis/standards/stakeholder-management-standard.md)
- [Develop Business Case Runbook](phase-1-business-analysis/runbooks/develop-business-case.md)
- [Create Project Charter Runbook](phase-1-business-analysis/runbooks/create-project-charter.md)
- [Business Value Assessment Reference](phase-1-business-analysis/references/business-value-assessment-reference.md)
- Training: [Business Analysis Overview](phase-1-business-analysis/guides/training/business-analysis-overview.md)

---

## Phase 2: Requirements Engineering

Full documentation: [Phase 2 README](phase-2-requirements-engineering/)

Key documents:
- [SDLC Framework](standards/sdlc-framework.md)
- [Requirements Engineering Standard](phase-2-requirements-engineering/standards/requirements-engineering-standard.md)
- [Requirements Classification](phase-2-requirements-engineering/standards/requirements-classification.md)
- [Requirements Traceability](phase-2-requirements-engineering/standards/requirements-traceability.md)
- [Conduct Stakeholder Analysis](phase-2-requirements-engineering/runbooks/conduct-stakeholder-analysis.md)
- [Extract Business Requirements](phase-2-requirements-engineering/runbooks/extract-business-requirements.md)
- [Derive Software Requirements](phase-2-requirements-engineering/runbooks/derive-software-requirements.md)
- [Validate Requirements](phase-2-requirements-engineering/runbooks/validate-requirements.md)
- [Manage Requirements Changes](phase-2-requirements-engineering/runbooks/manage-requirements-changes.md)
- Training: [Requirements Engineering Overview](phase-2-requirements-engineering/guides/training/requirements-engineering-overview.md)

---

## Phase 3: System Architecture

Full documentation: [Phase 3 README](phase-3-system-architecture/)

Key documents:
- [Architecture Description Standard](phase-3-system-architecture/standards/architecture-description-standard.md)
- [Architecture Decision Records Standard](phase-3-system-architecture/standards/architecture-decision-records-standard.md)
- [System Decomposition Standard](phase-3-system-architecture/standards/system-decomposition-standard.md)
- [Architecture Viewpoints Explained](phase-3-system-architecture/guides/architecture-viewpoints-explained.md)
- [From Requirements to Architecture](phase-3-system-architecture/guides/from-requirements-to-architecture.md)
- Training: [Architecture Description Overview](phase-3-system-architecture/guides/training/architecture-description-overview.md)

---

## Phase 4: Design

Full documentation: [Phase 4 README](phase-4-design/)

Key documents:
- [Detailed Design Standard](phase-4-design/standards/detailed-design-standard.md)
- [API Design Standard](phase-4-design/standards/api-design-standard.md)
- [Database Design Standard](phase-4-design/standards/database-design-standard.md)
- [Design Patterns Guide](phase-4-design/guides/design-patterns-guide.md)
- [From Architecture to Design](phase-4-design/guides/from-architecture-to-design.md)
- Training: [Design Phase Overview](phase-4-design/guides/training/design-phase-overview.md)

---

## Phase 5: Development

Full documentation: [Phase 5 README](phase-5-development/)

Key documents:
- [Coding Standards](phase-5-development/standards/coding-standards.md)
- [Git Workflow Standard](phase-5-development/standards/git-workflow-standard.md)
- [Code Review Standard](phase-5-development/standards/code-review-standard.md)
- [Unit Testing Standard](phase-5-development/standards/unit-testing-standard.md)
- [Implement Feature Runbook](phase-5-development/runbooks/implement-feature.md)
- Training: [Development Phase Overview](phase-5-development/guides/training/development-phase-overview.md)

---

## Phase 6: Testing

Full documentation: [Phase 6 README](phase-6-testing/)

Key documents:
- [Testing Strategy Standard](phase-6-testing/standards/testing-strategy-standard.md)
- [Integration Testing Standard](phase-6-testing/standards/integration-testing-standard.md)
- [Performance Testing Standard](phase-6-testing/standards/performance-testing-standard.md)
- [Security Testing Standard](phase-6-testing/standards/security-testing-standard.md)
- [Execute Test Cycle Runbook](phase-6-testing/runbooks/execute-test-cycle.md)
- Training: [Testing Phase Overview](phase-6-testing/guides/training/testing-phase-overview.md)

---

## Example Project

A complete worked example using **Power Atlas** (GlowPowerRental's power calculation tool) with filled-in artifacts for every phase. Use as a reference when creating your own project artifacts.

**[View Example Project](example-project/)**
