# System Decomposition Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P3-003 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Architecture Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Component identification and service boundaries required; formal interface specs optional (inline code docs acceptable)
> **IF** medium project (3-5 devs) **THEN** Full component identification, service boundaries, and interface specs required; dependency rules enforced
> **IF** large project (6+ devs) **THEN** Full compliance required including all integration patterns documented and dependency rules strictly enforced

---

## COMPLIANCE REQUIREMENTS

### Component Identification

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Each component has a clearly defined single responsibility (one reason to change) | All components | [ ] Responsibility statement present per component | Rework required |
| 2 | Each component exposes a well-defined interface | All components | [ ] Interface documented | Rework required |
| 3 | Each component can be developed and tested independently | All components | [ ] Independent testability confirmed | Rework required |
| 4 | Components identified by mapping business capabilities to services | All projects | [ ] Business capability-to-component mapping documented | Rework required |
| 5 | Single Responsibility Principle applied: no component has multiple unrelated responsibilities | All components | [ ] SRP verified per component | Rework required |
| 6 | Components that always change together are evaluated for merging | All components | [ ] Change coupling analysis documented | Rework required |
| 7 | Each component owns its data; no cross-boundary direct database access | All components | [ ] Data ownership boundaries verified | Block deployment |

### Service Boundary Definition

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 8 | Each service defines a Responsibility Statement (one sentence) | All services | [ ] Statement present | Rework required |
| 9 | Each service defines Owned Data (source-of-truth tables/entities) | All services | [ ] Owned data listed | Rework required |
| 10 | Each service defines Exposed Interface (API endpoints/methods) | All services | [ ] Exposed interface documented | Rework required |
| 11 | Each service defines Consumed Interfaces (dependencies on other services) | All services | [ ] Consumed interfaces listed | Rework required |
| 12 | Each service defines Events Published | All services | [ ] Published events listed | Rework required |
| 13 | Each service defines Events Consumed | All services | [ ] Consumed events listed | Rework required |

### Interface Specification -- REST APIs

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 14 | Endpoint URL and HTTP method documented | All REST interfaces | [ ] Present | Block integration |
| 15 | Request parameters (path, query, body) documented | All REST interfaces | [ ] Present | Block integration |
| 16 | Request body schema with types and constraints documented | All REST interfaces | [ ] Present | Block integration |
| 17 | Response schema with types documented | All REST interfaces | [ ] Present | Block integration |
| 18 | Error response codes and messages documented | All REST interfaces | [ ] Present | Block integration |
| 19 | Authentication requirement documented | All REST interfaces | [ ] Present | Block integration |
| 20 | Rate limiting documented | REST interfaces where applicable | [ ] Present if applicable | Rework required |
| 21 | Pagination documented | REST interfaces returning lists | [ ] Present if returning lists | Rework required |

### Interface Specification -- Message/Event Interfaces

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 22 | Topic/queue name documented | All message interfaces | [ ] Present | Block integration |
| 23 | Message schema with types documented | All message interfaces | [ ] Present | Block integration |
| 24 | Publishing trigger documented | All message interfaces | [ ] Present | Block integration |
| 25 | Delivery guarantee documented (at-most-once, at-least-once, exactly-once) | All message interfaces | [ ] Present | Block integration |
| 26 | Message ordering requirements documented | Message interfaces where applicable | [ ] Present if applicable | Rework required |
| 27 | Consumer group / subscription model documented | All message interfaces | [ ] Present | Block integration |

### Integration Patterns

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Each component interaction specifies its integration pattern | All interactions | [ ] Pattern selected and documented | Rework required |

Valid patterns:

| Pattern | When to Use |
|---------|------------|
| Synchronous REST | Request needs immediate response; caller blocks |
| Asynchronous Messaging | Producer does not wait for consumer; decoupled processing |
| Event-Driven | Multiple consumers react to the same event independently |
| Batch/Scheduled | Processing large datasets periodically |
| Webhook | External system notifies our system |

### Component Naming Conventions

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 29 | Service names use kebab-case, ending with -service | All services | [ ] Naming verified | Rework required |
| 30 | API resources use plural noun, kebab-case | All API resources | [ ] Naming verified | Rework required |
| 31 | Event/message topics use dot-separated, past tense for events | All topics | [ ] Naming verified | Rework required |
| 32 | Databases use snake_case, prefixed with service name | All databases | [ ] Naming verified | Rework required |
| 33 | Queue names use dot-separated format | All queues | [ ] Naming verified | Rework required |

### Dependency Rules -- Allowed

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 34 | Any service may depend on API Gateway | All services | [ ] Dependency direction verified | N/A |
| 35 | Business service may depend on business service via defined interface only (never direct DB) | Business services | [ ] Interface-only access verified | Block deployment |
| 36 | Any service may depend on shared libraries (logging, auth, validation) | All services | [ ] Shared lib usage verified | N/A |
| 37 | Any service may depend on infrastructure services (database, message broker, cache) | All services | [ ] Infrastructure dependency verified | N/A |

### Dependency Rules -- Forbidden

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 38 | No direct database access across service boundaries | All services | [ ] No cross-boundary DB access | Block deployment |
| 39 | No circular dependencies (A -> B -> A) | All services | [ ] Dependency graph acyclic | Block deployment |
| 40 | No business logic in API Gateway (routing, auth, rate limiting only) | API Gateway | [ ] Gateway logic reviewed | Block deployment |
| 41 | No shared mutable state (shared DB table, shared file) | All services | [ ] No shared mutable state | Block deployment |

---

## COMPLIANCE CHECKLIST

- [ ] All components identified from business capability mapping
- [ ] Each component has single responsibility, well-defined interface, independent testability
- [ ] Each component owns its data exclusively
- [ ] Service boundary defined for each service (responsibility, owned data, exposed/consumed interfaces, events published/consumed)
- [ ] All REST API interfaces fully specified (endpoint, params, schemas, errors, auth, rate limiting, pagination)
- [ ] All message/event interfaces fully specified (topic, schema, trigger, delivery guarantee, ordering, consumer model)
- [ ] Integration pattern selected and documented for each component interaction
- [ ] Naming conventions followed (kebab-case services, plural kebab-case resources, dot-separated topics, snake_case DBs, dot-separated queues)
- [ ] No forbidden dependencies (cross-boundary DB access, circular deps, business logic in gateway, shared mutable state)
- [ ] All allowed dependencies use defined interfaces only

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Architecture Description | Runbook | [../runbooks/create-architecture-description.md](../runbooks/create-architecture-description.md) |
| Conduct Architecture Review | Runbook | [../runbooks/conduct-architecture-review.md](../runbooks/conduct-architecture-review.md) |
| Component Diagram | Template | [../templates/component-diagram.md](../templates/component-diagram.md) |
| Architecture Description Document | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
