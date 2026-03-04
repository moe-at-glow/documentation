# Architecture Description Overview

How system architecture description works at GlowPowerRental and why it matters.

---

## What Is Architecture Description

Architecture description is the process of defining and documenting the fundamental structure of a software system. It answers questions that requirements alone cannot:

- **Requirements say:** "The system shall track 500+ IoT sensors in real time."
- **Architecture says:** "We will use an MQTT broker to receive sensor data, a time-series database to store it, and a WebSocket connection to push updates to the dashboard."

Architecture bridges the gap between **what the system must do** (requirements) and **how the system is organized to do it** (design and implementation).

---

## Why Architecture Matters

| Without Architecture | With Architecture |
|---------------------|-------------------|
| Developers make independent, inconsistent technology choices | A coherent technology stack is defined upfront |
| Components grow organically with unclear boundaries | Components have clear responsibilities and interfaces |
| Performance and security are addressed reactively (in production) | Quality attributes are addressed structurally (by design) |
| New team members cannot understand the system as a whole | A single document explains the entire system |
| Changes in one area cause unexpected breakage elsewhere | Dependencies are documented and managed |

The cost of changing architecture increases exponentially as development progresses. Getting architecture right in Phase 3 prevents expensive rework in Phases 5-8.

---

## ISO/IEC/IEEE 42010 in Plain Language

ISO 42010 provides a framework for architecture description. Here are its concepts in plain language:

```
Stakeholders have CONCERNS about the system.
   |
   v
Concerns are addressed by VIEWPOINTS.
   |
   v
Each viewpoint produces a VIEW (a diagram + description).
   |
   v
Architecture DECISIONS are made to resolve trade-offs.
   |
   v
All of this is captured in the ARCHITECTURE DESCRIPTION document.
```

| ISO 42010 Term | Plain Language | GlowPowerRental Example |
|---------------|---------------|------------------------|
| System of Interest | The thing we are building | The rental management platform |
| Stakeholder | A person who cares about the system | Operations Manager, CTO, Developers |
| Concern | Something a stakeholder cares about | "Can it handle 500 concurrent users?" |
| Viewpoint | A perspective from which to examine the architecture | Deployment viewpoint (where things run) |
| View | The actual diagram and description for a viewpoint | The deployment diagram showing servers and networks |
| Architecture Decision | A choice that shapes the system | "Use PostgreSQL because we need ACID for financial data" |
| Rationale | The reasoning behind a decision | Documented in ADRs |

---

## How Requirements Feed Into Architecture

```
Phase 2 Output                    Phase 3 Activity
+-------------------------+      +----------------------------------+
| Functional Requirements |----->| Component identification         |
| (SWR-xxx)               |      | (what components are needed)     |
+-------------------------+      +----------------------------------+

+-------------------------+      +----------------------------------+
| Non-Functional Reqs     |----->| Quality attribute approaches     |
| (Performance, Security) |      | (how to achieve performance,     |
+-------------------------+      |  security, scalability)          |
                                 +----------------------------------+

+-------------------------+      +----------------------------------+
| Interface Requirements  |----->| Integration architecture         |
| (External systems)      |      | (protocols, patterns, contracts) |
+-------------------------+      +----------------------------------+

+-------------------------+      +----------------------------------+
| Data Requirements       |----->| Data architecture                |
| (Storage, retention)    |      | (databases, data flow, storage)  |
+-------------------------+      +----------------------------------+
```

---

## Architecture in Agile

Architecture is not a waterfall-only activity. In Agile execution:

**Evolutionary Architecture:** Start with the simplest architecture that supports current requirements. Evolve it as new requirements emerge. But always document decisions.

**Architecture Runway:** Establish enough architectural foundation to support upcoming sprints. Do not architect the entire system upfront, but do not skip architecture entirely.

**Architecture Spikes:** Use time-boxed spikes (1-2 days) to explore architectural options before committing. Document findings as ADRs.

| Agile Practice | Architecture Activity |
|---------------|----------------------|
| Sprint 0 / Inception | Initial architecture: system context, component identification, key ADRs |
| Sprint Planning | Identify if upcoming stories require architecture changes |
| During Sprints | Architecture spikes for uncertain areas |
| Sprint Review | Review architecture impact of delivered features |
| Retrospective | Assess if architecture is supporting or hindering development |

---

## Common Architecture Styles

| Style | Description | Best For | Trade-offs |
|-------|------------|----------|------------|
| Monolith | Single deployable unit containing all functionality | Small teams (1-5 devs), early-stage products, simple domains | Simple to deploy and debug. Hard to scale independently. Hard to maintain as codebase grows. |
| Modular Monolith | Single deployable unit with clear internal module boundaries | Medium teams, growing products, preparation for future decomposition | Module boundaries enforce separation. Can evolve to microservices. Still a single deployment. |
| Microservices | Multiple independently deployable services | Large teams (10+), complex domains, high scalability needs | Independent scaling and deployment. High operational complexity. Network latency between services. |
| Event-Driven | Components communicate through events/messages | Systems with async workflows, IoT data ingestion, decoupled processing | Loose coupling, high throughput. Hard to debug, eventual consistency. |

**GlowPowerRental recommendation:** For most projects, start with a **modular monolith** and extract services only when a specific module has different scaling, deployment, or team ownership needs. This avoids the operational overhead of microservices while maintaining clean boundaries.

---

## Architecture Decision Matrix

When choosing an architecture style, evaluate:

| Factor | Monolith | Modular Monolith | Microservices |
|--------|----------|------------------|---------------|
| Team size 1-5 | Best fit | Good fit | Overkill |
| Team size 6-15 | Risky | Best fit | Good fit |
| Team size 15+ | Not viable | Possible | Best fit |
| Simple domain | Best fit | Acceptable | Overkill |
| Complex domain | Risky | Good fit | Best fit |
| Need independent scaling | Not possible | Not possible | Best fit |
| Need fast time to market | Best fit | Good fit | Slow |
| DevOps maturity: low | Best fit | Good fit | High risk |
| DevOps maturity: high | Acceptable | Good fit | Best fit |

---

## GlowPowerRental Architecture Evolution

```
Phase 1: MVP (current)
+------------------------------------------+
| Single Node.js Application (Monolith)    |
| - All business logic in one codebase     |
| - PostgreSQL for all data                |
| - Mosquitto for IoT (separate process)   |
| - Single DigitalOcean droplet            |
+------------------------------------------+

Phase 2: Growth
+------------------------------------------+
| Modular Monolith                          |
| - Clear module boundaries                |
| - Shared database with schema separation |
| - Mosquitto + Redis added                |
| - Separate worker for async jobs         |
+------------------------------------------+

Phase 3: Scale (if needed)
+------------------------------------------+
| Service Extraction                        |
| - Telemetry Service extracted (IoT)      |
| - Billing Service extracted (payments)    |
| - Core Rental Service remains monolith   |
| - Event-driven communication added       |
+------------------------------------------+
```

Each transition should be documented with ADRs explaining why and when the evolution occurred.
