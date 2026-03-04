# Common Design Pitfalls -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P4-003 |
| **Use When** | Reviewing a design for common mistakes before approval |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] No over-abstraction: max three layers (Controller -> Service -> Repository) unless requirement demands more
- [ ] No premature optimization: caching/replicas added only when measured performance misses NFR targets
- [ ] All error cases documented: every endpoint has error responses, not just 200
- [ ] No N+1 queries: list operations use JOINs or batch queries, not per-item fetches
- [ ] All list endpoints support pagination by default
- [ ] External APIs accessed through Adapter pattern, not direct SDK calls in business logic
- [ ] Write operations are idempotent: POST endpoints for financial records require Idempotency-Key header
- [ ] Input validation rules defined in API spec: min/max, regex, required fields, allowed values
- [ ] Concurrency handled: optimistic locking (version column) on entities with concurrent edits
- [ ] Code organized by domain module (rental/, billing/, equipment/) not by framework convention (routes/, models/)

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Request traces through 4+ layers to reach DB | Reduce to 3 layers: Controller -> Service -> Repository | Adding layers without concrete requirement |
| Tempted to add caching/read replicas before testing | Design for correctness first; optimize after profiling | Pre-emptive performance infrastructure |
| API spec shows only 200 responses | List all error scenarios; define error response for each | Leaving error handling to implementer discretion |
| List endpoint fetches related data per item | Use JOINs or batch queries | Per-item SELECT in a loop (N+1) |
| List endpoint returns unbounded results | Add pagination (limit/offset or cursor) | Returning all records in single response |
| Business logic calls external SDK directly | Wrap in Adapter behind an interface | Scattering SDK calls across business logic files |
| POST endpoint creates financial records | Require Idempotency-Key header; dedup before creating | Creating duplicate records on retry/double-click |
| Request fields lack validation rules | Define min/max, regex, required, allowed values in spec | Leaving validation to implementer interpretation |
| Multiple users can edit same entity simultaneously | Add version column; return 409 on version mismatch | Last-write-wins silently overwriting changes |
| Code structured by technical concern (routes/, models/) | Organize by domain module (billing/, rental/) | Framework-mirrored folder structure hiding business logic |

---

## QUICK-REFERENCE TABLE

| # | Pitfall | Symptom | Fix |
|---|---------|---------|-----|
| 1 | Over-Abstraction | 7+ files to trace a simple GET | 3 layers max: Controller -> Service -> Repository |
| 2 | Premature Optimization | Redis/replicas before any load test | Profile first, optimize second |
| 3 | Ignoring Error Cases | Only 200 in API spec | Document all error responses per endpoint |
| 4 | N+1 Query | 1 + N queries for a list page | Use JOINs or batch queries |
| 5 | Missing Pagination | Single response returns all records | Default pagination on all list endpoints |
| 6 | Tight Coupling to External APIs | SDK calls spread across business logic | Adapter pattern behind interface |
| 7 | No Idempotency | Duplicate records on retry | Idempotency-Key header for financial POSTs |
| 8 | Missing Input Validation | Inconsistent validation across developers | Define rules in API spec |
| 9 | Ignoring Concurrency | Last-write-wins, lost updates | Optimistic locking with version column |
| 10 | Framework-Driven Structure | Business logic scattered by tech concern | Organize by domain module |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/design-phase-overview.md] |
| Error handling details | Runbook | [../runbooks/create-detailed-design.md] |
| Pagination standard | Standard | [../standards/api-design-standard.md] |
