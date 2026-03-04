# Component Diagram Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-003 |
| **When to Use** | Documenting the internal structure, responsibilities, and interactions of system components |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect |
| **SLA** | 3 business days |
| **Runbook** | [Create Architecture Description](../runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Example section optional; Component Description Table required with minimum 2 components
> **IF** medium project (3-5 devs) **THEN** All sections required; Example section optional
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Template

```
+------------------------------------------------------------------+
|                      [API Gateway / Entry Point]                   |
|  [Responsibilities: routing, auth, rate limiting]                  |
+-----+--------+--------+---------+--------+--------+---------+-----+
      |        |        |         |        |        |         |
      v        v        v         v        v        v         v
+--------+ +--------+ +--------+ +------+ +------+ +-------+ +--------+
|[Comp A]| |[Comp B]| |[Comp C]| |[Comp]| |[Comp]| |[Comp] | |[Comp H]|
|        | |        | |        | |  D   | |  E   | |  F    | |        |
|Respons:| |Respons:| |Respons:| |Resp: | |Resp: | |Resp:  | |Respons:|
|[1 line]| |[1 line]| |[1 line]| |[...]| |[...]| |[...]  | |[1 line]|
|        | |        | |        | |      | |      | |       | |        |
|Owns:   | |Owns:   | |Owns:   | |Owns: | |Owns: | |Owns:  | |Owns:   |
|[data]  | |[data]  | |[data]  | |[data]| |[data]| |[data] | |[data]  |
+---+----+ +---+----+ +--------+ +--+---+ +--+---+ +--+----+ +--------+
    |          |                     |        |        |
    +--[type]->+                     |        |        |
    |  [desc]  |                     |        |        |
    +--[Event: xxx]----------------->+        |        |
    |                                +[Event]-+------->+
```

---

## [ ] Component Description Table

| Component | Responsibility | Owned Data | Exposed Interface | Dependencies |
|-----------|---------------|------------|------------------|-------------|
| [Name] | [One sentence: what this component does] | [Database tables/collections it owns] | [REST endpoints or events published] | [Other components it calls] |

---

## [ ] GlowPowerRental Example

```
+-------------------------------------------------------------------+
|                     Nginx (API Gateway)                            |
|  Routing, TLS, JWT validation, rate limiting                       |
+-----+--------+--------+---------+---------+--------+--------+-----+
      |        |        |         |         |        |        |
      v        v        v         v         v        v        v
+--------+ +--------+ +--------+ +-------+ +------+ +------+ +--------+
| Rental | | Equip  | | Cust   | |Billing| |Report| |Notif | |Teleme- |
| Svc    | | Svc    | | Svc    | |Svc    | |Svc   | |Svc   | |try Svc |
|        | |        | |        | |       | |      | |      | |        |
|Manage  | |Track   | |Manage  | |Calc   | |Build | |Send  | |Ingest  |
|rental  | |equip   | |customer| |fees,  | |report| |email,| |sensor  |
|lifecycl| |status, | |accts,  | |gen    | |s and | |SMS,  | |data,   |
|e       | |mainten | |auth    | |invoic | |dashbd| |push  | |alerts  |
|        | |ance    | |        | |es     | |      | |      | |        |
|Owns:   | |Owns:   | |Owns:   | |Owns:  | |Owns: | |Owns: | |Owns:   |
|rentals | |equip   | |custom  | |invoic | |report| |templ | |sensor  |
|line_itm| |maintnc | |users   | |paymt  | |cache | |logs  | |reading |
+---+----+ +---+----+ +---+----+ +--+----+ +------+ +--+---+ +---+----+
    |          |          |         ^                    ^         |
    |          |          |         |                    |         |
    +--REST--->+ check    |         |                    |         |
    |  availability       |         |                    |         |
    +-----REST----------->+ get     |                    |         |
    |     customer info   |         |                    |         |
    |                               |                    |         |
    +--Event: rental.overdue------->+                    |         |
    +--Event: rental.returned------>+                    |         |
    |                               |                    |         |
    |                               +--Event: invoice.-->+         |
    |                               |  created           |         |
    |                                                              |
    +<---Event: equipment.alert---<----------------------------<---+
```

---

## [ ] Validation Checklist

- [ ] Every component has a single, clear responsibility.
- [ ] Every component lists its owned data.
- [ ] No two components own the same data.
- [ ] All interactions are labeled with type (REST, Event, etc.).
- [ ] Every functional requirement traces to at least one component.
- [ ] No circular dependencies exist.
- [ ] API Gateway/entry point is shown.

---

## COMPLETION CHECKLIST

- [ ] Diagram drawn with all components identified
- [ ] Each component box shows responsibility and owned data
- [ ] All interactions labeled with type and description
- [ ] Component Description Table filled in for every component
- [ ] API Gateway / entry point included
- [ ] Validation Checklist items all pass
- [ ] Diagram reviewed by System Architect

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description-document.md](architecture-description-document.md) | Component diagram feeds into ADD Section 5 |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Context diagram defines external boundaries; component diagram shows internals |
| Architecture Decision Records | [architecture-decision-record.md](architecture-decision-record.md) | ADRs may drive component boundaries and technology choices |
| Software Requirements Specification | Phase 2 SRS | Functional requirements trace to components |
| Runbook | [Create Architecture Description](../runbooks/create-architecture-description.md) | Step-by-step procedure |
