# Test Case Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-002 |
| **When to Use** | Documenting individual test cases for any test level |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 1 business day per test case |
| **Runbook** | [Write Integration Tests](../runbooks/write-integration-tests.md), [Write System Tests](../runbooks/write-system-tests.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Factor | Simple (1-3 steps) | Standard (4-8 steps) | Complex (> 8 steps) |
|--------|---------------------|----------------------|----------------------|
| Step detail | Action + expected result | Action + input + expected result | Action + input + expected result + evidence |
| Preconditions | Inline list | Numbered list | Numbered list + setup script reference |
| Cleanup | Manual note | Numbered steps | Automated teardown script reference |
| Review required | Self-review | Peer review | Peer review + QA Lead sign-off |

---

## [ ] Test Case

| Field | Value |
|-------|-------|
| **Test Case ID** | <!-- TC-NNN or SYS-TC-NNN --> |
| **Title** | <!-- Clear description of what is being tested --> |
| **Test Level** | <!-- Unit / Integration / System / UAT --> |
| **Test Type** | <!-- Functional / Regression / Performance / Security --> |
| **Priority** | <!-- Critical / High / Medium / Low --> |
| **Requirement** | <!-- SWR-NNN --> |
| **Module** | <!-- Rentals / Billing / Equipment / Auth / etc. --> |
| **Author** | <!-- Name --> |
| **Date Created** | <!-- YYYY-MM-DD --> |

---

## [ ] Preconditions

1. <!-- Precondition 1 (e.g., "Customer account exists with email test@example.com") -->
2. <!-- Precondition 2 (e.g., "Equipment SP-100 exists with status 'available'") -->
3. <!-- Precondition 3 (e.g., "User is authenticated with valid JWT token") -->

---

## [ ] Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | <!-- What to do --> | <!-- What data to use --> | <!-- What should happen --> |
| 2 | <!-- --> | <!-- --> | <!-- --> |
| 3 | <!-- --> | <!-- --> | <!-- --> |
| 4 | <!-- --> | <!-- --> | <!-- --> |
| 5 | <!-- --> | <!-- --> | <!-- --> |

---

## [ ] Expected Result

<!-- Overall expected outcome when all steps are completed successfully -->

---

## [ ] Postconditions / Cleanup

1. <!-- Postcondition 1 (e.g., "Created rental is deleted") -->
2. <!-- Postcondition 2 (e.g., "Equipment status reset to 'available'") -->

---

## [ ] Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | <!-- YYYY-MM-DD --> | <!-- Name --> | <!-- staging --> | <!-- Pass / Fail / Blocked --> | <!-- DEF-NNN or N/A --> |
| Run 2 | <!-- --> | <!-- --> | <!-- --> | <!-- --> | <!-- --> |

### [ ] Actual Results (if different from expected)

<!-- Describe what actually happened if the test failed -->

### [ ] Notes

<!-- Any additional observations during execution -->

---

## [ ] Example: Completed Test Case

| Field | Value |
|-------|-------|
| **Test Case ID** | SYS-TC-001 |
| **Title** | Customer creates a rental for available equipment |
| **Test Level** | System |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-101, SWR-102 |
| **Module** | Rentals |
| **Author** | Sara |
| **Date Created** | 2026-03-01 |

### Preconditions

1. Customer account exists (test@example.com / test-password)
2. Equipment "Solar Panel SP-100" (eq-test-001) exists with status "available"
3. Staging environment is deployed and healthy

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST /api/v1/auth/login | `{ "email": "test@example.com", "password": "test-password" }` | 200 with JWT token |
| 2 | GET /api/v1/equipment?status=available | Auth header with token from step 1 | 200 with list containing eq-test-001 |
| 3 | POST /api/v1/rentals | `{ "customer_id": "{from login}", "equipment_id": "eq-test-001", "start_date": "2026-04-01", "end_date": "2026-04-30" }` | 201 with rental data, status = "pending" |
| 4 | GET /api/v1/rentals/{id from step 3} | Auth header | 200 with rental details, status = "pending" |
| 5 | GET /api/v1/equipment/eq-test-001 | Auth header | 200 with status = "reserved" |

### Expected Result

Rental created successfully. Equipment status changed to "reserved". Rental visible in customer's rental list.

### Postconditions / Cleanup

1. DELETE /api/v1/rentals/{id} to remove test rental
2. Reset equipment eq-test-001 status to "available"

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-03-02 | Sara | staging | Pass | N/A |

---

## Completion Checklist

- [ ] Test Case ID assigned following naming convention
- [ ] Title clearly describes what is being tested
- [ ] Test level and type specified
- [ ] Priority assigned
- [ ] Requirement traceability linked (SWR-NNN)
- [ ] Preconditions documented
- [ ] Test steps written with actions, inputs, and expected results
- [ ] Overall expected result stated
- [ ] Postconditions / cleanup steps defined
- [ ] Test execution record section ready for use

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Write Integration Tests | [../runbooks/write-integration-tests.md](../runbooks/write-integration-tests.md) |
| Runbook | Write System Tests | [../runbooks/write-system-tests.md](../runbooks/write-system-tests.md) |
| Template | Test Plan Template | [test-plan-template.md](test-plan-template.md) |
| Template | Defect Report Template | [defect-report-template.md](defect-report-template.md) |
| Template | Test Summary Report Template | [test-summary-report-template.md](test-summary-report-template.md) |
