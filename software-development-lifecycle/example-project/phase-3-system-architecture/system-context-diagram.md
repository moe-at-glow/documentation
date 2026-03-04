> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# System Context Diagram -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-004 |
| **When to Use** | Defining the system boundary and all external actors/systems that interact with it |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect, Product Owner |
| **SLA** | 2 business days |
| **Runbook** | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **Applied:** Small project (1-2 devs) -- Example section not applicable (this is the example). All sections completed.

---

## [x] System Context Diagram

```
                                +------------------+
                                |  Email SMTP      |
                                |  Service         |
                                |  (e.g., Gmail    |
                                |   SMTP relay)    |
                                +--------+---------+
                                         ^
                                         |
                                    SMTP (port 587)
                                    (password resets,
                                     requirement status
                                     notifications,
                                     project alerts)
                                         |
+----------------+              +--------+---------+              +------------------+
| Power          | HTTPS (443)  |                  |              | Future:          |
| Engineers      +------------->+                  + - - - - - -> | Moyasar          |
| (Web Browser)  |              |                  |   HTTPS      | Payment Gateway  |
|                | (create      |                  |   (payment   | (online payment  |
| - Create       |  projects,   |                  |    charges,  |  for client      |
|   projects     |  loads,      |   POWER ATLAS    |    refunds)  |  invoices)       |
| - Assign       |  generators, |                  |              +------------------+
|   generators   |  layouts,    |   GlowPower      |
| - Calculate    |  calcs,      |   Rental          |
|   power        |  PDF reports)|                  |
| - Generate     |              |                  |              +------------------+
|   PDF reports  |              |                  |              | Future:          |
| - Review       |              |                  + - - - - - -> | ZATCA            |
|   requirements |              |                  |   HTTPS      | E-Invoicing      |
+----------------+              |                  |   (tax       | (Saudi tax       |
                                |                  |    invoices, |  authority        |
+----------------+              |                  |    compliance|  integration)     |
| Admin Users    | HTTPS (443)  |                  |    reports)  +------------------+
| (Web Browser)  +------------->+                  |
|                |              |                  |
| - Manage users | (user CRUD,  |                  |
| - System       |  settings,   |                  |
|   settings     |  audit logs, |                  |
| - View reports |  analytics)  |                  |
| - Audit logs   |              |                  |
+----------------+              +--------+---------+
                                         |
+----------------+                       |
| Client Users   | HTTPS (443)           |
| (Web Browser)  +------------->+--------+---------+
|                |              |                  |
| - Submit power | (requirement |                  |
|   requirements |  forms,      |                  |
| - Track status |  status      |                  |
| - View         |  tracking,   |                  |
|   notifications|  notifs)     +------------------+
+----------------+                       |
                                         |
                                    MQTT (port 1883)
                                    (future: generator
                                     telemetry -- fuel,
                                     runtime, load %,
                                     GPS coordinates)
                                         |
                                +--------v---------+
                                | Future:          |
                                | IoT Sensors      |
                                | (generator-      |
                                |  mounted units)  |
                                +------------------+
```

---

## [x] External Entities Table

| Entity | Type | Protocol | Port | Data Exchanged | Direction |
|--------|------|----------|------|---------------|-----------|
| Power Engineers | Human (Web Browser) | HTTPS | 443 | Projects, loads, generators, folders, power calculations, site layouts, PDF reports | Both |
| Admin Users | Human (Web Browser) | HTTPS | 443 | User accounts (CRUD), system settings, audit/activity logs, analytics dashboards | Both |
| Client Users | Human (Web Browser) | HTTPS | 443 | Power requirement submissions, requirement status updates, notifications | Both |
| Email SMTP Service | External System | SMTP | 587 (STARTTLS) | Password reset emails, requirement status change notifications, project alert emails | Outbound |
| Moyasar Payment Gateway (future) | External System | HTTPS REST | 443 | Payment charges for client invoices, payment status callbacks, refund requests | Both |
| ZATCA E-Invoicing (future) | External System | HTTPS REST | 443 | Tax-compliant electronic invoices, compliance validation responses | Outbound |
| IoT Sensors (future) | External System | MQTT | 1883 | Generator telemetry: fuel level %, runtime hours, current load %, GPS coordinates, alert thresholds | Inbound |

---

## [x] System Boundary Notes

The **Power Atlas** system boundary encompasses:

- **Nginx** reverse proxy (TLS termination, static file serving, rate limiting)
- **Flask API server** (all backend business logic, authentication, REST endpoints)
- **PDF Server** (ReportLab-based document generation service)
- **SQLite database** (all persistent data)
- **Frontend assets** (HTML pages, JavaScript bundles, CSS, images)
- **Layout Builder** (React/Konva.js sub-application served as static files)

Everything inside the system boundary runs on a **single DigitalOcean droplet**. External entities communicate with the system exclusively through the Nginx entry point on ports 80/443 (HTTPS). The SMTP connection is outbound-only from the Flask server. Future MQTT connections will be inbound to the Mosquitto broker on port 1883.

---

## [x] Validation Checklist

- [x] System is shown as a single box (no internal details).
- [x] Every external system from the SRS interface requirements appears (Email SMTP, Moyasar, ZATCA, IoT).
- [x] Every user role from the SRS appears (Engineer, Admin, Client).
- [x] Every line has a protocol label (HTTPS, SMTP, MQTT).
- [x] Every line has a data description (projects, notifications, telemetry, etc.).
- [x] Every line has directional arrows (-->, or dashed for future).
- [x] No internal components are shown in the context diagram.

---

## COMPLETION CHECKLIST

- [x] System boundary drawn as a single box with system name
- [x] All user roles from SRS identified and placed (Engineer, Admin, Client)
- [x] All external systems from SRS interface requirements placed (Email, Moyasar, ZATCA, IoT)
- [x] Every connection labeled with protocol
- [x] Every connection labeled with data description
- [x] Every connection has direction arrows
- [x] Future integrations clearly marked with dashed lines and "Future:" label
- [x] Validation Checklist items all pass
- [x] Diagram reviewed by System Architect and Product Owner

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description.md](architecture-description.md) | Context diagram feeds into ADD Section 4 |
| Component Diagram | [component-diagram.md](component-diagram.md) | Context diagram defines boundaries; component diagram details internals |
| Architecture Decision Records | [architecture-decision-records.md](architecture-decision-records.md) | ADRs may affect external integration choices |
| Software Requirements Specification | Phase 2 SRS | Interface requirements define external entities |
| Runbook | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) | Step-by-step procedure |
