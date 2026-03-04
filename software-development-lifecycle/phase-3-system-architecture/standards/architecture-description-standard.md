# Architecture Description Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P3-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Architecture Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 1-5, 10, 11 required; remaining sections optional
> **IF** medium project (3-5 devs) **THEN** All sections required; viewpoints may combine Deployment and Development into one
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### ADD Structure

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | ADD must contain Section 1: Introduction (purpose, scope, definitions, references) | All projects | [ ] Section present and complete | Block architecture review |
| 2 | ADD must contain Section 2: Architecture Goals and Constraints | All projects | [ ] Business and technical drivers documented | Block architecture review |
| 3 | ADD must contain Section 3: Stakeholder Concerns (mapped from stakeholder analysis) | All projects | [ ] Concerns mapped to viewpoints | Block architecture review |
| 4 | ADD must contain Section 4: System Context View | All projects | [ ] System boundary and external interactions shown | Block architecture review |
| 5 | ADD must contain Section 5: Logical/Functional View | All projects | [ ] Components, responsibilities, interfaces documented | Block architecture review |
| 6 | ADD must contain Section 6: Process/Runtime View | All projects | [ ] Data flows, concurrency, communication shown | Block architecture review |
| 7 | ADD must contain Section 7: Deployment View | All projects | [ ] Infrastructure, networking, environments documented | Block architecture review |
| 8 | ADD must contain Section 8: Development View | All projects | [ ] Code organization, build structure, repositories shown | Block architecture review |
| 9 | ADD must contain Section 9: Quality Attribute Approaches | All projects | [ ] Performance, security, scalability, reliability strategies listed | Block architecture review |
| 10 | ADD must contain Section 10: Technology Stack (with rationale) | All projects | [ ] Technologies listed with selection rationale | Block architecture review |
| 11 | ADD must contain Section 11: Architecture Decisions (ADR references) | All projects | [ ] ADRs referenced | Block architecture review |
| 12 | ADD must contain Section 12: Risks and Mitigations | All projects | [ ] Known architectural risks documented | Block architecture review |
| 13 | ADD must contain Section 13: Traceability (requirements-to-architecture mapping) | All projects | [ ] Mapping present and complete | Block architecture review |

### Mandatory Viewpoints

All viewpoint diagrams **must** be created as PlantUML `.puml` files and committed to the `diagrams/` directory. Use the PlantUML templates in `diagrams/` as starting points.

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 14 | System Context Viewpoint: show system boundary, all external systems (with protocol/format), all user types, all data flows crossing boundary. **Deliver as PlantUML `.puml` file.** | All projects | [ ] `diagrams/system-context-diagram.puml` committed and valid | Rework required |
| 15 | Logical/Functional Viewpoint: show every component with name, responsibility summary, exposed interfaces, consumed interfaces. **Deliver as PlantUML `.puml` file.** | All projects | [ ] `diagrams/component-diagram.puml` committed and valid | Rework required |
| 16 | Process/Runtime Viewpoint: document top 3 user workflows, async flows, scheduled/batch flows, error/retry flows. **Deliver as PlantUML `.puml` files (one per scenario).** | All projects | [ ] `diagrams/sequence-*.puml` files committed for all required scenarios | Rework required |
| 17 | Deployment Viewpoint: show all servers/nodes, network boundaries, load balancers, databases, message brokers, external connections, environment labels. **Deliver as PlantUML `.puml` file.** | All projects | [ ] `diagrams/deployment-diagram.puml` committed and valid | Rework required |
| 18 | Development Viewpoint: show repository structure, major directories, package/module organization, build pipeline stages, dependency relationships | All projects | [ ] Directory tree or module dependency diagram present | Rework required |
| 18a | Entity-Relationship Diagram: show all data entities, attributes, and relationships. **Deliver as PlantUML `.puml` file.** | All projects | [ ] `diagrams/erd-diagram.puml` committed and valid | Rework required |
| 18b | State Diagrams: show lifecycle states for key domain entities. **Deliver as PlantUML `.puml` files.** | All projects | [ ] `diagrams/state-*.puml` files committed for key entities | Rework required |

### Architecture Concerns Mapping

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 19 | Every stakeholder concern must map to at least one viewpoint | All projects | [ ] Concern-to-viewpoint traceability complete | Rework required |

Reference mapping:

| Concern Category | Typical Viewpoint |
|-----------------|-------------------|
| What the system does | Logical View |
| How data flows | Process View |
| Where it runs | Deployment View |
| How it handles load | Deployment + Process View |
| How it stays secure | All Views |
| How code is organized | Development View |

### Quality Attributes

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 20 | Performance approach documented (caching, connection pooling, async processing, CDN) | All projects | [ ] Strategy defined | Block deployment |
| 21 | Security approach documented (auth mechanism, authorization model, encryption, secrets management) | All projects | [ ] Strategy defined | Block deployment |
| 22 | Scalability approach documented (horizontal/vertical scaling, stateless design, DB scaling) | All projects | [ ] Strategy defined | Block deployment |
| 23 | Reliability approach documented (redundancy, failover, health checks, circuit breakers, retries) | All projects | [ ] Strategy defined | Block deployment |
| 24 | Maintainability approach documented (modularity, loose coupling, DI, config externalization) | All projects | [ ] Strategy defined | Block deployment |

### Technology Selection

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 25 | Every technology choice documented with: name/version, purpose, alternatives considered, selection rationale, risks, license | All tech selections | [ ] All fields populated per technology | Rework required |
| 26 | Significant technology choices (database, framework, message broker, cloud provider) require a formal ADR | Major selections | [ ] ADR exists and is referenced | Block architecture review |

### Naming Conventions

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 27 | Service/Component names use kebab-case | All components | [ ] Naming verified | Rework required |
| 28 | API endpoints use /api/v{N}/{resource} format | All APIs | [ ] URL format verified | Rework required |
| 29 | Database names use snake_case | All databases | [ ] Naming verified | Rework required |
| 30 | Table names use plural snake_case | All tables | [ ] Naming verified | Rework required |
| 31 | Message queue/topic names use dot-separated format | All queues/topics | [ ] Naming verified | Rework required |
| 32 | Environment variables use SCREAMING_SNAKE_CASE | All env vars | [ ] Naming verified | Rework required |
| 33 | Configuration files use kebab-case | All config files | [ ] Naming verified | Rework required |

---

## COMPLIANCE CHECKLIST

- [ ] ADD contains all 13 required sections
- [ ] All diagrams created as PlantUML `.puml` files in `diagrams/` directory
- [ ] `diagrams/system-context-diagram.puml` -- system boundary, external systems, user types, data flows
- [ ] `diagrams/component-diagram.puml` -- all components, responsibilities, interfaces
- [ ] `diagrams/sequence-*.puml` -- top 3 workflows, async flows, batch flows, error flows
- [ ] `diagrams/deployment-diagram.puml` -- production topology with all required elements
- [ ] `diagrams/erd-diagram.puml` -- all data entities, attributes, relationships
- [ ] `diagrams/state-*.puml` -- lifecycle states for key domain entities
- [ ] Development Viewpoint shows repository structure, packages, build pipeline
- [ ] Every stakeholder concern maps to at least one viewpoint
- [ ] Quality attribute approaches documented for performance, security, scalability, reliability, maintainability
- [ ] Every technology choice has name/version, purpose, alternatives, rationale, risks, license
- [ ] Significant technology choices have formal ADRs
- [ ] All naming conventions followed (kebab-case services, /api/v{N}/{resource} endpoints, snake_case DBs/tables, dot-separated topics, SCREAMING_SNAKE_CASE env vars, kebab-case configs)
- [ ] Requirements-to-architecture traceability mapping complete
- [ ] Architectural risks and mitigations documented

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Architecture Description | Runbook | [../runbooks/create-architecture-description.md](../runbooks/create-architecture-description.md) |
| Conduct Architecture Review | Runbook | [../runbooks/conduct-architecture-review.md](../runbooks/conduct-architecture-review.md) |
| Architecture Description Document | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
| System Context Diagram | Template | [../templates/system-context-diagram.md](../templates/system-context-diagram.md) |
| Component Diagram | Template | [../templates/component-diagram.md](../templates/component-diagram.md) |
| System Context Diagram (PlantUML) | Diagram Template | [../diagrams/system-context-diagram.puml](../diagrams/system-context-diagram.puml) |
| Component Diagram (PlantUML) | Diagram Template | [../diagrams/component-diagram.puml](../diagrams/component-diagram.puml) |
| Sequence Diagram (PlantUML) | Diagram Template | [../diagrams/sequence-diagram.puml](../diagrams/sequence-diagram.puml) |
| Deployment Diagram (PlantUML) | Diagram Template | [../diagrams/deployment-diagram.puml](../diagrams/deployment-diagram.puml) |
| ERD (PlantUML) | Diagram Template | [../diagrams/erd-diagram.puml](../diagrams/erd-diagram.puml) |
| State Diagram (PlantUML) | Diagram Template | [../diagrams/state-diagram.puml](../diagrams/state-diagram.puml) |
