# Architecture Viewpoints -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P3-001 |
| **Use When** | Selecting or creating architecture views for stakeholder communication |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Verified each viewpoint has a clearly identified primary audience
- [ ] System context diagram shows system as a single black box (no internal components exposed)
- [ ] All external systems from the SRS are represented in the system context view
- [ ] Every line/arrow in diagrams is labeled with protocol and data flow direction
- [ ] Logical view assigns data ownership to exactly one component per entity
- [ ] No circular dependencies exist between components
- [ ] No component directly accesses another component's database

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Presenting to all stakeholders / project kickoff | Start with System Context viewpoint | Showing internal component details |
| Defining internal structure and responsibilities | Use Logical/Functional viewpoint | Leaving data ownership unlabeled |
| Documenting runtime behavior and async flows | Use Process/Runtime viewpoint | Showing only the happy path |
| Planning infrastructure and deployment | Use Deployment viewpoint | Omitting specs (CPU/RAM) and network topology |
| Onboarding developers to the codebase | Use Development viewpoint | Skipping build pipeline documentation |
| New external integration added | Update System Context view | Showing individual API endpoints in context diagram |
| New component or changed responsibility | Update Logical view | Assigning multiple unrelated responsibilities to one component |
| Communication pattern changed (sync to async) | Update Process/Runtime view | Leaving stale sequence diagrams |
| Infrastructure change (new server, resize) | Update Deployment view | Forgetting to update network topology |
| New module or repo structure change | Update Development view | Omitting module boundary definitions |

---

## QUICK-REFERENCE TABLE

| Viewpoint | Question It Answers | Primary Audience | Key Elements |
|-----------|-------------------|-----------------|--------------|
| System Context | What interacts with our system? | Product Owner, BA, all stakeholders | System as black box, external actors, external systems, data flows with protocols |
| Logical/Functional | What are the components and how do they relate? | Tech Lead, Developers, QA Lead | Internal components, responsibilities, data ownership, interfaces, dependencies |
| Process/Runtime | How does the system behave at runtime? | Tech Lead, Developers, QA Lead | Sequence flows, sync vs async, message queues, scheduled jobs, error/retry behavior |
| Deployment | Where does the system run? | Infra Engineer, Ops Lead, Tech Lead | Servers/containers with specs, network topology, DB instances, load balancers, backups |
| Development | How is the codebase organized? | Developers, Tech Lead | Repo structure, module boundaries, build pipeline stages, dev tooling |

### Common Mistakes by Viewpoint

| Viewpoint | Mistake | Fix |
|-----------|---------|-----|
| System Context | Showing internal components | Keep it black-box; internals belong in Logical view |
| System Context | Missing external system from SRS | Cross-check every interface requirement |
| System Context | Unlabeled protocols/directions | Every line needs label and directional arrows |
| System Context | Too much detail (API endpoints) | Show integration, not endpoints |
| Logical | Multiple unrelated responsibilities per component | Apply single responsibility; split the component |
| Logical | Circular dependencies (A calls B, B calls A) | Introduce events or extract shared logic |
| Logical | Missing data ownership labels | Every entity owned by exactly one component |
| Logical | Direct cross-component DB access | Always go through owning component's interface |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background on architecture description and ISO 42010 | Training | [training/architecture-description-overview.md] |
