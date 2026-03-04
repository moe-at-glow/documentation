# Design Patterns Guide -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P4-001 |
| **Use When** | Selecting a design pattern for a component |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Confirmed a recurring problem exists that the pattern solves
- [ ] Verified the pattern simplifies the code, not complicates it
- [ ] Confirmed the team understands the chosen pattern
- [ ] Ruled out a simpler approach that works just as well
- [ ] Avoided premature abstraction (no interface until a second implementation exists)
- [ ] Checked for God Object anti-pattern (class exceeding single responsibility)
- [ ] Checked for Anemic Domain Model (logic belongs in entities, not only in services)

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Multiple implementations of an interface chosen at runtime | Factory pattern | Using Factory when only one implementation exists |
| Object with many optional parameters (10+) | Builder pattern | Using Builder for simple objects with 2-3 required fields |
| Component accesses a database | Repository pattern | Skipping Repository (exception: one-off scripts/migrations) |
| Integrating with external API or third-party library | Adapter pattern | Using Adapter for internal code you control |
| Complex subsystem needs simplified API for external consumers | Facade pattern | Using Facade on already-simple subsystems |
| Multiple algorithms for the same operation, selectable at runtime | Strategy pattern | Using Strategy when only one algorithm exists |
| Multiple components react to an event without source knowing consumers | Observer / Event Emitter | Using Observer when only one consumer exists (use direct call) |
| Entity transitions through defined states with transition rules | State Machine pattern | Using State Machine for simple boolean flags |

---

## QUICK-REFERENCE TABLE

### Creational Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Factory | Runtime type selection | `NotificationFactory.createSender("email")` --> EmailSender |
| Builder | Complex object, many optional params | `InvoiceBuilder.forRental("ra-042").withLateFee(6.00).build()` |

### Structural Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Repository | Any database access | `RentalService` -> `RentalRepository` (interface) -> `PostgresRentalRepository` |
| Adapter | External system integration | `BillingService` -> `PaymentGateway` (interface) -> `StripeAdapter` |
| Facade | Simplifying complex subsystem | `RentalFacade` hides Rental + Equipment + Customer coordination |

### Behavioral Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Strategy | Multiple algorithms, same operation | `LateFeeCalculator` -> `FeeStrategy`: Percentage, FlatRate, Tiered |
| Observer | Decoupled event reactions | `rental.overdue` -> Billing, Notification, Reporting services |
| State Machine | Entity lifecycle with transition rules | Rental: active -> returned / overdue / cancelled |

### Rental Agreement State Transitions

| From | To | Trigger |
|------|----|---------|
| active | returned | Equipment returned on time |
| active | overdue | Daily check finds past due date |
| active | cancelled | Customer or admin cancels |
| overdue | returned | Equipment returned late |

**Blocked transitions:** returned -> active, cancelled -> active.

### Anti-Patterns

| Anti-Pattern | Symptom | Fix |
|-------------|---------|-----|
| God Object | 2000+ lines, 50+ methods | Split by responsibility (SRP) |
| Anemic Domain Model | Entities with only getters/setters | Move business logic into entity methods |
| Spaghetti Code | No clear call structure | Refactor into layers: controller -> service -> repository |
| Golden Hammer | One pattern used for everything | Choose the right tool per problem |
| Premature Abstraction | Interfaces before second implementation | Abstract after the third instance |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/design-phase-overview.md] |
