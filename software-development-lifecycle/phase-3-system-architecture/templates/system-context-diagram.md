# System Context Diagram Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-004 |
| **When to Use** | Defining the system boundary and all external actors/systems that interact with it |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect, Product Owner |
| **SLA** | 2 business days |
| **Runbook** | [Create Architecture Description](../runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Example section optional; minimum 1 user role and 1 external system required
> **IF** medium project (3-5 devs) **THEN** All sections required; Example section optional
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Template

```
                                +------------------+
                                | [External        |
                                |  System 1]       |
                                +--------+---------+
                                         |
                                    [Protocol]
                                    ([data desc])
                                         |
+----------------+              +--------v---------+              +----------------+
| [User Role 1]  | [Protocol]  |                  | [Protocol]   | [External      |
| ([desc])       +------------>+                  +------------->+ System 2]      |
|                |  ([data])   |                  |  ([data])    |                |
+----------------+              |   [YOUR SYSTEM]  |              +----------------+
                                |   [System Name]  |
+----------------+              |                  |              +----------------+
| [User Role 2]  | [Protocol]  |                  | [Protocol]   | [External      |
| ([desc])       +------------>+                  +------------->+ System 3]      |
|                |  ([data])   |                  |  ([data])    |                |
+----------------+              +--------+---------+              +----------------+
                                         |
                                    [Protocol]
                                    ([data desc])
                                         |
                                +--------v---------+
                                | [External        |
                                |  Entity 4]       |
                                +------------------+
```

---

## [ ] GlowPowerRental Example

```
                                +------------------+
                                |  SAP Business    |
                                |  One (ERP)       |
                                +--------+---------+
                                         |
                                    REST API
                                    (customers,
                                     invoices)
                                         |
+----------------+              +--------v---------+              +----------------+
| Rental Desk    | HTTPS        |                  | HTTPS        | Payment        |
| Staff          +------------->+  GlowPowerRental +------------->+ Gateway        |
| (Web Portal)   | (UI, forms)  |  Rental Mgmt     | (charges)    | (Stripe)       |
+----------------+              |  System           |              +----------------+
                                |                  |
+----------------+              |                  |              +----------------+
| Customers      | HTTPS        |                  | SMTP         | Email Provider |
| (Self-Service) +------------->+                  +------------->+ (SendGrid)     |
+----------------+ (bookings)   |                  | (notifs)     +----------------+
                                |                  |
+----------------+              |                  |              +----------------+
| Management     | HTTPS        |                  | SMS API      | SMS Provider   |
| (Dashboards,   +------------->+                  +------------->+ (Twilio)       |
|  Reports)      | (analytics)  +------+-+---------+ (alerts)     +----------------+
+----------------+                     | |
                                  MQTT | | HTTPS
                                       | |
                        +--------------+ +----------+
                        |                           |
               +--------v------+           +--------v------+
               | IoT Sensors   |           | GPS Tracking  |
               | (Equipment-   |           | Service       |
               |  mounted)     |           | (Fleet)       |
               +---------------+           +---------------+
```

---

## [ ] Validation Checklist

- [ ] System is shown as a single box (no internal details).
- [ ] Every external system from the SRS interface requirements appears.
- [ ] Every user role from the SRS appears.
- [ ] Every line has a protocol label.
- [ ] Every line has a data description.
- [ ] Every line has directional arrows (-->, <--, or <-->).
- [ ] No internal components are shown.

---

## COMPLETION CHECKLIST

- [ ] System boundary drawn as a single box with system name
- [ ] All user roles from SRS identified and placed
- [ ] All external systems from SRS interface requirements placed
- [ ] Every connection labeled with protocol
- [ ] Every connection labeled with data description
- [ ] Every connection has direction arrows
- [ ] Validation Checklist items all pass
- [ ] Diagram reviewed by System Architect and Product Owner

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description-document.md](architecture-description-document.md) | Context diagram feeds into ADD Section 4 |
| Component Diagram | [component-diagram.md](component-diagram.md) | Context diagram defines boundaries; component diagram details internals |
| Architecture Decision Records | [architecture-decision-record.md](architecture-decision-record.md) | ADRs may affect external integration choices |
| Software Requirements Specification | Phase 2 SRS | Interface requirements define external entities |
| Runbook | [Create Architecture Description](../runbooks/create-architecture-description.md) | Step-by-step procedure |
