# Write System Tests

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P6-003 |
| **Owner** | QA Lead |
| **Accountable** | QA Lead |
| **SLA** | 3-5 business days per release |
| **Escalation** | Tech Lead (technical issues), Business Analyst (requirements clarification) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Feature deployed to staging environment
- [ ] API specification and acceptance criteria available
- [ ] Test data loaded in staging
- [ ] Test accounts with appropriate roles available
- [ ] System testing standard reviewed: [system-testing-standard.md](../standards/system-testing-standard.md)

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Staging environment unavailable or unstable | STOP. Raise infra ticket | Tech Lead |
| Acceptance criteria missing or ambiguous | STOP. Clarify with Business Analyst before writing tests | Business Analyst |
| Test accounts not provisioned | STOP. Request account provisioning | Tech Lead |
| Test data missing or corrupted in staging | STOP. Reset staging data | Tech Lead |

---

## PROCEDURE

### Step 1: Identify Critical User Journeys

| Action | Owner | SLA |
|--------|-------|-----|
| Map user journeys from requirements to SRS requirement IDs | QA Lead | 2 hours |

| Journey | Steps | SRS Requirements |
|---------|-------|-----------------|
| Create and manage rental | Login > Browse equipment > Create rental > View rental | SWR-101, SWR-102, SWR-103 |
| Process overdue rental | Rental becomes overdue > Late fee calculated > Invoice generated > Payment | SWR-201, SWR-203, SWR-204 |
| Equipment lifecycle | Add equipment > Assign to rental > Track usage > Return > Maintenance | SWR-301, SWR-302 |

- [ ] All critical user journeys identified
- [ ] Each journey mapped to SRS requirements

> **IF** requirements incomplete or conflicting **THEN** escalate to Business Analyst for clarification
> **ELSE** proceed to Step 2

### Step 2: Write Test Cases

| Action | Owner | SLA |
|--------|-------|-----|
| Write test cases using [Test Case Template](../templates/test-case-template.md) | QA Lead | 4 hours |

For each test case, include:

- [ ] Test ID assigned (format: `SYS-TC-XXX`)
- [ ] Title is specific and descriptive
- [ ] Priority assigned (Critical / High / Medium / Low)
- [ ] Preconditions listed
- [ ] Steps numbered with exact API calls or actions
- [ ] Expected result defined for each step
- [ ] Cleanup procedure documented

> **IF** test case depends on another test case **THEN** document dependency and ensure execution order
> **ELSE** ensure test case is independently executable

### Step 3: Organize Test Cases by Priority

| Action | Owner | SLA |
|--------|-------|-----|
| Assign priority to each test case and organize execution order | QA Lead | 1 hour |

| Priority | Coverage Target |
|----------|----------------|
| Critical | 100% executed every test cycle |
| High | 100% executed every test cycle |
| Medium | Executed for release cycles |
| Low | Executed quarterly or on-demand |

- [ ] All test cases prioritized
- [ ] Execution order documented

### Step 4: Write Automated System Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Create automated tests for critical journeys in `tests/system/<journey>.system.test.ts` | QA Lead | 1 day |

- [ ] Automated tests authenticate via API (no direct DB access)
- [ ] Automated tests use staging URL from environment variable
- [ ] Automated tests create their own test data via API
- [ ] Automated tests clean up after execution in `afterAll`
- [ ] All critical journeys have automated coverage

> **IF** journey cannot be fully automated **THEN** automate what is possible, document manual steps separately
> **ELSE** proceed to Step 5

### Step 5: Execute Manual Test Cases

| Action | Owner | SLA |
|--------|-------|-----|
| Open test plan and execute each manual test case in priority order | QA Lead | 4-8 hours |

For each test case:

- [ ] Preconditions verified
- [ ] Each step executed in order
- [ ] Actual result recorded next to each step
- [ ] Actual vs. expected compared

> **IF** Pass **THEN** mark as Pass, move to next test
> **ELSE IF** Fail **THEN** capture screenshot/API response, log defect using [Defect Report Template](../templates/defect-report-template.md), link defect to test case, continue testing
> **ELSE IF** Blocked **THEN** document blocker, move to next test, revisit when unblocked

### Step 6: Handle Test Failures

| Action | Owner | SLA |
|--------|-------|-----|
| Log defects for all failures | QA Lead | 30 min per defect |
| Link defects to test cases | QA Lead | Continuous |

| Result | Action |
|--------|--------|
| Pass | Mark as passed. Move to next test. |
| Fail | Log defect. Continue testing other test cases. |
| Blocked | Document the blocker. Move to next test. Revisit when unblocked. |

- [ ] All failures logged as defects
- [ ] All defects linked to originating test cases

> **IF** single failure blocks multiple other tests **THEN** escalate to Tech Lead for priority fix
> **ELSE** continue executing remaining test cases

### Step 7: Clean Up Test Data

| Action | Owner | SLA |
|--------|-------|-----|
| Delete test data created during testing via API | QA Lead | 1 hour |
| Reset modified records to original state | QA Lead | 30 min |
| Verify staging environment is clean | QA Lead | 15 min |

- [ ] All test-created data deleted
- [ ] Modified records restored
- [ ] Staging environment verified clean for next cycle

> **IF** cleanup cannot be completed via API **THEN** request DB reset from Tech Lead
> **ELSE** procedure complete

---

## EXIT CRITERIA

- [ ] Critical user journeys identified and mapped to requirements
- [ ] Test cases written with clear steps and expected results
- [ ] Test cases prioritized (Critical > High > Medium > Low)
- [ ] Automated system tests created for critical journeys
- [ ] Manual test cases documented
- [ ] Test data strategy defined (API-driven, no direct DB access)
- [ ] Cleanup procedures documented and executed
- [ ] All failures logged as defects

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| System test cases | [test-case-template.md](../templates/test-case-template.md) | Project tracker |
| Automated system tests | `tests/system/<journey>.system.test.ts` | Source repository |
| Defect reports (from failures) | [defect-report-template.md](../templates/defect-report-template.md) | Project tracker |
| Test execution results | Per test plan | Project tracker |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| System Testing Standard | Standard | [../standards/system-testing-standard.md](../standards/system-testing-standard.md) |
| Testing Strategy Standard | Standard | [../standards/testing-strategy-standard.md](../standards/testing-strategy-standard.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
