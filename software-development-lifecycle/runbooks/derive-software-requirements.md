# Derive Software Requirements

Step-by-step procedure to decompose business requirements into software requirements.

---

## Prerequisites

- Approved and baselined BRD.
- Completed stakeholder analysis.
- Tech lead and business analyst available.

---

## Procedure

### Step 1: Review Approved Business Requirements

1. Read the baselined BRD.
2. List all Must Have and Should Have business requirements.
3. Identify any requirements that need clarification. Resolve with the Product Owner before proceeding.

### Step 2: Identify System Boundaries and Interfaces

Define what is inside and outside the system:

| Boundary Element | Description |
|-----------------|-------------|
| System Scope | What the software system is responsible for |
| External Systems | Systems the software integrates with (payment gateway, ERP, IoT sensors) |
| User Interfaces | How users interact with the system (web app, mobile app, dashboard) |
| Data Interfaces | Data flowing in and out (API calls, file imports, sensor data) |
| Infrastructure | Servers, databases, message brokers the system depends on |

### Step 3: Decompose Business Requirements into Stakeholder Requirements

For each business requirement, identify what each stakeholder group needs:

**Example:**

| Business Requirement | Stakeholder | Stakeholder Requirement |
|---------------------|-------------|------------------------|
| BR-042: Track equipment returns and calculate late fees | Operations Staff | STK-087: View overdue rentals on dashboard with calculated fees |
| BR-042: Track equipment returns and calculate late fees | Finance Team | STK-088: Generate late fee invoices automatically |
| BR-042: Track equipment returns and calculate late fees | Customers | STK-089: Receive notification of overdue status and fees |

### Step 4: Decompose Stakeholder Requirements into System Requirements

For each stakeholder requirement, define what the system must do:

**Example:**

| Stakeholder Requirement | System Requirement |
|------------------------|-------------------|
| STK-087: View overdue rentals on dashboard | SYS-134: Compare return dates against rental agreements and flag overdue items |
| STK-087: View overdue rentals on dashboard | SYS-135: Calculate late fee as [rate] x [days overdue] |
| STK-088: Generate late fee invoices | SYS-136: Generate invoice document with line items for late fees |

### Step 5: Decompose System Requirements into Software Requirements

For each system requirement, define specific software behavior:

**Example:**

| System Requirement | Software Requirement |
|-------------------|---------------------|
| SYS-134: Flag overdue items | SWR-201: API endpoint GET /rentals/overdue returns items past due date |
| SYS-134: Flag overdue items | SWR-202: Scheduled job runs daily at 06:00 to update overdue status |
| SYS-135: Calculate late fee | SWR-203: Late fee = daily_rate * 0.02 * days_overdue |
| SYS-135: Calculate late fee | SWR-204: Fees calculated in SAR, rounded to 2 decimal places |

### Step 6: Classify Each Requirement

For every SWR, assign:

| Attribute | Options |
|-----------|---------|
| Type | Functional / Non-Functional |
| NFR Category (if applicable) | Performance / Security / Usability / Reliability / Scalability / Maintainability / Compliance |
| Priority | Must Have / Should Have / Could Have / Won't Have |
| Risk | High / Medium / Low |
| Source | Stakeholder / Regulatory / Technical / Business |

Refer to [Requirements Classification Standard](../standards/requirements-classification.md).

### Step 7: Define Acceptance Criteria

Write acceptance criteria for each software requirement using Given/When/Then format:

```
Given: A rental agreement with return date 2026-03-01
  And: The equipment is not returned by 2026-03-04
  And: The daily rental rate is 100 SAR
When:  The overdue check job runs on 2026-03-04
Then:  The rental is flagged as overdue
  And: The late fee is calculated as 100 * 0.02 * 3 = 6.00 SAR
```

### Step 8: Establish Traceability Links

Update the Requirements Traceability Matrix:

| SWR ID | SYS ID | STK ID | BR ID |
|--------|--------|--------|-------|
| SWR-201 | SYS-134 | STK-087 | BR-042 |
| SWR-202 | SYS-134 | STK-087 | BR-042 |
| SWR-203 | SYS-135 | STK-087 | BR-042 |
| SWR-204 | SYS-135 | STK-087 | BR-042 |

Every SWR must trace back to at least one BR. Software requirements without a business requirement trace are candidates for removal.

### Step 9: Peer Review and Tech Lead Approval

1. Business Analyst reviews all requirements for completeness and consistency.
2. Tech Lead reviews for technical feasibility.
3. Resolve any issues identified.
4. Tech Lead approves and signs off.
5. Update all requirement statuses from Draft to Approved.

---

## Output Artifacts

- Software Requirements Specification (SRS) -- use [SRS Template](../templates/software-requirements-specification.md)
- Updated Requirements Traceability Matrix
- Peer review record

---

## Decomposition Example

```
BR-042: Track equipment returns and calculate late fees
  |
  +-- STK-087: Operations staff view overdue rentals on dashboard
  |     +-- SYS-134: Compare return dates and flag overdue items
  |     |     +-- SWR-201: GET /rentals/overdue API endpoint
  |     |     +-- SWR-202: Daily overdue check scheduled job
  |     +-- SYS-135: Calculate late fee
  |           +-- SWR-203: Fee calculation formula
  |           +-- SWR-204: Currency and rounding rules
  |
  +-- STK-088: Finance team gets auto-generated invoices
  |     +-- SYS-136: Generate invoice document
  |           +-- SWR-205: Invoice PDF generation service
  |           +-- SWR-206: Invoice data model and storage
  |
  +-- STK-089: Customers receive overdue notifications
        +-- SYS-137: Send notification to customer
              +-- SWR-207: Email notification with fee breakdown
              +-- SWR-208: SMS notification for overdue status
```

---

## Checklist

- [ ] All approved business requirements reviewed
- [ ] System boundaries and interfaces defined
- [ ] Business requirements decomposed into stakeholder requirements
- [ ] Stakeholder requirements decomposed into system requirements
- [ ] System requirements decomposed into software requirements
- [ ] Each requirement classified (type, priority, risk, source)
- [ ] Acceptance criteria defined for all software requirements
- [ ] Traceability matrix updated with all links
- [ ] Peer review completed by business analyst
- [ ] Tech lead review and sign-off obtained
