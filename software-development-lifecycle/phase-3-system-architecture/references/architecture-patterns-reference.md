# Architecture Patterns Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P3-002 |
| **Use When** | Selecting an architecture pattern for a new system or major component |
| **Last Updated** | 2026-03-04 |

---

## Pattern Lookup Table

| Pattern | Description | When to Use | Pros | Cons | GlowPowerRental Applicability |
|---------|-------------|------------|------|------|-------------------------------|
| **Layered** | Organizes code into horizontal layers (presentation, business logic, data access). Each layer only calls the layer directly below it. | General-purpose web applications. Good default for most projects. | Simple to understand, enforces separation of concerns, well-known pattern. | Can become rigid, performance overhead from layer traversal, tendency toward anemic domain models. | **High.** Default for most GlowPowerRental web applications. |
| **Modular Monolith** | Single deployable unit with strict internal module boundaries. Each module owns its data and exposes a defined interface. | Small-to-medium teams building applications that may need to scale later. | Simplicity of monolith deployment with modularity of services. Easier to refactor than microservices. | Requires discipline to maintain module boundaries. Single deployment means all-or-nothing releases. | **High.** Recommended default for GlowPowerRental projects. |
| **Microservices** | Multiple independently deployable services, each owning its data. Services communicate via APIs or events. | Large teams (10+), complex domains, need for independent scaling and deployment. | Independent scaling, technology diversity, team autonomy, fault isolation. | Operational complexity, distributed debugging, network latency, data consistency challenges. | **Low for now.** Only if GlowPowerRental grows beyond 10 developers. |
| **Event-Driven** | Components communicate by publishing and consuming events. Producers do not know about consumers. | Decoupled processing, async workflows, systems where multiple consumers react to the same event. | Loose coupling, high throughput, easy to add new consumers. | Hard to debug, eventual consistency, event ordering challenges, message broker dependency. | **Medium.** Used for IoT telemetry ingestion and inter-module notifications. |
| **CQRS** | Command Query Responsibility Segregation. Separate models for reading and writing data. | Read-heavy applications, complex reporting alongside transactional operations. | Optimized read and write paths, scalable reads via read replicas, simplified queries. | Increased complexity, eventual consistency between read and write models, more code to maintain. | **Low.** Useful only if reporting requirements grow significantly. |
| **Hexagonal (Ports and Adapters)** | Business logic at the center, surrounded by ports (interfaces) and adapters (implementations). External dependencies are injected. | Applications that need to be testable in isolation, or that integrate with multiple external systems. | Highly testable, external dependencies are swappable, business logic is pure. | More abstractions, can feel over-engineered for simple CRUD. | **Medium.** Useful for services with multiple external integrations (SAP, payment gateway). |
| **Pipe and Filter** | Data flows through a pipeline of processing stages. Each stage transforms the data and passes it to the next. | Data processing pipelines, ETL, telemetry data transformation. | Each stage is simple and testable, easy to add/remove stages, parallelizable. | Not suitable for interactive applications, debugging requires understanding the full pipeline. | **Medium.** Used for IoT telemetry data pipeline (ingest → validate → store → alert). |
| **Client-Server** | Clients (browsers, mobile apps) interact with a centralized server that holds business logic and data. | Web applications, mobile backends, any system with a frontend/backend split. | Centralized data management, consistent business logic, standard web architecture. | Server is a single point of failure, all clients depend on server availability. | **High.** Standard pattern for all GlowPowerRental web applications. |

---

## DECISION TREE

### Which architecture pattern should I use?

```
IF building a standard web application with frontend/backend split
  THEN use Client-Server as the deployment pattern
  AND continue to select an internal architecture pattern below

IF team size < 10 developers
  AND no need for independent service deployment
  THEN use Modular Monolith
    IF application is simple CRUD with few integrations
      THEN combine with Layered pattern internally
    IF application has multiple external integrations (SAP, payment, etc.)
      THEN combine with Hexagonal (Ports and Adapters) internally

IF team size >= 10 developers
  OR independent scaling per service is required
  OR independent deployment cadence per service is required
  THEN use Microservices
    NOTE: Requires mature DevOps pipeline and monitoring

IF system processes streaming data or asynchronous workflows
  THEN use Event-Driven
    IF data flows through sequential transformation stages (ETL, telemetry)
      THEN combine with Pipe and Filter

IF read-to-write ratio is very high (10:1 or more)
  AND reporting queries are complex and distinct from transactional models
  THEN use CQRS
    NOTE: Only justified when reporting requirements are significant
```

### Can I combine patterns?

```
IF primary pattern = Modular Monolith
  THEN internal modules MAY use Layered or Hexagonal
  THEN inter-module communication MAY use Event-Driven for async workflows

IF primary pattern = Microservices
  THEN each service MAY use any internal pattern independently
  THEN inter-service communication SHOULD use Event-Driven or REST APIs

IF data pipeline exists alongside main application
  THEN main application uses its own pattern (e.g., Modular Monolith)
  AND data pipeline uses Pipe and Filter
```

### GlowPowerRental default selection

```
IF new GlowPowerRental project with no special constraints
  THEN use Modular Monolith + Layered + Client-Server
  THEN document rationale in an ADR

IF IoT telemetry processing component
  THEN use Event-Driven + Pipe and Filter

IF service integrating with SAP, payment gateway, or 3+ external systems
  THEN use Hexagonal (Ports and Adapters)
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Architecture Description | Runbook | ../runbooks/create-architecture-description.md |
| Conduct Architecture Review | Runbook | ../runbooks/conduct-architecture-review.md |
| Write Architecture Decision Record | Runbook | ../runbooks/write-architecture-decision-record.md |
