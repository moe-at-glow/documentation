# Design Phase Overview

How the Design phase works at GlowPowerRental.

---

## What Is the Design Phase

Design is Phase 4 of the SDLC. It takes the approved architecture and specifies each component in enough detail that developers can implement it without ambiguity.

**Architecture tells you:** "We have a Billing Service that calculates late fees and generates invoices."

**Design tells you:** "The Billing Service exposes POST /api/v1/invoices, uses the formula daily_rate * 0.02 * days_overdue, stores invoices in the late_fee_invoices table with columns id, rental_id, amount, currency, status, and publishes an invoice.created event."

---

## Difference Between Architecture and Design

| Aspect | Architecture | Design |
|--------|-------------|--------|
| Scope | Entire system | Individual components |
| Level of detail | High-level structure | Implementation-level |
| Audience | All stakeholders | Developers and QA |
| Focus | What components exist and how they relate | How each component works internally |
| Technology | Technology stack choices | Specific libraries, query patterns, algorithms |
| Output | ADD, ADRs, diagrams | DDD, API specs, data models, wireframes |

---

## Design Inputs and Outputs

### Inputs

| Input | From Phase | Used For |
|-------|-----------|---------|
| Architecture Description Document | Phase 3 | Component boundaries, interfaces, technology constraints |
| Architecture Decision Records | Phase 3 | Technology choices, pattern decisions |
| Software Requirements Specification | Phase 2 | Functional behavior, acceptance criteria |
| Requirements Traceability Matrix | Phase 2 | Mapping requirements to design elements |

### Outputs

| Output | Used By | Purpose |
|--------|---------|---------|
| Detailed Design Document | Phase 5 (Development) | Implementation guide for developers |
| API Specifications | Phase 5 (Development), Phase 6 (Testing) | API contract for implementation and testing |
| Data Model | Phase 5 (Development) | Database schema implementation |
| UI Wireframes | Phase 5 (Development) | Frontend implementation guide |
| Updated RTM | Phase 6 (Testing) | Design-to-requirement traceability |

---

## Design Principles (SOLID)

### Single Responsibility Principle

Every module has one, and only one, reason to change.

**GlowPowerRental example:** The LateFeeCalculator calculates fees. It does not send emails about fees (that is the NotificationService's job) and it does not persist fees to the database (that is the InvoiceRepository's job).

### Open/Closed Principle

Software entities should be open for extension but closed for modification.

**GlowPowerRental example:** The fee calculation supports multiple strategies (percentage-based, flat rate, tiered). Adding a new strategy does not require modifying the LateFeeCalculator class -- you add a new strategy class.

### Liskov Substitution Principle

Objects of a superclass should be replaceable with objects of a subclass without breaking the application.

**GlowPowerRental example:** If you have a NotificationSender interface with EmailSender and SmsSender implementations, any code that uses NotificationSender should work correctly regardless of which implementation is provided.

### Interface Segregation Principle

No client should be forced to depend on methods it does not use.

**GlowPowerRental example:** Instead of one large RentalService interface with 20 methods, split it into RentalReader (get, list, search) and RentalWriter (create, update, cancel). Read-only consumers only depend on RentalReader.

### Dependency Inversion Principle

High-level modules should not depend on low-level modules. Both should depend on abstractions.

**GlowPowerRental example:** BillingService depends on a PaymentGateway interface, not directly on the Stripe SDK. To switch to a different payment provider, you implement a new adapter without changing BillingService.

---

## Design in Agile

In Agile execution, design happens incrementally:

| Sprint Activity | Design Work |
|----------------|-------------|
| Backlog refinement | Identify which stories need design work (technical stories) |
| Sprint planning | Include design tasks in sprint capacity |
| Design spike | Time-boxed investigation for uncertain designs (1-2 days) |
| Technical story | Produce DDD/API spec/data model before implementation stories begin |
| Implementation story | Must not start until its design is reviewed and approved |

**Just-enough design:** Design what you need for the current sprint, not the entire system. But complete the design for a component before starting to implement it.
