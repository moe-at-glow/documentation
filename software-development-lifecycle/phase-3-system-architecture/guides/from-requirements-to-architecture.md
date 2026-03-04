# From Requirements to Architecture -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P3-002 |
| **Use When** | Mapping baselined Phase 2 requirements to architecture decisions and components |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Phase 2 requirements are baselined before starting architecture
- [ ] All NFR categories reviewed (performance, security, scalability, reliability, maintainability, compliance)
- [ ] Architecture-Significant Requirements (ASRs) explicitly identified and separated from non-ASRs
- [ ] Every ASR has a corresponding ADR documenting the decision
- [ ] RTM updated with architecture component and ADR references
- [ ] No architecture decisions based on hypothetical future requirements

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Requirement drives technology choice (e.g., 500 IoT sensors) | Identify as ASR; write ADR for technology selection | Choosing technology without tracing to a requirement |
| Requirement defines scalability/performance threshold | Identify as ASR; define caching, indexing, pooling approach | Deferring performance architecture to production |
| Requirement mandates external integration | Identify as ASR; define adapter component and sync/async pattern | Skipping error handling and retry strategy for integrations |
| Requirement specifies security controls | Identify as ASR; define auth middleware and token strategy | Bolting on authentication after all APIs are built |
| Requirement specifies data retention | Identify as ASR; define partitioning and archival approach | Ignoring storage growth and retention in architecture |
| Grouping functional requirements | Cluster related SWRs to identify service/component boundaries | Creating one component per requirement |
| Architecture is defined | Update RTM with component mapping and ADR references | Leaving RTM without architecture traceability |

---

## QUICK-REFERENCE TABLE

### Requirement-to-Architecture Transformation

| Phase 2 Output | Phase 3 Transformation | Output |
|----------------|----------------------|--------|
| Functional Requirements (SWR-xxx) | Component identification | Service/module boundaries |
| Non-Functional Requirements (Performance, Security) | Quality attribute approaches | Caching, auth, failover strategies |
| Interface Requirements (External systems) | Integration architecture | Protocols, adapters, error handling |
| Data Requirements (Storage, retention) | Data architecture | DB selection, partitioning, archival |

### ASR Identification Indicators

| Indicator | Example | Action |
|-----------|---------|--------|
| Drives technology choice | "500 concurrent IoT sensors" | Select protocol/broker; write ADR |
| Defines scalability target | "200 concurrent users" | Determine server topology; write ADR |
| Specifies performance threshold | "API < 200ms at p95" | Define caching/indexing strategy; write ADR |
| Requires external integration | "Sync with SAP B1" | Define adapter + sync pattern; write ADR |
| Mandates security control | "JWT on all endpoints" | Define auth middleware; write ADR |
| Specifies data retention | "7-year rental records" | Define partitioning/archival; write ADR |
| Defines availability target | "99.5% monthly" | Define redundancy/recovery; write ADR |

### NFR-to-Architecture Mapping

| NFR Category | Architecture Approach |
|-------------|----------------------|
| Performance: API < 200ms | DB query optimization, Redis caching, connection pooling |
| Performance: Dashboard < 3s | SSR for initial load, background aggregation jobs |
| Security: JWT auth | Auth middleware at API gateway, token validation before routing |
| Security: RBAC | Permission matrix in middleware, roles in JWT claims |
| Security: Encryption at rest | Encrypted storage, .env with 640 permissions |
| Scalability: 200 concurrent | Connection pooling (pgBouncer), Node.js async I/O |
| Scalability: 500+ concurrent | Read replica for reporting, separate worker process |
| Reliability: 99.5% uptime | systemd auto-restart, health checks, monitoring alerts |
| Reliability: No financial data loss | WAL replication, daily backups to object storage |
| Reliability: Graceful degradation | Circuit breaker for external calls, async queue fallback |

### Functional Requirements to Components

| SWR Range | Component |
|-----------|-----------|
| SWR-001 to SWR-015 | Rental Service |
| SWR-016 to SWR-025 | Equipment Service |
| SWR-026 to SWR-035 | Customer Service |
| SWR-201 to SWR-210 | Billing Service |
| SWR-207 to SWR-208 | Notification Service |
| SWR-301 to SWR-310 | Telemetry Service |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background on architecture description and ISO 42010 | Training | [training/architecture-description-overview.md] |
