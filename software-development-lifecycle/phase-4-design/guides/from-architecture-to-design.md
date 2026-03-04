# From Architecture to Design -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P4-002 |
| **Use When** | Transforming architecture artifacts into detailed component design |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Architecture Description Document (ADD) is approved and available
- [ ] Architecture Decision Records (ADRs) reviewed for technology choices
- [ ] Component boundaries and responsibilities identified from ADD
- [ ] Owned data entities identified for the component
- [ ] Exposed interfaces (REST, events) identified from ADD
- [ ] Consumed interfaces/events identified from ADD
- [ ] NFR targets (response time, throughput) noted for the component

---

## SELECTION CRITERIA / DECISION TABLE

| Architecture Artifact | Design Output | Action |
|----------------------|---------------|--------|
| Component with responsibility description | Internal module structure | Define files: controller, service, repository, entity, DTOs, events, tests |
| Interface marked "REST API" | API contract | Specify method, endpoint, request/response schemas for each operation |
| Owned data entity | Data model (DDL) | Define table, columns, types, constraints, indexes |
| NFR performance target | Caching/indexing strategy | Add Redis cache or DB indexes only where NFR demands it |
| Consumed event | Event handler | Define event payload extraction, deduplication check, processing steps |
| Published event | Event emission | Define event name, payload schema, trigger point in business logic |

---

## QUICK-REFERENCE TABLE

### Architecture-to-Design Mapping

| Architecture Says | Design Produces |
|-------------------|----------------|
| Component: Billing Service | Module: `src/modules/billing/` with controller, service, repository, entity, DTOs, events, tests |
| Responsibility: Calculate fees, generate invoices | Methods: `calculateLateFee(rentalId)`, `generateInvoice(rentalId)`, `getInvoice(invoiceId)` |
| Interface: REST API | `POST /api/v1/invoices`, `GET /api/v1/invoices/:id`, `GET /api/v1/invoices` |
| Owned data: invoices | Table `late_fee_invoices`: id, rental_id, amount, currency, status + indexes |
| NFR: Response < 200ms | Redis cache for frequent queries, index `idx_invoices_rental_id` |
| Publishes: invoice.created | Event payload: `{ invoice_id, rental_id, amount }` |
| Consumes: rental.overdue | Handler: extract rental_id, dedup check, calculate fee, generate invoice, publish event |

### API Contract Template

| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | /api/v1/invoices | Generate invoice for a rental |
| GET | /api/v1/invoices/:id | Get invoice by ID |
| GET | /api/v1/invoices | List invoices (paginated, filterable) |

### Business Logic Specification Template

```
calculateLateFee(rentalId):
  1. Fetch rental from Rental Service API
  2. Validate: rental.status must be 'overdue'
  3. Calculate: amount = rental.daily_rate * 0.02 * rental.days_overdue
  4. Round to 2 decimal places (banker's rounding)
  5. Return { amount, currency: 'SAR', days_overdue, daily_rate }
```

### Event Handling Template

```
On receiving: rental.overdue
  1. Extract rental_id from event payload
  2. Check if invoice already exists for this rental today
  3. If not: call calculateLateFee(rental_id)
  4. Call generateInvoice(rental_id, feeResult)
  5. Publish: invoice.created { invoice_id, rental_id, amount }
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/design-phase-overview.md] |
