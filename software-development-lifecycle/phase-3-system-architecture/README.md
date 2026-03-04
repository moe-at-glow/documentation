# Phase 3: System Architecture

Defines the structure, components, interfaces, and deployment topology for GlowPowerRental, aligned with ISO/IEC/IEEE 42010.

All documents follow the **QRH (Quick Reference Handbook)** format. For background/educational content, see the `training/` subdirectory.

---

## Phase Summary

| Attribute | Detail |
|-----------|--------|
| Entry Criteria | Baselined BRD and SRS, populated RTM, validated Must Have requirements, assigned architect |
| Exit Criteria | Complete ADD with all viewpoints, ADRs documented, architecture review conducted, ADD approved, RTM updated |
| Key Roles | System Architect, Tech Lead, Product Owner, Infrastructure Engineer, QA Lead |
| ISO Alignment | ISO/IEC/IEEE 42010 - Architecture Description |

---

## Documentation

### Standards (compliance checklists)
- [Architecture Description Standard](standards/architecture-description-standard.md)
- [Architecture Decision Records Standard](standards/architecture-decision-records-standard.md)
- [System Decomposition Standard](standards/system-decomposition-standard.md)

### Runbooks (QRH procedures)
- [Create Architecture Description](runbooks/create-architecture-description.md)
- [Conduct Architecture Review](runbooks/conduct-architecture-review.md)
- [Write Architecture Decision Record](runbooks/write-architecture-decision-record.md)

### Guides (quick references)
- [Architecture Viewpoints Explained](guides/architecture-viewpoints-explained.md)
- [From Requirements to Architecture](guides/from-requirements-to-architecture.md)
- [Common Architecture Pitfalls](guides/common-architecture-pitfalls.md)

### Training Materials
- [Architecture Description Overview](guides/training/architecture-description-overview.md) -- Background on architecture documentation and ISO 42010

### References (decision aids)
- [Architecture Artifacts Checklist](references/architecture-artifacts-checklist.md)
- [Architecture Patterns Reference](references/architecture-patterns-reference.md)
- [Technology Evaluation Matrix](references/technology-evaluation-matrix.md)

### Templates
- [Architecture Description Document](templates/architecture-description-document.md)
- [Architecture Decision Record](templates/architecture-decision-record.md)
- [System Context Diagram](templates/system-context-diagram.md)
- [Component Diagram](templates/component-diagram.md)

### PlantUML Diagram Templates (`diagrams/`)

All architecture diagrams **must** be created as PlantUML `.puml` files. Copy these templates and fill in your project details:

| Diagram | Template | Required |
|---------|----------|----------|
| System Context | [system-context-diagram.puml](diagrams/system-context-diagram.puml) | All projects |
| Component Diagram | [component-diagram.puml](diagrams/component-diagram.puml) | All projects |
| Sequence Diagram | [sequence-diagram.puml](diagrams/sequence-diagram.puml) | All projects (top 3 workflows) |
| Deployment Diagram | [deployment-diagram.puml](diagrams/deployment-diagram.puml) | All projects |
| Entity-Relationship Diagram | [erd-diagram.puml](diagrams/erd-diagram.puml) | All projects |
| State Diagram | [state-diagram.puml](diagrams/state-diagram.puml) | All projects (key entities) |

---

## Entry Criteria

- [ ] Business Requirements Document (BRD) is baselined and approved.
- [ ] Software Requirements Specification (SRS) is baselined and approved.
- [ ] Requirements Traceability Matrix (RTM) is populated with BR-to-SWR links.
- [ ] All Must Have requirements have passed validation.
- [ ] System Architect and Tech Lead are assigned.

## Exit Criteria

- [ ] Architecture Description Document (ADD) is complete with all required viewpoints.
- [ ] All PlantUML diagrams committed to `diagrams/` directory (system-context, component, sequence, deployment, ERD, state).
- [ ] All architecture-significant decisions are documented as ADRs.
- [ ] Architecture review has been conducted.
- [ ] ADD is approved by Tech Lead, System Architect, and Product Owner.
- [ ] RTM is updated with architecture references.
