# Common Architecture Pitfalls -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P3-003 |
| **Use When** | Reviewing architecture decisions before approval or during architecture retrospectives |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Architecture complexity matches team size and project scale
- [ ] Component boundaries, data ownership, and interface contracts are explicitly defined
- [ ] All NFR categories addressed in architecture (performance, security, reliability, scalability, maintainability, compliance)
- [ ] No unnecessary abstraction layers -- every layer justified by a current requirement
- [ ] Components communicate only through defined interfaces (APIs or events), not shared DB tables
- [ ] System boundary is clearly defined (what is IN vs OUT of scope)
- [ ] Vendor dependencies documented as ADRs with explicit trade-off acknowledgment
- [ ] Failure modes documented for every external dependency and inter-component interaction
- [ ] Scaling strategy documented (even if not yet implemented)
- [ ] Every significant technology/pattern choice recorded as an ADR

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Small team (1-5 devs), simple domain | Use monolith or modular monolith | Microservices, Kubernetes, service mesh |
| Choosing between abstraction layers | Justify each layer with a current requirement | Building for hypothetical future needs ("what if we switch DBs?") |
| Component needs data from another component | Call the owning component's API or subscribe to its events | Directly querying another component's database tables |
| Defining system scope | Draw system context diagram with clear boundary | Letting scope grow unbounded ("the system does everything") |
| Using vendor-specific services | Write ADR documenting lock-in trade-off | Using proprietary services without acknowledging portability risk |
| Designing integrations and inter-component flows | Document failure mode, detection, retry, fallback for each | Showing only the happy path |
| Current capacity is sufficient | Document scaling strategy for future; do not implement yet | "We will figure it out later" with no documented plan |
| Making technology or pattern decisions | Write an ADR (30 min) with rationale and alternatives considered | Deciding in hallway conversations with no written record |

---

## QUICK-REFERENCE TABLE

| Pitfall | Warning Sign | Resolution |
|---------|-------------|------------|
| Over-engineering | Team size vs. architecture complexity mismatch (e.g., 3 devs managing 8 microservices) | Match architecture to project scale; start with modular monolith |
| Under-engineering | Developers cannot draw the system on a whiteboard; no component boundaries | Define component boundaries, data ownership, interface contracts (2-3 hours) |
| Ignoring NFRs | No mention of performance, security, or reliability in architecture | Address every NFR category before development begins |
| Architecture astronaut | More abstraction layers than domain concepts; 4+ layers between request and DB | Every abstraction layer must justify itself with a current requirement |
| Tight coupling | Schema changes break multiple services; components share DB tables | Components communicate only through APIs or events; DB is internal |
| No system boundaries | No system context diagram or diagram has no boundary line | Define IN vs OUT of scope in system context diagram |
| Vendor lock-in | Vendor-specific services used without ADR | Document vendor dependencies and trade-offs in ADRs |
| Missing failure analysis | Architecture only shows the happy path | Document: what fails, detection, retry strategy, fallback, alerting |
| No scalability plan | "We will deal with scaling when we need it" | Document scaling strategy even if not implementing yet |
| Skipping ADRs | "Why did we choose X?" has no documented answer | Write ADR for every significant technology/pattern choice |

### Architecture Review Checklist

| # | Check | Pass Criteria |
|---|-------|--------------|
| 1 | Team size vs. complexity | Architecture style appropriate for team size |
| 2 | Documentation exists | System context + component diagram at minimum |
| 3 | NFRs addressed | Each NFR category has an architectural approach |
| 4 | Abstraction justified | No layer exists without a current requirement |
| 5 | Coupling managed | No shared DB access across components |
| 6 | Scope bounded | System context diagram has clear boundary |
| 7 | Vendor risk documented | ADR for each vendor-specific dependency |
| 8 | Failure modes covered | Failure handling for each external dependency |
| 9 | Scaling planned | Documented strategy even if deferred |
| 10 | Decisions recorded | ADR for each significant decision |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background on architecture description and ISO 42010 | Training | [training/architecture-description-overview.md] |
