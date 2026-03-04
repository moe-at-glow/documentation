> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Software Requirements Specification (SRS)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-SRS |
| **When to Use** | Derive and document software requirements from an approved BRD |
| **Owner** | Business Analyst / Tech Lead |
| **Reviewer** | QA Lead |
| **SLA** | 10 business days from BRD baseline |
| **Runbook** | [Derive Software Requirements](../../runbooks/derive-software-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 3.2.3-3.2.5 (Usability/Reliability/Scalability), 3.3.2 (Hardware Interfaces), 3.3.4 (Communications Interfaces), and Appendices are optional.
> **IF** medium project (3-5 devs) **THEN** All Section 3 subsections required; Appendices optional if covered in separate documents.
> **IF** large project (6+ devs) **THEN** Full template required. Aligned with ISO/IEC/IEEE 29148.

**Power Atlas classification: Medium project (3 devs) -- All Section 3 subsections required; Appendices optional.**

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Document Title | Power Atlas -- Software Requirements Specification |
| Version | 1.1 |
| Status | Approved |
| Author | Hasan Hazime |
| Date Created | 2026-02-01 |
| Last Updated | 2026-02-28 |
| Related BRD | Power Atlas BRD v1.2 (2026-02-20) |

### [x] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | 2026-02-01 | Hasan Hazime | Initial draft derived from BRD v1.0 |
| 0.2 | 2026-02-10 | Hasan Hazime | Added layout builder and generator database requirements |
| 1.0 | 2026-02-20 | Hasan Hazime | Complete SRS aligned with BRD v1.2 |
| 1.1 | 2026-02-28 | Hasan Hazime | Incorporated QA review feedback; finalized NFRs |

### [x] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Omar Farouk | Tech Lead | Approved | 2026-02-26 |
| Hasan Hazime | Product Owner | Approved | 2026-02-27 |
| Layla Ibrahim | QA Lead | Approved | 2026-02-28 |

---

## [x] 1. Introduction

### [x] 1.1 Purpose

This Software Requirements Specification defines the functional and non-functional requirements for Power Atlas, a web-based power calculation and project management tool developed for GlowPowerRental. It translates the business requirements documented in the BRD into implementable software requirements that will guide the design, development, and testing of the system.

### [x] 1.2 Scope

Power Atlas is a web application comprising a Python/Flask backend with SQLite database, a Vite/Tailwind CSS frontend, and a React/Konva-based equipment layout builder. The system provides power calculations (kW, kVA, Amps) for single-phase and three-phase configurations, project management with client association, a public client requirements portal, PDF report generation, a visual equipment layout builder, and a searchable generator database. The system enforces role-based access control with Admin, Engineer, and Client roles and supports bilingual Arabic/English interfaces.

### [x] 1.3 Definitions and Acronyms

| Term | Definition |
|------|-----------|
| kW | Kilowatt -- unit of real (active) power |
| kVA | Kilovolt-Ampere -- unit of apparent power |
| PF | Power Factor -- ratio of real power to apparent power |
| DF | Demand Factor -- ratio of maximum demand to total connected load |
| DivF | Diversity Factor -- ratio of sum of individual max demands to system max demand |
| CRUD | Create, Read, Update, Delete operations |
| RTL | Right-to-Left text direction (Arabic) |
| LTR | Left-to-Right text direction (English) |
| Konva | JavaScript 2D canvas library used for the layout builder |

### [x] 1.4 References

| Document | Version | Date |
|----------|---------|------|
| Power Atlas -- Business Requirements Document | 1.2 | 2026-02-20 |
| IEC 60038 -- Standard Voltages | Ed. 7.0 | 2009 |
| GlowPowerRental Calculation Standards Manual | 3.1 | 2025-11-01 |
| WCAG 2.1 Accessibility Guidelines | 2.1 | 2018-06-05 |

---

## [x] 2. Overall Description

### [x] 2.1 Product Perspective

Power Atlas is a new, standalone web application that replaces the existing Excel-based power calculation workflow. It does not integrate with external systems in its initial release but is designed with a REST API architecture to support future integration with GlowPowerRental's ERP and inventory systems.

```
                                    +-------------------+
                                    |   Power Atlas     |
                                    |   Web Application |
+----------------+                  |                   |                  +----------------+
| Engineers      | <-- HTTPS/UI --> | - Flask Backend   | <-- SQLite -->   | SQLite         |
| (Browser)      |                  | - Vite Frontend   |                  | Database       |
+----------------+                  | - React/Konva     |                  +----------------+
                                    |   Layout Builder  |
+----------------+                  |                   |                  +----------------+
| Admin Users    | <-- HTTPS/UI --> | - PDF Generation  |                  | File System    |
| (Browser)      |                  |   (WeasyPrint)    | <-- File I/O --> | (Reports,      |
+----------------+                  |                   |                  |  Uploads)      |
                                    |                   |                  +----------------+
+----------------+                  |                   |
| Clients        | <-- HTTPS/UI --> |                   |
| (Browser/      |                  +-------------------+
|  Public Form)  |
+----------------+
```

### [x] 2.2 Product Functions

| Function | Description |
|----------|-------------|
| Power Calculation Engine | Compute kW, kVA, and Amps for single-phase and three-phase loads with PF, demand factor, and diversity factor |
| Project Management | Create, organize, share, and track power calculation projects with client association |
| Load Management | Add, edit, and categorize electrical loads within a project |
| Client Requirements Portal | Public form for clients to submit power requirements; admin review pipeline |
| PDF Report Generation | Generate professional reports with company letterhead, load summaries, and generator recommendations |
| Equipment Layout Builder | Visual drag-and-drop canvas for creating site power distribution diagrams |
| Generator Database | Searchable catalog of generators with filtering and selection assistance |
| User Management | Registration, authentication, role-based access control |

### [x] 2.3 User Characteristics

| User Type | Description | Technical Proficiency | Frequency of Use |
|-----------|-------------|----------------------|-----------------|
| Admin | System administrators who manage users, generator database, and system settings | High | Daily |
| Engineer | Power engineers who create projects, perform calculations, and generate reports | Medium | Daily |
| Client | External clients who submit requirements and view submission status | Low | Monthly |

### [x] 2.4 Constraints

| Constraint | Description |
|-----------|-------------|
| Technology Stack | Backend: Python 3.11+ / Flask; Database: SQLite; Frontend: Vite + Tailwind CSS; Layout Builder: React + Konva.js |
| Deployment | On-premises Linux server; no cloud dependencies |
| Browser Support | Chrome 90+, Firefox 90+, Safari 15+, Edge 90+ |
| Database | SQLite -- single-writer concurrency model; sufficient for expected user base |
| Budget | Internal development team only; no third-party commercial component licenses |

### [x] 2.5 Assumptions

| ID | Assumption |
|----|-----------|
| ASM-001 | Users have modern web browsers with JavaScript enabled |
| ASM-002 | Server has minimum 4GB RAM and 50GB storage available |
| ASM-003 | Network latency between users and server is < 100ms |
| ASM-004 | Generator catalog contains < 500 models at launch |

---

## [x] 3. Specific Requirements

### [x] 3.1 Functional Requirements

#### Power Calculation Module

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-001 | Single-Phase kW Calculation | The system shall calculate single-phase real power using the formula: kW = (Amps x Voltage x PF) / 1000, where default voltage is 230V | M | BR-001, BR-002 | Given a load with Amps=100, Voltage=230V, PF=0.8, When calculation is performed, Then kW = 18.40 | Approved |
| SWR-002 | Three-Phase kW Calculation | The system shall calculate three-phase real power using the formula: kW = (Amps x Voltage x sqrt(3) x PF) / 1000, where default voltage is 400V | M | BR-001, BR-002 | Given a load with Amps=100, Voltage=400V, PF=0.8, When calculation is performed, Then kW = 55.42 | Approved |
| SWR-003 | kVA Calculation | The system shall calculate apparent power using the formula: kVA = kW / PF | M | BR-001, BR-002 | Given kW=18.40 and PF=0.8, When calculation is performed, Then kVA = 23.00 | Approved |
| SWR-004 | Demand Factor Application | The system shall apply a demand factor to each load, reducing the effective load by the specified ratio (0.0 to 1.0) | M | BR-001, BR-002 | Given a load of 100 kW with demand factor 0.6, When totals are calculated, Then the effective load contribution is 60 kW | Approved |
| SWR-005 | Diversity Factor Application | The system shall apply a diversity factor to the total project load to account for non-simultaneous operation | M | BR-001, BR-002 | Given total demand of 500 kW and diversity factor of 0.8, When project total is calculated, Then diversified total is 400 kW | Approved |
| SWR-006 | Reverse Calculation | The system shall support reverse calculations (given kW, calculate Amps; given kVA, calculate kW) | S | BR-001 | Given kW=18.40, Voltage=230V, PF=0.8 for single-phase, When reverse calculation is performed, Then Amps = 100.0 | Approved |

#### Project Management

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-007 | Project CRUD | The system shall allow Engineers and Admins to create, read, update, and delete projects with properties: name, reference number, voltage, frequency, power factor, demand factor, diversity factor, status, and notes | M | BR-003 | Given an authenticated Engineer, When they create a project with all required fields, Then the project is saved and appears in their project list | Approved |
| SWR-008 | Project Folder Organization | The system shall allow users to organize projects into hierarchical folders (up to 3 levels deep) | S | BR-003 | Given an Engineer with multiple projects, When they create a folder and drag projects into it, Then projects are organized under that folder | Approved |
| SWR-009 | Project Sharing | The system shall allow project owners to share projects with other Engineers with either "View" or "Edit" permissions | S | BR-011 | Given a project owner, When they share a project with another Engineer with "Edit" permission, Then that Engineer can modify the project | Approved |
| SWR-010 | Project Status Tracking | The system shall track project status through states: Draft, In Progress, Under Review, Approved, Completed, Archived | M | BR-003 | Given a project in "Draft" status, When the Engineer changes status to "In Progress", Then the status is updated and the change is logged | Approved |
| SWR-011 | Client Association | The system shall allow linking a project to a client record with name, contact person, email, phone, and address fields | M | BR-003 | Given a project, When the Engineer associates a client, Then the client details are linked and displayed on the project | Approved |

#### Load Management

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-012 | Load CRUD | The system shall allow adding, editing, and deleting loads within a project with properties: name, type (Lighting/HVAC/General Power/Motor/Custom), quantity, rated power (kW or Amps), power factor, demand factor, and critical flag | M | BR-001, BR-003 | Given a project, When an Engineer adds a load with name="AHU-1", type="HVAC", quantity=3, Amps=45, Then three loads are created and included in the project calculation | Approved |
| SWR-013 | Load Summary Table | The system shall display a summary table of all loads in a project showing individual and total kW, kVA, and Amps with demand and diversity factors applied | M | BR-001, BR-010 | Given a project with multiple loads, When viewing the project, Then a summary table shows each load's calculated values and project totals | Approved |
| SWR-014 | Critical Load Flagging | The system shall allow marking loads as "Critical" to distinguish essential loads that require dedicated or redundant power supply | S | BR-001 | Given a load marked as Critical, When viewing the project summary, Then critical loads are visually distinguished and their subtotal is shown separately | Approved |

#### Client Requirements Portal

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-015 | Public Requirements Form | The system shall provide a publicly accessible form (no authentication required) for clients to submit power requirements including: event name, date range, location, estimated load description, contact details, and file attachments | M | BR-004 | Given an unauthenticated user, When they access the requirements URL and complete the form, Then the submission is saved and a confirmation is displayed with a reference number | Approved |
| SWR-016 | Requirements Admin Queue | The system shall present submitted requirements in an admin review queue with filtering by status (New, Under Review, Approved, Rejected, Edit Requested) and sorting by submission date | M | BR-004, BR-012 | Given an Admin or Engineer, When they access the requirements queue, Then they see all submissions organized by status with newest first | Approved |
| SWR-017 | Requirements Review Actions | The system shall allow Admins and Engineers to approve, reject, or request edits on submitted requirements, with mandatory comments for reject and edit request actions | M | BR-012 | Given a submission in "New" status, When an Admin selects "Request Edits" and provides comments, Then the status changes to "Edit Requested" and the client is notified | Approved |
| SWR-018 | Client Edit Response | The system shall allow clients to respond to edit requests by updating their submission using a unique link sent to their email | S | BR-012 | Given a submission with "Edit Requested" status, When the client uses the edit link and updates their information, Then the status changes to "Updated" and re-enters the review queue | Approved |

#### Generator Database

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-019 | Generator Catalog | The system shall maintain a database of generators with fields: model, manufacturer, rated kW, rated kVA, voltage, frequency, fuel type, noise level (dB), dimensions, weight, and fuel consumption | M | BR-007 | Given an Admin user, When they add a generator with all required fields, Then the generator appears in the searchable catalog | Approved |
| SWR-020 | Generator Search and Filter | The system shall allow searching generators by model/manufacturer name and filtering by kW range, kVA range, voltage, fuel type, and manufacturer | M | BR-007 | Given an Engineer searching for generators, When they filter by kW >= 100 and fuel type = "Diesel", Then only matching generators are displayed | Approved |
| SWR-021 | Generator Recommendation | The system shall recommend suitable generators based on a project's total calculated load (including the 20% safety margin), showing the best-fit options sorted by closest capacity match | S | BR-007, BR-013 | Given a project with 400 kW total load, When the Engineer requests a recommendation, Then the system shows generators with capacity >= 480 kW (400 x 1.2) sorted by capacity ascending | Approved |

#### Authentication and Authorization

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-022 | User Registration | The system shall allow new user registration with email, name, password (minimum 8 characters, must contain uppercase, lowercase, and number), and role assignment (by Admin only) | M | BR-008 | Given a new user, When they register with valid details, Then an account is created with default "Engineer" role pending Admin approval | Approved |
| SWR-023 | User Authentication | The system shall authenticate users via email and password with session-based management; sessions expire after 8 hours of inactivity | M | BR-008 | Given a registered user, When they provide correct credentials, Then they are authenticated and redirected to the dashboard | Approved |
| SWR-024 | Account Lockout | The system shall lock a user account after 5 consecutive failed login attempts for a duration of 30 minutes | M | BR-008 | Given a user with 4 failed attempts, When they fail a 5th time, Then the account is locked and subsequent login attempts are rejected for 30 minutes | Approved |
| SWR-025 | Role-Based Permissions | The system shall enforce role-based access: Admins have full access; Engineers can manage own projects, calculations, and view generator database; Clients can only view their own requirement submissions | M | BR-008 | Given an Engineer user, When they attempt to access Admin settings, Then access is denied with a 403 response | Approved |

#### PDF Report Generation

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-026 | PDF Report Content | The system shall generate PDF reports containing: company letterhead, project summary, client details, load list with calculations, generator recommendation, and preparing engineer details | M | BR-005 | Given a project with loads and a generator selection, When the Engineer clicks "Generate Report", Then a PDF is created containing all specified sections | Approved |
| SWR-027 | PDF Report Formatting | The system shall format PDF reports using WeasyPrint with A4 page size, company color scheme, page numbers, and table of contents for reports exceeding 3 pages | M | BR-005 | Given a generated PDF, When opened, Then it displays correct letterhead, consistent formatting, and page numbers | Approved |

#### Equipment Layout Builder

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-028 | Layout Canvas | The system shall provide an interactive canvas (React/Konva) with zoom, pan, grid snapping, and undo/redo functionality for creating equipment layout diagrams | S | BR-006 | Given the layout builder, When an Engineer opens it, Then a canvas is displayed with grid lines, zoom controls, and toolbar | Approved |
| SWR-029 | Equipment Library | The system shall provide a draggable equipment library containing generators, distribution panels, cable runs, transformers, and load connection points with standard electrical symbols | S | BR-006 | Given the equipment library panel, When an Engineer drags a generator onto the canvas, Then the generator symbol is placed at the drop location with default properties | Approved |
| SWR-030 | Wire Connections | The system shall allow drawing cable/wire connections between equipment items on the canvas with configurable cable type labels and routing | S | BR-006 | Given two equipment items on the canvas, When the Engineer draws a wire between them, Then a connection line is rendered and stored as part of the layout | Approved |
| SWR-031 | Layout Export | The system shall export equipment layouts as PNG and SVG images, and include them in PDF reports | S | BR-006, BR-005, BR-010 | Given a completed layout, When the Engineer clicks "Export as PNG", Then a high-resolution PNG image is downloaded | Approved |

#### Data Export and Audit

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-032 | Excel Export | The system shall export project load lists to Excel (.xlsx) format with all calculation columns, formulas preserved as values, and project metadata in a header row | M | BR-010 | Given a project with loads, When the Engineer clicks "Export to Excel", Then an .xlsx file is downloaded containing the complete load list | Approved |
| SWR-033 | Audit Trail Logging | The system shall log all project modifications (create, update, delete, status change, share) with user ID, timestamp, action type, and change details | S | BR-014 | Given a project modification, When the change is saved, Then an audit log entry is created with all required fields | Approved |
| SWR-034 | Audit Trail Viewing | The system shall allow Admins to view the audit trail for any project, filtered by date range and action type | S | BR-014 | Given an Admin viewing a project's audit trail, When they filter by date range, Then only matching entries are displayed in reverse chronological order | Approved |

### [x] 3.2 Non-Functional Requirements

#### [x] 3.2.1 Performance

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-P001 | The system shall return power calculation results within 200ms of form submission | M | Response time measured from form submit to result display; 95th percentile < 200ms under normal load | Approved |
| SWR-NFR-P002 | The system shall generate PDF reports within 5 seconds for projects with up to 100 loads | M | PDF generation time measured from button click to download prompt; 95th percentile < 5 seconds | Approved |
| SWR-NFR-P003 | The system shall load the project dashboard within 2 seconds on first access | S | Page load time measured from navigation to fully interactive state; 95th percentile < 2 seconds | Approved |
| SWR-NFR-P004 | The layout builder canvas shall maintain >= 30 FPS with up to 50 equipment items | S | Frame rate measured during drag operations with 50 items on canvas | Approved |

#### [x] 3.2.2 Security

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-S001 | The system shall store passwords using bcrypt with a minimum cost factor of 12 | M | Password hashes in database use bcrypt algorithm; plain-text passwords are never stored or logged | Approved |
| SWR-NFR-S002 | The system shall enforce HTTPS for all traffic in production | M | All HTTP requests are redirected to HTTPS; HSTS header is set | Approved |
| SWR-NFR-S003 | The system shall implement CSRF protection on all state-changing requests | M | All POST/PUT/DELETE requests include a valid CSRF token; requests without tokens are rejected | Approved |
| SWR-NFR-S004 | The system shall sanitize all user inputs to prevent XSS and SQL injection attacks | M | Input validation is applied on both client and server; no raw SQL queries with user input | Approved |

#### [x] 3.2.3 Usability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-U001 | The system shall comply with WCAG 2.1 Level AA accessibility guidelines | S | Automated accessibility scan (axe-core) reports zero critical or serious violations | Approved |
| SWR-NFR-U002 | The system shall support full Arabic RTL layout with correct text alignment, mirrored navigation, and RTL-aware form controls | S | All pages render correctly in RTL mode; no overlapping text or misaligned elements | Approved |
| SWR-NFR-U003 | The system shall allow language switching between Arabic and English without page reload | S | Given a user on any page, When they toggle the language selector, Then all UI text switches language and layout direction updates immediately | Approved |

#### [x] 3.2.4 Reliability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-R001 | The system shall maintain 99.5% uptime during business hours (Sunday-Thursday 07:00-19:00 AST) | M | Uptime monitoring shows >= 99.5% availability measured monthly | Approved |
| SWR-NFR-R002 | The system shall perform automated daily database backups retained for 30 days | M | Backup script runs daily at 02:00 AST; backup files verified weekly by restore test | Approved |
| SWR-NFR-R003 | The system shall gracefully handle database write contention (SQLite locking) by retrying with exponential backoff up to 3 attempts | S | When concurrent writes cause a lock, the system retries transparently; users see an error only after 3 failed attempts | Approved |

#### [x] 3.2.5 Scalability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-SC001 | The system shall support 100 concurrent users without performance degradation | M | Load testing with 100 simulated users shows all response times within specified SLAs | Approved |
| SWR-NFR-SC002 | The system shall support up to 10,000 projects and 500,000 load records without query performance degradation | S | Query response times remain within SLA with test dataset of specified size | Approved |

### [x] 3.3 Interface Requirements

#### [x] 3.3.1 User Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-UI-001 | The system shall provide a responsive web interface that adapts to screen widths from 768px (tablet) to 2560px (widescreen desktop) | S | Approved |
| SWR-UI-002 | The system shall use Tailwind CSS for consistent styling with GlowPowerRental brand colors (primary: #1E3A5F navy, accent: #F59E0B amber, background: #F8FAFC) | M | Approved |
| SWR-UI-003 | The system shall provide keyboard navigation for all primary workflows (calculations, project management) | S | Approved |

#### [x] 3.3.2 Hardware Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-HW-001 | The system shall run on a Linux server with minimum 4 CPU cores, 4GB RAM, and 50GB SSD storage | M | Approved |

#### [x] 3.3.3 Software Interfaces

| ID | Description | Protocol/Format | Priority | Status |
|----|-------------|----------------|----------|--------|
| SWR-SW-001 | The system shall expose a RESTful API for all data operations to support future external integrations | JSON over HTTPS | S | Approved |
| SWR-SW-002 | The system shall use WeasyPrint library for HTML-to-PDF conversion | Python library (local) | M | Approved |
| SWR-SW-003 | The system shall use openpyxl library for Excel file generation | Python library (local) | M | Approved |

#### [x] 3.3.4 Communications Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-COM-001 | The system shall send email notifications for requirement submission confirmations and edit requests via SMTP | S | Approved |

### [x] 3.4 Data Requirements

| ID | Description | Retention Period | Priority | Status |
|----|-------------|-----------------|----------|--------|
| SWR-DATA-001 | Project data (including loads, calculations, and client associations) shall be retained for a minimum of 5 years from project completion date | 5 years | M | Approved |
| SWR-DATA-002 | Audit trail records shall be retained for a minimum of 5 years and shall not be editable or deletable by any user | 5 years | M | Approved |
| SWR-DATA-003 | Generated PDF reports shall be stored on the file system with a reference in the database for a minimum of 3 years | 3 years | S | Approved |
| SWR-DATA-004 | Client requirement submissions and their attachments shall be retained for 2 years from submission date | 2 years | S | Approved |

---

## [x] 4. Traceability to Business Requirements

| SWR ID | BR ID | Notes |
|--------|-------|-------|
| SWR-001 | BR-001, BR-002 | Single-phase power formula |
| SWR-002 | BR-001, BR-002 | Three-phase power formula |
| SWR-003 | BR-001, BR-002 | Apparent power formula |
| SWR-004 | BR-001, BR-002 | Demand factor application |
| SWR-005 | BR-001, BR-002 | Diversity factor application |
| SWR-006 | BR-001 | Reverse calculation capability |
| SWR-007 | BR-003 | Project CRUD operations |
| SWR-008 | BR-003 | Folder organization |
| SWR-009 | BR-011 | Project sharing |
| SWR-010 | BR-003 | Status tracking |
| SWR-011 | BR-003 | Client association |
| SWR-012 | BR-001, BR-003 | Load management |
| SWR-013 | BR-001, BR-010 | Load summary display |
| SWR-014 | BR-001 | Critical load flagging |
| SWR-015 | BR-004 | Public requirements form |
| SWR-016 | BR-004, BR-012 | Admin review queue |
| SWR-017 | BR-012 | Review actions |
| SWR-018 | BR-012 | Client edit response |
| SWR-019 | BR-007 | Generator catalog |
| SWR-020 | BR-007 | Generator search/filter |
| SWR-021 | BR-007, BR-013 | Generator recommendation |
| SWR-022 | BR-008 | User registration |
| SWR-023 | BR-008 | Authentication |
| SWR-024 | BR-008 | Account lockout |
| SWR-025 | BR-008 | Role-based permissions |
| SWR-026 | BR-005 | PDF report content |
| SWR-027 | BR-005 | PDF report formatting |
| SWR-028 | BR-006 | Layout canvas |
| SWR-029 | BR-006 | Equipment library |
| SWR-030 | BR-006 | Wire connections |
| SWR-031 | BR-006, BR-005, BR-010 | Layout export |
| SWR-032 | BR-010 | Excel export |
| SWR-033 | BR-014 | Audit logging |
| SWR-034 | BR-014 | Audit viewing |

Full traceability: [Requirements Traceability Matrix](requirements-traceability-matrix.md)

---

## [x] 5. Appendices

### [x] Appendix A: Use Cases

See [Use Cases](use-cases.md) for the top 5 detailed use case specifications:
- UC-001: Calculate Power Requirements
- UC-002: Submit Client Requirements
- UC-003: Generate PDF Report
- UC-004: Create Equipment Layout
- UC-005: Review and Approve Requirements

### [x] Appendix B: Calculation Formula Reference

| Calculation | Formula | Variables |
|------------|---------|-----------|
| Single-Phase kW | kW = (Amps x V x PF) / 1000 | V = 230V default |
| Three-Phase kW | kW = (Amps x V x sqrt(3) x PF) / 1000 | V = 400V default |
| kVA from kW | kVA = kW / PF | |
| Amps from kW (1-phase) | Amps = (kW x 1000) / (V x PF) | V = 230V default |
| Amps from kW (3-phase) | Amps = (kW x 1000) / (V x sqrt(3) x PF) | V = 400V default |
| Effective Load | Effective kW = kW x Quantity x Demand Factor | |
| Diversified Total | Total kW = Sum(Effective kW) x Diversity Factor | |
| Generator Sizing | Required kVA = Diversified Total kVA x 1.2 | 20% safety margin |

---

## COMPLETION CHECKLIST

- [x] All required sections filled
- [x] Every SWR traces to at least one BR
- [x] Reviewed by QA Lead
- [x] Approved by Tech Lead and Product Owner
- [x] Stored in project SharePoint / repository
- [x] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Derive Software Requirements](../../runbooks/derive-software-requirements.md) |
| Business Requirements Document | [BRD](business-requirements-document.md) |
| Requirements Traceability Matrix | [RTM](requirements-traceability-matrix.md) |
| Use Cases | [Use Cases](use-cases.md) |
