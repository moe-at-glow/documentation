# From Business Need to Software Requirement

End-to-end walkthrough showing how a business need transforms into software requirements at GlowPowerRental.

---

## The Example

**Business need:** "We need to track equipment rental returns and generate late fee invoices."

This need was raised by the Operations Manager during a quarterly review. Equipment is frequently returned late, and late fees are calculated manually using spreadsheets. This causes errors, delays in invoicing, and revenue leakage.

---

## Step 1: Business Need to Business Requirement

The Business Analyst works with the Product Owner to formalize the business need:

| Attribute | Value |
|-----------|-------|
| ID | BR-042 |
| Title | Automated Late Return Tracking and Fee Invoicing |
| Description | The business shall have an automated system to track equipment return dates, identify overdue rentals, calculate late fees, and generate invoices for those fees |
| Priority | Must Have |
| Source | Operations Manager (Quarterly Review Q4 2025) |
| Rationale | Manual tracking causes 15% of late fees to be uncollected. Automation reduces errors and accelerates revenue recovery. |
| Acceptance Criteria | Late returns are identified within 24 hours. Late fee invoices are generated automatically without manual intervention. |
| Status | Approved |

**Key principle:** Business requirements describe *what the business needs*, not how the system will implement it.

---

## Step 2: Business Requirement to Stakeholder Requirements

The Business Analyst identifies who interacts with this capability and what each group needs:

| ID | Stakeholder | Requirement | Priority |
|----|-------------|-------------|----------|
| STK-087 | Operations Staff | View all overdue rentals on a dashboard with rental details and calculated fees | Must Have |
| STK-088 | Finance Team | Receive auto-generated late fee invoices ready for distribution to customers | Must Have |
| STK-089 | Customers | Receive notification when rental is overdue with fee breakdown | Should Have |
| STK-090 | Management | View late return trends and total late fee revenue in reports | Could Have |

**Key principle:** Each stakeholder group gets requirements that describe what *they* need from the system, from their perspective.

---

## Step 3: Stakeholder Requirements to System Requirements

The Business Analyst and Tech Lead define what the system must do to satisfy each stakeholder need:

| STK ID | System Requirement ID | System Requirement |
|--------|----------------------|-------------------|
| STK-087 | SYS-134 | The system shall compare equipment return dates against rental agreement end dates and flag items not returned by the end date |
| STK-087 | SYS-135 | The system shall calculate late fees using the formula: daily_rental_rate x fee_percentage x days_overdue |
| STK-088 | SYS-136 | The system shall generate an invoice document containing rental details, overdue period, fee calculation, and total amount |
| STK-089 | SYS-137 | The system shall send notifications to customers when their rental becomes overdue |
| STK-090 | SYS-138 | The system shall aggregate late return data for reporting by time period, equipment type, and customer |

**Key principle:** System requirements describe *what the system does*, independent of specific technology choices.

---

## Step 4: System Requirements to Software Requirements

The Tech Lead and developers define specific software behavior:

### From SYS-134 (Flag overdue items):

| ID | Software Requirement | Acceptance Criteria |
|----|---------------------|-------------------|
| SWR-201 | The API shall expose GET /api/v1/rentals/overdue returning all rental agreements past their return date with rental details and calculated fees | Given 3 overdue rentals exist, when GET /api/v1/rentals/overdue is called, then response contains 3 items with rental_id, customer_name, due_date, days_overdue, and calculated_fee |
| SWR-202 | A scheduled job shall run daily at 06:00 AST to scan all active rentals and update overdue status | Given a rental with return date 2026-03-01 and today is 2026-03-02, when the job runs, then the rental status is updated to "overdue" |

### From SYS-135 (Calculate late fee):

| ID | Software Requirement | Acceptance Criteria |
|----|---------------------|-------------------|
| SWR-203 | Late fee shall be calculated as: daily_rental_rate x 0.02 x days_overdue | Given daily rate 100 SAR and 3 days overdue, when fee is calculated, then fee equals 6.00 SAR |
| SWR-204 | All fee amounts shall be in SAR, rounded to 2 decimal places using banker's rounding | Given a calculated fee of 7.125 SAR, when rounding is applied, then the result is 7.12 SAR |

### From SYS-136 (Generate invoice):

| ID | Software Requirement | Acceptance Criteria |
|----|---------------------|-------------------|
| SWR-205 | The system shall generate a PDF invoice containing: company header, customer details, rental agreement number, equipment description, rental period, overdue days, fee calculation, total amount, payment terms | Given overdue rental data, when invoice is generated, then a PDF is created with all required fields populated |
| SWR-206 | Invoice records shall be stored with: invoice_id, rental_id, customer_id, amount, currency, generated_date, status (draft/sent/paid) | Given a generated invoice, when stored, then all fields are persisted and retrievable by invoice_id |

### From SYS-137 (Customer notification):

| ID | Software Requirement | Acceptance Criteria |
|----|---------------------|-------------------|
| SWR-207 | An email notification shall be sent to the customer's registered email containing: rental reference, equipment name, due date, days overdue, current fee amount, payment instructions | Given an overdue rental with customer email on file, when notification is triggered, then email is sent within 1 hour |
| SWR-208 | An SMS notification shall be sent to the customer's registered phone number containing: rental reference, days overdue, fee amount, contact number for inquiries | Given an overdue rental with customer phone on file, when notification is triggered, then SMS is sent within 1 hour |

---

## The Complete Traceability Chain

```
BR-042: Track returns and generate late fee invoices
|
+-- STK-087: Ops staff view overdue rentals on dashboard
|   +-- SYS-134: Compare dates and flag overdue
|   |   +-- SWR-201: GET /api/v1/rentals/overdue endpoint
|   |   +-- SWR-202: Daily overdue check job (06:00 AST)
|   +-- SYS-135: Calculate late fee
|       +-- SWR-203: Fee = daily_rate x 0.02 x days_overdue
|       +-- SWR-204: SAR currency, 2 decimal places
|
+-- STK-088: Finance gets auto-generated invoices
|   +-- SYS-136: Generate invoice document
|       +-- SWR-205: PDF invoice generation
|       +-- SWR-206: Invoice data model and storage
|
+-- STK-089: Customers receive overdue notification
|   +-- SYS-137: Send notification to customer
|       +-- SWR-207: Email notification
|       +-- SWR-208: SMS notification
|
+-- STK-090: Management views late return reports
    +-- SYS-138: Aggregate data for reporting
        +-- (SWRs defined during that decomposition)
```

One business requirement produced 4 stakeholder requirements, 5 system requirements, and 8+ software requirements.

---

## What Gets Lost When You Skip Levels

### Skipping Stakeholder Requirements (BR directly to SYS)

- You miss STK-089 (customer notification) because Operations and Finance are obvious stakeholders but customers are not consulted.
- You miss STK-090 (management reporting) because the original request focused on operational tracking.

### Skipping System Requirements (STK directly to SWR)

- You jump to implementation details without defining system behavior.
- SWR-204 (currency rounding) gets missed because nobody thought about edge cases at the stakeholder level.
- Integration requirements between components are not identified.

### Skipping Software Requirements (SYS directly to code)

- Developers make assumptions about acceptance criteria.
- "Calculate late fee" is implemented differently by different developers.
- QA has no specification to test against.

---

## Common Decomposition Mistakes

| Mistake | Example | Fix |
|---------|---------|-----|
| Combining levels | "The dashboard shall show overdue rentals with fees calculated at 2% daily" mixes stakeholder need with calculation logic | Separate: STK defines what user sees, SWR defines calculation |
| Specifying technology in business requirements | "BR-042: The system shall use PostgreSQL to track returns" | BR describes business need, not technology. Move to SWR. |
| One-to-one decomposition | Every BR maps to exactly one SWR | Genuine decomposition produces multiple lower-level requirements per parent |
| Missing non-functional requirements | No performance, security, or reliability requirements defined | Add NFRs: "SWR-209: Overdue check job completes within 5 minutes for 10,000 active rentals" |
| Orphan requirements | SWR exists with no parent requirement | Every SWR must trace to a SYS, which traces to a STK, which traces to a BR |
