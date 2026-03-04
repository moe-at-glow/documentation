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

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 14 | System Context Viewpoint: show system boundary, all external systems (with protocol/format), all user types, all data flows crossing boundary | All projects | [ ] Box-and-line diagram with all required elements present | Rework required |
| 15 | Logical/Functional Viewpoint: show every component with name, responsibility summary, exposed interfaces, consumed interfaces | All projects | [ ] Component diagram complete | Rework required |
| 16 | Process/Runtime Viewpoint: document top 3 user workflows, async flows, scheduled/batch flows, error/retry flows | All projects | [ ] Sequence/data flow diagrams for all required scenarios | Rework required |
| 17 | Deployment Viewpoint: show all servers/nodes, network boundaries, load balancers, databases, message brokers, external connections, environment labels | All projects | [ ] Deployment diagram covers production topology | Rework required |
| 18 | Development Viewpoint: show repository structure, major directories, package/module organization, build pipeline stages, dependency relationships | All projects | [ ] Directory tree or module dependency diagram present | Rework required |

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
- [ ] System Context Viewpoint diagram present with system boundary, external systems, user types, data flows
- [ ] Logical/Functional Viewpoint diagram present with all components, responsibilities, interfaces
- [ ] Process/Runtime Viewpoint covers top 3 workflows, async flows, batch flows, error flows
- [ ] Deployment Viewpoint diagram covers production topology with all required elements
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
