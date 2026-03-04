# Defect Report Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-003 |
| **When to Use** | Reporting bugs found during any testing phase |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 4 hours for Critical/High, 1 business day for Medium/Low |
| **Runbook** | [Report and Track Defects](../runbooks/report-and-track-defects.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Factor | Minor (Low/Medium) | Major (High) | Blocker (Critical) |
|--------|---------------------|--------------|---------------------|
| Evidence required | Description + steps | Description + steps + API logs | Description + steps + API logs + screenshots |
| Reproduction detail | Summary steps | Exact steps with data | Exact steps + reproduction rate + env details |
| Impact analysis | One-liner | Affected users/workflows | Business impact + revenue/SLA implications |
| Escalation | Standard triage | Notify Tech Lead | Immediate escalation to Tech Lead + PO |

---

## [ ] Defect Information

| Field | Value |
|-------|-------|
| **Defect ID** | <!-- DEF-NNN --> |
| **Title** | <!-- Clear, specific summary --> |
| **Severity** | <!-- Critical / High / Medium / Low --> |
| **Priority** | <!-- Urgent / High / Medium / Low --> |
| **Status** | <!-- New / Triaged / Assigned / In Progress / Fixed / Re-test / Closed / Reopened --> |
| **Reporter** | <!-- Name --> |
| **Date Reported** | <!-- YYYY-MM-DD --> |
| **Assigned To** | <!-- Developer name (filled during triage) --> |
| **Module** | <!-- Rentals / Billing / Equipment / Auth / etc. --> |
| **Environment** | <!-- Local / Test / Staging / Production --> |
| **Version / Branch** | <!-- Branch name or version number --> |
| **Related Ticket** | <!-- TICKET-NNN (if related to a feature) --> |
| **Related Test Case** | <!-- TC-NNN (if found during test execution) --> |

---

## [ ] Description

<!-- What is the defect? One or two sentences describing the problem. -->

---

## [ ] Steps to Reproduce

1. <!-- Step 1 -->
2. <!-- Step 2 -->
3. <!-- Step 3 -->
4. <!-- Step 4 -->

**Reproduction rate:** <!-- Always / Intermittent (X out of Y attempts) -->

---

## [ ] Expected Result

<!-- What should have happened? -->

---

## [ ] Actual Result

<!-- What actually happened? -->

---

## [ ] Evidence

### [ ] API Request (if applicable)

```http
<!-- Method URL -->
<!-- Headers -->

<!-- Request body -->
```

### [ ] API Response (if applicable)

```json
<!-- Response body -->
```

### [ ] Screenshot(s)

<!-- Attach screenshots or describe what was seen -->

### [ ] Error Logs (if applicable)

```
<!-- Relevant log entries -->
```

---

## [ ] Impact

<!-- What is the business impact of this defect? Who is affected? -->

---

## [ ] Workaround

<!-- Is there a workaround? Describe it. If none, write "None." -->

---

## [ ] Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | <!-- Name --> |
| **Fix Date** | <!-- YYYY-MM-DD --> |
| **Fix Description** | <!-- What was changed to fix the issue --> |
| **Fix Commit** | <!-- Commit hash or PR link --> |

---

## [ ] Verification

| Field | Value |
|-------|-------|
| **Verified By** | <!-- Name --> |
| **Verification Date** | <!-- YYYY-MM-DD --> |
| **Verification Result** | <!-- Passed / Failed --> |
| **Regression Check** | <!-- Passed / Failed / Not Applicable --> |
| **Notes** | <!-- Any observations during verification --> |

---

## [ ] Example: Completed Defect Report

| Field | Value |
|-------|-------|
| **Defect ID** | DEF-042 |
| **Title** | Late fee calculation returns 0 when equipment daily rate has fractional cents (e.g., 99.995 SAR) |
| **Severity** | High |
| **Priority** | High |
| **Status** | Closed |
| **Reporter** | Sara (QA) |
| **Date Reported** | 2026-03-01 |
| **Assigned To** | Ali (Developer) |
| **Module** | Billing |
| **Environment** | Staging |
| **Version / Branch** | develop (commit abc1234) |
| **Related Ticket** | TICKET-123 |
| **Related Test Case** | SYS-TC-015 |

### Description

The late fee calculator returns 0 SAR when the equipment daily rate has more than 2 decimal places. The rounding logic truncates the rate to 0 before multiplication.

### Steps to Reproduce

1. Login as admin
2. Create equipment with daily rate 99.995 SAR
3. Create a rental with this equipment, set end date to yesterday
4. POST /api/v1/rentals/{id}/calculate-late-fee
5. Observe the returned fee amount

**Reproduction rate:** Always

### Expected Result

Late fee = 99.995 * 0.02 * 1 = 2.00 SAR (rounded to 2 decimal places)

### Actual Result

Late fee = 0.00 SAR

### API Response

```json
{
  "data": {
    "rental_id": "ra-test-001",
    "late_fee": {
      "amount": 0.00,
      "currency": "SAR"
    }
  }
}
```

### Impact

Customers with equipment that has fractional daily rates are not being charged late fees. Financial impact: approximately 15% of equipment has fractional rates.

### Workaround

Manually adjust equipment daily rates to exactly 2 decimal places before calculating late fees.

### Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | Ali |
| **Fix Date** | 2026-03-02 |
| **Fix Description** | Changed rounding to occur after multiplication, not before. Used banker's rounding (Math.round) on the final result. |
| **Fix Commit** | fix(billing): correct rounding order in late fee calculation (def5678) |

### Verification

| Field | Value |
|-------|-------|
| **Verified By** | Sara |
| **Verification Date** | 2026-03-02 |
| **Verification Result** | Passed |
| **Regression Check** | Passed (all billing tests pass) |
| **Notes** | Verified with rates: 99.995, 0.005, 100.00, 0.01. All produce correct results. |

---

## Completion Checklist

- [ ] Defect ID assigned following naming convention
- [ ] Title is clear and specific
- [ ] Severity and priority assessed
- [ ] Steps to reproduce are exact and repeatable
- [ ] Expected and actual results documented
- [ ] Evidence attached (API logs, screenshots, error logs as applicable)
- [ ] Impact described with affected scope
- [ ] Workaround documented (or "None" stated)
- [ ] Related ticket and test case linked
- [ ] Resolution section completed after fix
- [ ] Verification section completed after re-test

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Report and Track Defects | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Template | Test Case Template | [test-case-template.md](test-case-template.md) |
| Template | Test Plan Template | [test-plan-template.md](test-plan-template.md) |
| Template | Test Summary Report Template | [test-summary-report-template.md](test-summary-report-template.md) |
