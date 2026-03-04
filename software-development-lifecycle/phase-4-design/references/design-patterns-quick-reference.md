# Design Patterns Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P4-002 |
| **Use When** | Selecting the appropriate design pattern for a component or problem |
| **Last Updated** | 2026-03-04 |

---

## PATTERN LOOKUP TABLE

| Pattern | Category | Problem It Solves | When to Use |
|---------|----------|------------------|-------------|
| Factory | Creational | Creating objects when exact type depends on runtime conditions | Multiple implementations of an interface, chosen at runtime |
| Builder | Creational | Constructing complex objects with many optional parameters | Objects with 5+ constructor parameters, many optional |
| Singleton | Creational | Ensuring only one instance exists | Database connection pool, configuration manager. Use sparingly. |
| Repository | Structural | Separating business logic from data access | Always for database access. Enables testing without DB. |
| Adapter | Structural | Converting an external interface to match your internal interface | Integrating third-party APIs and SDKs |
| Facade | Structural | Providing a simple interface to a complex subsystem | Complex subsystems that need a simplified entry point |
| Decorator | Structural | Adding behavior to objects without modifying their class | Logging, caching, validation wrappers |
| Strategy | Behavioral | Multiple algorithms for the same task, selectable at runtime | Business rules with multiple calculation methods |
| Observer/Events | Behavioral | Multiple components react to the same event independently | Decoupled event-driven processing |
| State Machine | Behavioral | Entity transitions through defined states with rules | Entities with lifecycle (rental: active -> overdue -> returned) |
| Command | Behavioral | Encapsulating a request as an object for queuing or undo | Job queues, undo/redo, audit logging |
| Middleware/Pipeline | Behavioral | Processing requests through a chain of handlers | HTTP middleware (auth, logging, validation, rate limiting) |

---

## DECISION TREE

### Which design pattern to use?

```
IF you need to CREATE objects
  IF exact type depends on runtime conditions
    THEN use FACTORY
  ELSE IF object has 5+ constructor parameters or many optional fields
    THEN use BUILDER
  ELSE IF only one instance must exist (connection pool, config)
    THEN use SINGLETON (use sparingly)

ELSE IF you need to STRUCTURE components
  IF accessing a database
    THEN use REPOSITORY (always)
  ELSE IF integrating a third-party API or SDK
    THEN use ADAPTER
  ELSE IF exposing a complex subsystem through a simple interface
    THEN use FACADE
  ELSE IF adding cross-cutting behavior (logging, caching, validation)
    THEN use DECORATOR

ELSE IF you need to define BEHAVIOR
  IF multiple algorithms/calculations selectable at runtime
    THEN use STRATEGY
  ELSE IF multiple components must react to the same event independently
    THEN use OBSERVER/EVENTS
  ELSE IF entity transitions through defined states with rules
    THEN use STATE MACHINE
  ELSE IF requests need queuing, undo, or audit trail
    THEN use COMMAND
  ELSE IF processing through a chain of handlers (auth, logging, validation)
    THEN use MIDDLEWARE/PIPELINE
```

### Can I combine patterns?

```
IF component has database access
  THEN use REPOSITORY
  AND IF multiple DB implementations exist
    THEN combine with FACTORY to select repository at runtime

IF component has complex business rules
  THEN use STRATEGY for rule selection
  AND IF rules change based on entity state
    THEN combine with STATE MACHINE

IF component processes HTTP requests
  THEN use MIDDLEWARE/PIPELINE for cross-cutting concerns
  AND use REPOSITORY for data access
  AND use FACTORY for service resolution
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Detailed Design | Runbook | ../runbooks/create-detailed-design.md |
| Design API Contracts | Runbook | ../runbooks/design-api-contracts.md |
| Design Data Models | Runbook | ../runbooks/design-data-models.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
