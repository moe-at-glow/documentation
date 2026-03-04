> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Use Cases -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-UCT |
| **When to Use** | Document a specific user interaction flow derived from business requirements |
| **Owner** | Business Analyst |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per use case |
| **Runbook** | [Extract Business Requirements](../../runbooks/extract-business-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections Alternative Flows, Exception Flows, Non-Functional Requirements, and Assumptions are optional. Main Flow is sufficient.
> **IF** medium project (3-5 devs) **THEN** All sections required; Open Issues optional if tracked in a backlog tool.
> **IF** large project (6+ devs) **THEN** Full template required.

**Power Atlas classification: Medium project (3 devs) -- All sections required; Open Issues optional.**

---

# UC-001: Calculate Power Requirements

## [x] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-001 |
| Use Case Name | Calculate Power Requirements |
| Version | 1.0 |
| Author | Hasan Hazime |
| Date | 2026-02-15 |
| Status | Approved |

---

## [x] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| Engineer | Human | A GlowPowerRental power engineer who creates and manages power calculations |
| Power Atlas System | System | The calculation engine that processes load data and produces kW/kVA/Amps results |

---

## [x] Description

An Engineer adds electrical loads to a project and the system calculates the total power requirements in kW, kVA, and Amps, applying demand factor and diversity factor to produce a final load summary.

---

## [x] Preconditions

1. The Engineer is authenticated and has an active session.
2. A project exists with voltage, frequency, and default power factor configured.

---

## [x] Postconditions

### [x] Success

1. All loads are saved to the project with their calculated kW, kVA, and Amps values.
2. The project load summary displays individual and total values with demand and diversity factors applied.
3. The project's last-modified timestamp and audit trail are updated.

### [x] Failure

1. No changes are persisted to the database.
2. The user is shown an error message describing the issue.
3. Previously saved loads remain unchanged.

---

## [x] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | Engineer navigates to an existing project | |
| 2 | | System displays the project dashboard with existing loads (if any) and project parameters (voltage, PF, demand factor, diversity factor) |
| 3 | Engineer clicks "Add Load" | |
| 4 | | System displays the load entry form with fields: name, type (Lighting/HVAC/General Power/Motor/Custom), quantity, rated value (Amps or kW), power factor (defaulting to project PF), demand factor, and critical flag |
| 5 | Engineer enters load details: name="AHU-1", type="HVAC", quantity=3, Amps=45, PF=0.85, demand factor=0.8, critical=No | |
| 6 | | System calculates in real time: Single-phase kW = (45 x 230 x 0.85) / 1000 = 8.80 kW per unit; kVA = 8.80 / 0.85 = 10.35 kVA; effective kW = 8.80 x 3 x 0.8 = 21.12 kW |
| 7 | Engineer reviews the calculated values and clicks "Save Load" | |
| 8 | | System saves the load and updates the project load summary table |
| 9 | Engineer repeats steps 3-8 for additional loads | |
| 10 | | System recalculates project totals: sums all effective kW values, applies diversity factor, and computes total kVA and Amps |
| 11 | Engineer reviews the final load summary | |

---

## [x] Alternative Flows

### [x] AF-1: Three-Phase Load Entry

**Trigger:** At Step 5, the Engineer selects "Three-Phase" for the load configuration.

| Step | Actor | System |
|------|-------|--------|
| 5a | Engineer enters load details with three-phase selected: name="Chiller", Amps=120, PF=0.9 | |
| 5b | | System calculates: kW = (120 x 400 x 1.732 x 0.9) / 1000 = 74.83 kW; kVA = 74.83 / 0.9 = 83.14 kVA |

Returns to Main Flow at Step 7.

### [x] AF-2: Enter Load by kW Instead of Amps

**Trigger:** At Step 5, the Engineer enters the load value in kW rather than Amps.

| Step | Actor | System |
|------|-------|--------|
| 5a | Engineer toggles input mode to "kW" and enters kW=18.40, PF=0.8 | |
| 5b | | System performs reverse calculation: Amps = (18.40 x 1000) / (230 x 0.8) = 100.0 Amps; kVA = 18.40 / 0.8 = 23.00 kVA |

Returns to Main Flow at Step 7.

### [x] AF-3: Edit Existing Load

**Trigger:** At Step 3, the Engineer clicks "Edit" on an existing load instead of "Add Load".

| Step | Actor | System |
|------|-------|--------|
| 3a | Engineer clicks "Edit" on an existing load row | |
| 3b | | System populates the load entry form with the existing load's values |
| 3c | Engineer modifies values and clicks "Save Load" | |
| 3d | | System recalculates and updates the load and project totals |

Returns to Main Flow at Step 10.

---

## [x] Exception Flows

### [x] EF-1: Invalid Load Values

**Trigger:** At Step 7, the Engineer submits a load with invalid values (negative Amps, PF > 1.0, or PF <= 0).

| Step | Actor | System |
|------|-------|--------|
| 7a | | System displays validation error: "Power factor must be between 0.01 and 1.0" (or appropriate message for the invalid field) |
| 7b | Engineer corrects the invalid values | |

Returns to Main Flow at Step 7.

### [x] EF-2: Database Save Failure

**Trigger:** At Step 8, the database write fails (SQLite lock contention).

| Step | Actor | System |
|------|-------|--------|
| 8a | | System retries the save operation up to 3 times with exponential backoff |
| 8b | | If retries fail, system displays error: "Unable to save at this time. Please try again in a few moments." |
| 8c | Engineer clicks "Save Load" again | |

Returns to Main Flow at Step 8.

---

## [x] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-001 | Default voltages: 230V single-phase, 400V three-phase (IEC 60038) |
| RULE-002 | Default power factor: 0.8 unless overridden at project or load level |
| RULE-008 | Default demand factors by type: Lighting 1.0, HVAC 0.8, General Power 0.6 |

---

## [x] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-001 | Online power calculation tool |
| BR-002 | Standardized calculation methodology |
| SWR-001 | Single-phase kW calculation |
| SWR-002 | Three-phase kW calculation |
| SWR-003 | kVA calculation |
| SWR-004 | Demand factor application |
| SWR-005 | Diversity factor application |
| SWR-006 | Reverse calculation |
| SWR-012 | Load CRUD |
| SWR-013 | Load summary table |

---

## [x] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | Calculation results must appear within 200ms of input change (SWR-NFR-P001) |
| Security | Engineer must be authenticated with "Engineer" or "Admin" role (SWR-025) |
| Usability | Load entry form must be navigable by keyboard; tab order follows logical field sequence |

---

## [x] Assumptions

1. The Engineer has already created a project with correct voltage and frequency settings before adding loads.
2. The Engineer knows the rated Amps or kW values for the equipment being entered.

---

---

# UC-002: Submit Client Requirements

## [x] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-002 |
| Use Case Name | Submit Client Requirements |
| Version | 1.0 |
| Author | Hasan Hazime |
| Date | 2026-02-15 |
| Status | Approved |

---

## [x] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| Client | Human | An external client who needs temporary power for an event or project |
| Power Atlas System | System | Receives, validates, and stores the requirement submission |

---

## [x] Description

A Client accesses a public web form (no login required) to submit their power requirements for an event or project. The system validates the submission, stores it, and places it in the admin review queue.

---

## [x] Preconditions

1. The public requirements form URL is accessible (no authentication required).
2. The system is online and the requirements module is operational.

---

## [x] Postconditions

### [x] Success

1. The requirement submission is stored in the database with status "New".
2. The Client receives a confirmation page with a reference number.
3. A confirmation email is sent to the Client's provided email address.
4. The submission appears in the admin review queue.

### [x] Failure

1. No submission is stored in the database.
2. The Client is shown an error message with guidance on how to resolve the issue.

---

## [x] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | Client navigates to the public requirements form URL | |
| 2 | | System displays the requirements form with sections: Event/Project Details, Power Requirements, Contact Information, and File Attachments |
| 3 | Client fills in Event/Project Details: event name, date range, location, event type (Concert/Conference/Construction/Industrial/Other), and description | |
| 4 | Client fills in Power Requirements: estimated total load (kW), load breakdown description, special requirements (e.g., redundancy, quiet generators), and preferred generator fuel type | |
| 5 | Client fills in Contact Information: name, company, email, phone number, and preferred language (Arabic/English) | |
| 6 | Client optionally attaches supporting files (site plans, load schedules) up to 10MB total | |
| 7 | Client reviews the form and clicks "Submit Requirements" | |
| 8 | | System validates all required fields (event name, date range, contact name, email, phone) |
| 9 | | System saves the submission with status "New" and generates a unique reference number (format: REQ-YYYYMMDD-XXXX) |
| 10 | | System displays confirmation page: "Your requirements have been submitted. Reference number: REQ-20260315-0042. Our engineering team will review your submission within 2 business days." |
| 11 | | System sends a confirmation email to the Client with the reference number and a summary of submitted details |

---

## [x] Alternative Flows

### [x] AF-1: Client Submits in Arabic

**Trigger:** At Step 2, the Client selects Arabic as the interface language.

| Step | Actor | System |
|------|-------|--------|
| 2a | Client clicks the Arabic language toggle | |
| 2b | | System switches the form to Arabic (RTL layout) with all labels and instructions in Arabic |

Returns to Main Flow at Step 3 (Client fills form in Arabic).

### [x] AF-2: Client Saves as Draft

**Trigger:** At Step 7, the Client is not ready to submit and wants to save progress.

| Step | Actor | System |
|------|-------|--------|
| 7a | Client clicks "Save Draft" instead of "Submit" | |
| 7b | | System saves form data to browser local storage and displays: "Your progress has been saved locally. Return to this page to continue." |

Returns to Main Flow at Step 2 on next visit (form is pre-populated from local storage).

---

## [x] Exception Flows

### [x] EF-1: Missing Required Fields

**Trigger:** At Step 8, validation fails because required fields are empty.

| Step | Actor | System |
|------|-------|--------|
| 8a | | System highlights missing required fields in red and displays: "Please complete the highlighted fields before submitting." |
| 8b | Client fills in the missing fields | |

Returns to Main Flow at Step 7.

### [x] EF-2: File Attachment Too Large

**Trigger:** At Step 6, attached files exceed the 10MB total limit.

| Step | Actor | System |
|------|-------|--------|
| 6a | | System displays: "Total file size exceeds 10MB. Please reduce file sizes or remove attachments." |
| 6b | Client removes or replaces files to reduce total size | |

Returns to Main Flow at Step 7.

### [x] EF-3: Invalid Email Format

**Trigger:** At Step 8, the email address is not in a valid format.

| Step | Actor | System |
|------|-------|--------|
| 8a | | System highlights the email field: "Please enter a valid email address." |
| 8b | Client corrects the email address | |

Returns to Main Flow at Step 7.

---

## [x] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-004 | Client-submitted requirements must be reviewed within 2 business days |
| RULE-005 | Reference numbers follow format REQ-YYYYMMDD-XXXX |

---

## [x] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-004 | Client self-service requirements submission |
| BR-009 | Bilingual support (Arabic RTL / English LTR) |
| BR-012 | Requirements review and approval workflow |
| SWR-015 | Public requirements form |
| SWR-016 | Requirements admin queue |
| SWR-NFR-U002 | Arabic RTL layout support |
| SWR-NFR-U003 | Language switching without page reload |

---

## [x] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | Form submission must complete within 3 seconds including file upload |
| Security | Public form must include CAPTCHA or similar bot protection; file uploads must be scanned for malicious content |
| Usability | Form must work on mobile devices (>= 768px); form progress must be clearly indicated |

---

## [x] Assumptions

1. Clients have a working email address to receive confirmation and edit request notifications.
2. Clients can estimate their power requirements at a high level even if exact load details are unknown.

---

---

# UC-003: Generate PDF Report

## [x] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-003 |
| Use Case Name | Generate PDF Report |
| Version | 1.0 |
| Author | Hasan Hazime |
| Date | 2026-02-16 |
| Status | Approved |

---

## [x] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| Engineer | Human | A GlowPowerRental engineer who needs a professional report for a client or internal review |
| Power Atlas System | System | Generates the PDF using WeasyPrint |

---

## [x] Description

An Engineer generates a professional PDF report for a project that includes the company letterhead, project summary, client details, complete load list with calculations, generator recommendation, and optionally an equipment layout diagram.

---

## [x] Preconditions

1. The Engineer is authenticated with "Engineer" or "Admin" role.
2. The project has at least one load entered with completed calculations.
3. Company letterhead and branding assets are configured in the system.

---

## [x] Postconditions

### [x] Success

1. A PDF report file is generated and stored on the server.
2. The PDF is downloaded to the Engineer's browser.
3. A record of the report generation is added to the project audit trail.

### [x] Failure

1. No PDF file is created.
2. The Engineer is shown an error message describing the issue.

---

## [x] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | Engineer navigates to a project and clicks "Generate Report" | |
| 2 | | System displays the Report Options dialog with checkboxes: Include Project Summary (default: checked), Include Load List (default: checked), Include Generator Recommendation (default: checked), Include Equipment Layout (default: unchecked if no layout exists), Report Language (English/Arabic) |
| 3 | Engineer selects desired sections and report language, then clicks "Generate" | |
| 4 | | System displays a progress indicator: "Generating report..." |
| 5 | | System assembles the HTML report template with: GlowPowerRental letterhead, project reference number and date, client name and contact details, selected sections with calculated data, preparing engineer's name and credentials |
| 6 | | System converts HTML to PDF using WeasyPrint with A4 formatting, page numbers, and table of contents (if > 3 pages) |
| 7 | | System saves the PDF to the file system with naming convention: {ProjectRef}_{Date}_{Version}.pdf |
| 8 | | System prompts the Engineer to download the file |
| 9 | Engineer downloads the PDF | |

---

## [x] Alternative Flows

### [x] AF-1: Generate Arabic Report

**Trigger:** At Step 3, the Engineer selects "Arabic" as the report language.

| Step | Actor | System |
|------|-------|--------|
| 3a | Engineer selects Arabic language | |
| 3b | | System generates the report with Arabic text (RTL), Arabic number formatting, and Arabic letterhead variant |

Returns to Main Flow at Step 4.

### [x] AF-2: Include Equipment Layout

**Trigger:** At Step 3, the Engineer checks "Include Equipment Layout" and a layout exists for the project.

| Step | Actor | System |
|------|-------|--------|
| 3a | Engineer checks "Include Equipment Layout" | |
| 3b | | System exports the layout canvas as a high-resolution image and includes it as a full-page section in the report |

Returns to Main Flow at Step 4.

---

## [x] Exception Flows

### [x] EF-1: No Loads in Project

**Trigger:** At Step 1, the project has no loads entered.

| Step | Actor | System |
|------|-------|--------|
| 1a | | System displays: "Cannot generate report. This project has no loads. Add at least one load before generating a report." |
| 1b | Engineer adds loads to the project | |

Returns to Main Flow at Step 1.

### [x] EF-2: PDF Generation Fails

**Trigger:** At Step 6, WeasyPrint encounters an error during conversion.

| Step | Actor | System |
|------|-------|--------|
| 6a | | System logs the error details for debugging |
| 6b | | System displays: "Report generation failed. Please try again. If the problem persists, contact support." |
| 6c | Engineer clicks "Generate" to retry | |

Returns to Main Flow at Step 4.

---

## [x] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-005 | Reports must include GlowPowerRental logo, project reference number, date, and preparing engineer name |
| RULE-003 | Generator sizing in reports includes 20% safety margin |

---

## [x] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-005 | Professional PDF report generation with company letterhead |
| BR-010 | Data export capabilities (PDF) |
| SWR-026 | PDF report content |
| SWR-027 | PDF report formatting |
| SWR-031 | Layout export in PDF reports |
| SWR-NFR-P002 | PDF generation < 5 seconds for 100 loads |

---

## [x] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | PDF generation must complete within 5 seconds for projects with up to 100 loads (SWR-NFR-P002) |
| Security | Only authenticated Engineers and Admins can generate reports; reports are stored with restricted file system permissions |
| Usability | Report options dialog must be a single screen; generation progress must be clearly indicated |

---

## [x] Assumptions

1. The company letterhead assets (logo, color codes, fonts) have been uploaded and configured in the system by an Admin.
2. The server has WeasyPrint and its dependencies (Cairo, Pango) correctly installed.

---

---

# UC-004: Create Equipment Layout

## [x] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-004 |
| Use Case Name | Create Equipment Layout |
| Version | 1.0 |
| Author | Hasan Hazime |
| Date | 2026-02-17 |
| Status | Approved |

---

## [x] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| Engineer | Human | A GlowPowerRental engineer creating a site power distribution diagram |
| Power Atlas System | System | The React/Konva layout builder that renders and manages the canvas |

---

## [x] Description

An Engineer uses the visual equipment layout builder to create a site power distribution diagram by placing generators, panels, cables, and other equipment on a canvas, connecting them with wire runs, and exporting the result as an image or including it in a PDF report.

---

## [x] Preconditions

1. The Engineer is authenticated with "Engineer" or "Admin" role.
2. A project exists to which the layout will be attached.
3. The Engineer is using a supported browser with JavaScript enabled (Chrome 90+, Firefox 90+, Safari 15+, Edge 90+).

---

## [x] Postconditions

### [x] Success

1. The equipment layout is saved to the project.
2. All equipment positions, connections, and labels are persisted.
3. The layout can be exported as PNG/SVG or included in PDF reports.

### [x] Failure

1. Unsaved changes are lost if the browser is closed without saving.
2. The last saved version of the layout remains intact.

---

## [x] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | Engineer opens a project and clicks "Layout Builder" | |
| 2 | | System loads the React/Konva canvas with grid lines, zoom controls, toolbar, and equipment library panel |
| 3 | Engineer drags a "Generator" from the equipment library onto the canvas | |
| 4 | | System places the generator symbol at the drop location with grid snapping; displays a properties panel showing: label, model (linked to generator database), rated kW/kVA |
| 5 | Engineer sets the generator label to "GEN-01" and selects model "CAT C15 -- 500kVA" from the database | |
| 6 | | System updates the generator symbol with the label and capacity information |
| 7 | Engineer drags a "Distribution Panel" onto the canvas and labels it "MDP-01" | |
| 8 | | System places the panel symbol and displays its properties |
| 9 | Engineer selects the wire tool and draws a cable connection from GEN-01 to MDP-01 | |
| 10 | | System renders a wire line between the two items; displays wire properties: cable type label, length, rating |
| 11 | Engineer sets cable label to "4C x 240mm2 AL" | |
| 12 | Engineer continues adding equipment and connections as needed | |
| 13 | Engineer clicks "Save Layout" | |
| 14 | | System saves all canvas objects, positions, connections, and properties to the database |
| 15 | | System displays: "Layout saved successfully." |

---

## [x] Alternative Flows

### [x] AF-1: Export Layout as Image

**Trigger:** After Step 14, the Engineer wants to export the layout.

| Step | Actor | System |
|------|-------|--------|
| 15a | Engineer clicks "Export" and selects "PNG" or "SVG" | |
| 15b | | System renders the canvas to the selected format at high resolution (2x for PNG) and triggers a download |

Use case ends.

### [x] AF-2: Edit Existing Layout

**Trigger:** At Step 2, a layout already exists for this project.

| Step | Actor | System |
|------|-------|--------|
| 2a | | System loads the existing layout with all saved equipment, connections, and properties |

Returns to Main Flow at Step 3 (Engineer can add, move, or delete items).

### [x] AF-3: Undo/Redo Operations

**Trigger:** At any step after Step 3, the Engineer wants to undo the last action.

| Step | Actor | System |
|------|-------|--------|
| Xa | Engineer presses Ctrl+Z (or clicks Undo button) | |
| Xb | | System reverts the last canvas action (place, move, connect, delete) |
| Xc | Engineer presses Ctrl+Y (or clicks Redo button) to redo if needed | |
| Xd | | System re-applies the reverted action |

Returns to the step where the undo was triggered.

---

## [x] Exception Flows

### [x] EF-1: Browser Crashes or Tab Closed Without Saving

**Trigger:** The browser closes unexpectedly before the Engineer saves.

| Step | Actor | System |
|------|-------|--------|
| Xa | | System has auto-saved the layout to browser local storage every 60 seconds |
| Xb | Engineer reopens the layout builder | |
| Xc | | System detects unsaved local changes and prompts: "Unsaved changes were recovered. Do you want to restore them?" |
| Xd | Engineer clicks "Restore" | |

Returns to Main Flow at the state where auto-save occurred.

### [x] EF-2: Canvas Performance Degradation

**Trigger:** The canvas drops below 30 FPS due to too many items (> 50).

| Step | Actor | System |
|------|-------|--------|
| Xa | | System displays a warning: "Layout contains many items. Performance may be affected. Consider splitting into multiple layouts." |

Engineer continues working or simplifies the layout.

---

## [x] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-003 | Generator symbols must display rated capacity from the generator database |
| RULE-001 | Voltage labels on connections should reference IEC standard voltages |

---

## [x] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-006 | Equipment layout visualization |
| BR-007 | Generator database (linked to equipment properties) |
| SWR-028 | Layout canvas with zoom/pan/grid/undo |
| SWR-029 | Equipment library with standard symbols |
| SWR-030 | Wire connections |
| SWR-031 | Layout export (PNG, SVG, PDF inclusion) |
| SWR-NFR-P004 | Canvas >= 30 FPS with 50 items |

---

## [x] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | Canvas must maintain >= 30 FPS with up to 50 equipment items (SWR-NFR-P004) |
| Security | Only Engineers and Admins can create/edit layouts; layouts are project-scoped |
| Usability | Equipment drag-and-drop must work with mouse and touch; grid snapping helps alignment |

---

## [x] Assumptions

1. Engineers are familiar with basic electrical distribution symbols and terminology.
2. The layout builder is used on devices with screens >= 1024px wide for practical usability.
3. Complex CAD-level detail is not required; the layout builder provides schematic-level diagrams.

---

---

# UC-005: Review and Approve Requirements

## [x] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-005 |
| Use Case Name | Review and Approve Requirements |
| Version | 1.0 |
| Author | Hasan Hazime |
| Date | 2026-02-18 |
| Status | Approved |

---

## [x] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| Admin/Engineer | Human | A GlowPowerRental admin or engineer who reviews client-submitted requirements |
| Client | Human | The external client who submitted the requirements (receives notifications) |
| Power Atlas System | System | Manages the review pipeline and sends notifications |

---

## [x] Description

An Admin or Engineer reviews a client-submitted requirement from the admin queue, evaluates the completeness and feasibility of the request, and either approves it (creating a new project), rejects it (with a reason), or requests edits (triggering a notification to the client with an edit link).

---

## [x] Preconditions

1. The Admin/Engineer is authenticated with "Admin" or "Engineer" role.
2. At least one requirement submission exists with status "New" or "Updated" in the review queue.

---

## [x] Postconditions

### [x] Success (Approve)

1. The requirement submission status is changed to "Approved".
2. A new project is created from the requirement details (if the reviewer chooses).
3. The Client receives an email notification that their requirements have been approved.

### [x] Success (Reject)

1. The requirement submission status is changed to "Rejected" with a reason.
2. The Client receives an email notification with the rejection reason.

### [x] Success (Request Edits)

1. The requirement submission status is changed to "Edit Requested".
2. The Client receives an email with specific edit instructions and a unique link to update their submission.

### [x] Failure

1. The requirement submission status remains unchanged.
2. The reviewer is shown an error message.

---

## [x] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | Admin/Engineer navigates to the Requirements Review Queue | |
| 2 | | System displays all submissions organized by status tabs (New, Updated, Under Review, Approved, Rejected, Edit Requested) with "New" tab active by default; shows submission date, client name, event name, and estimated load for each entry |
| 3 | Admin/Engineer clicks on a submission to review | |
| 4 | | System displays the full submission details: event/project information, power requirements description, contact details, attached files, and submission history (including any previous edit cycles) |
| 5 | | System changes the submission status to "Under Review" |
| 6 | Admin/Engineer reviews all details and attached files | |
| 7 | Admin/Engineer clicks "Approve" | |
| 8 | | System prompts: "Create a new project from this requirement?" with options Yes/No |
| 9 | Admin/Engineer clicks "Yes" | |
| 10 | | System creates a new project pre-populated with client details, event name, and estimated load from the submission |
| 11 | | System changes submission status to "Approved" and links it to the new project |
| 12 | | System sends approval notification email to the Client |

---

## [x] Alternative Flows

### [x] AF-1: Reject Requirements

**Trigger:** At Step 7, the Admin/Engineer determines the requirements are not feasible or out of scope.

| Step | Actor | System |
|------|-------|--------|
| 7a | Admin/Engineer clicks "Reject" | |
| 7b | | System displays a mandatory comment field: "Please provide a reason for rejection" |
| 7c | Admin/Engineer enters reason: "Requested capacity exceeds our available fleet for the specified dates. Please contact us to discuss alternative arrangements." | |
| 7d | Admin/Engineer clicks "Confirm Rejection" | |
| 7e | | System changes submission status to "Rejected" with the reason |
| 7f | | System sends rejection notification email to the Client with the reason |

Use case ends.

### [x] AF-2: Request Edits

**Trigger:** At Step 7, the Admin/Engineer determines the submission needs additional information or corrections.

| Step | Actor | System |
|------|-------|--------|
| 7a | Admin/Engineer clicks "Request Edits" | |
| 7b | | System displays a mandatory comment field: "Please describe what changes are needed" |
| 7c | Admin/Engineer enters instructions: "Please provide a detailed load breakdown (number and type of HVAC units, lighting circuits, and general power outlets). Also, please confirm the event dates." | |
| 7d | Admin/Engineer clicks "Send Edit Request" | |
| 7e | | System changes submission status to "Edit Requested" |
| 7f | | System generates a unique edit link (valid for 14 days) |
| 7g | | System sends an email to the Client with the edit instructions and the unique link |

Use case ends. The Client uses the link (see UC-002 AF or SWR-018) to update and resubmit, which changes the status to "Updated" and the submission re-enters the queue.

### [x] AF-3: Approve Without Creating Project

**Trigger:** At Step 9, the Admin/Engineer clicks "No" when prompted to create a project.

| Step | Actor | System |
|------|-------|--------|
| 9a | Admin/Engineer clicks "No" | |
| 9b | | System changes submission status to "Approved" without creating a project |
| 9c | | System sends approval notification email to the Client |

Use case ends.

---

## [x] Exception Flows

### [x] EF-1: Submission Already Under Review

**Trigger:** At Step 3, another reviewer has already opened the same submission.

| Step | Actor | System |
|------|-------|--------|
| 3a | | System displays a warning: "This submission is currently being reviewed by [Reviewer Name]. You may view it in read-only mode." |
| 3b | Admin/Engineer views the submission in read-only mode or selects a different submission | |

Returns to Main Flow at Step 2 or ends.

### [x] EF-2: Email Notification Fails

**Trigger:** At Step 12, 7f, or 7g, the email notification fails to send.

| Step | Actor | System |
|------|-------|--------|
| Xa | | System logs the email failure and displays a warning: "Review action saved, but email notification could not be sent. Client email: [email]. Please notify them manually." |
| Xb | Admin/Engineer notes the email address for manual follow-up | |

Use case ends (the review action itself was still successful).

---

## [x] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-004 | Client-submitted requirements must be reviewed within 2 business days |
| RULE-007 | All review actions and comments are retained as part of the permanent record |

---

## [x] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-004 | Client self-service requirements submission |
| BR-012 | Requirements review and approval workflow |
| SWR-016 | Requirements admin review queue with filters |
| SWR-017 | Review actions: approve, reject, request edits |
| SWR-018 | Client edit response via unique link |
| SWR-033 | Audit trail logging |

---

## [x] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | Review queue must load within 2 seconds; status changes must persist within 1 second |
| Security | Only Admin and Engineer roles can access the review queue; submission details contain client PII and must be access-controlled |
| Usability | Status tabs must show count badges; review actions must require confirmation to prevent accidental approvals/rejections |

---

## [x] Assumptions

1. The Client's email address provided in the submission is valid and can receive notifications.
2. Admins and Engineers have sufficient domain knowledge to evaluate power requirements feasibility.
3. Only one reviewer should actively work on a submission at a time to avoid conflicting actions.

---

## COMPLETION CHECKLIST

- [x] All required sections filled for each use case
- [x] Reviewed by Tech Lead
- [x] Approved by Product Owner
- [x] Stored in project SharePoint / repository
- [x] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Extract Business Requirements](../../runbooks/extract-business-requirements.md) |
| Business Requirements Document | [BRD](business-requirements-document.md) |
| Software Requirements Specification | [SRS](software-requirements-specification.md) |
| Requirements Traceability Matrix | [RTM](requirements-traceability-matrix.md) |
