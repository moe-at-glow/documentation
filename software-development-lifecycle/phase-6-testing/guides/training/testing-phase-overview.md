# Testing Phase Overview

How the Testing phase fits into the GlowPowerRental SDLC and what it produces.

---

## Purpose

The Testing phase verifies that the software built in Phase 5 meets the requirements defined in Phase 2, follows the architecture from Phase 3, and matches the detailed designs from Phase 4. Testing provides the evidence needed to approve a release.

**Input:** Working code on `develop` with passing unit tests (Phase 5 exit).

**Output:** Tested software with test reports, resolved defects, and sign-off for deployment (Phase 7 entry).

---

## Where Testing Fits

```
Phase 2           Phase 4          Phase 5           Phase 6            Phase 7
Requirements --> Design --> Development --> [TESTING] --> Deployment
     SRS           DDD        Source Code     Test Reports    Release
     RTM           API Spec   Unit Tests      Defect Log      Package
                              PR History      Sign-Off
```

Testing validates against requirements (Phase 2) and design (Phase 4), not against the code itself. The question is not "does the code work?" but "does the code do what the business needs?"

---

## Key Principles

### 1. Test Early, Test Often

Testing is not a phase you do once at the end. It happens continuously:

| When | What | Who |
|------|------|-----|
| During development (Phase 5) | Unit tests (TDD) | Developer |
| After merge to develop | Integration tests (CI) | Automated |
| Per sprint | System tests | QA Engineer |
| Before release | Full regression + performance + security | QA Team |
| After deployment | Smoke tests | Automated |

### 2. Requirements-Based Testing

Every test case traces back to a requirement:

```
BR-042 (Business Requirement)
  └── SWR-203 (Software Requirement)
        └── SYS-TC-015 (System Test Case)
              └── Result: Pass/Fail
```

If a test cannot be linked to a requirement, question whether it is needed. If a requirement has no test, the requirement is not verified.

### 3. Risk-Based Priority

Not all tests are equal. Focus testing effort where the risk is highest:

| Risk Factor | Testing Effort |
|-------------|---------------|
| Financial operations (payments, fees) | Maximum: unit + integration + system + performance |
| Security (auth, data access) | Maximum: unit + integration + security tests |
| Core workflows (rental lifecycle) | High: unit + integration + system |
| Supporting features (reports, exports) | Moderate: unit + integration |
| Cosmetic (formatting, alignment) | Low: manual check |

### 4. Independent Verification

The person who wrote the code should not be the only person who tests it:

| Role | Testing Responsibility |
|------|----------------------|
| Developer | Unit tests, self-review, integration tests |
| Peer Developer | Code review (Phase 5) |
| QA Engineer | System tests, regression, defect reporting |
| Product Owner | UAT, acceptance criteria verification |

---

## Test Levels Summary

```
            ┌──────────────────────┐
            │   Acceptance (UAT)   │  Business validates requirements
            │   Few tests, manual  │
            ├──────────────────────┤
            │    System Tests      │  Complete user workflows
            │   Staging env        │
            ├──────────────────────┤
            │  Integration Tests   │  Components working together
            │   Test database      │
            ├──────────────────────┤
            │    Unit Tests        │  Individual functions
            │   In-memory, fast    │
            └──────────────────────┘
```

| Level | Count | Speed | Cost | Catches |
|-------|-------|-------|------|---------|
| Unit | Hundreds | Milliseconds | Low | Logic errors, edge cases |
| Integration | Dozens | Seconds | Medium | API errors, data flow issues, auth gaps |
| System | Tens | Minutes | High | Workflow breaks, cross-module issues |
| UAT | Few | Hours | Highest | Requirement misunderstandings |

---

## Artifacts Produced

| Artifact | Description | Template |
|----------|-------------|----------|
| Test Plan | What will be tested, by whom, with what data | [Test Plan Template](../../templates/test-plan-template.md) |
| Test Cases | Individual test scenarios with steps and expected results | [Test Case Template](../../templates/test-case-template.md) |
| Defect Reports | Issues found during testing | [Defect Report Template](../../templates/defect-report-template.md) |
| Test Summary Report | Results, metrics, and go/no-go recommendation | [Test Summary Report Template](../../templates/test-summary-report-template.md) |
| UAT Sign-Off | Business acceptance of the tested software | [UAT Sign-Off Template](../../templates/uat-sign-off-template.md) |

---

## Roles and Responsibilities

| Role | Responsibility |
|------|---------------|
| QA Engineer | Writes and executes test cases, reports defects, writes test reports |
| QA Lead | Approves test plans, triages defects, signs off on testing |
| Developer | Fixes defects, writes unit/integration tests |
| Tech Lead | Triages defects, approves risk acceptance for medium/low defects |
| Product Owner | Verifies acceptance criteria, provides UAT sign-off |
| Business Analyst | Clarifies requirements during testing, reviews test coverage |

---

## Common Mistakes

| Mistake | Why It Happens | How to Avoid |
|---------|---------------|--------------|
| Testing only the happy path | Time pressure | Write test cases from requirements, which include error scenarios |
| No traceability to requirements | Tests written ad-hoc | Link every test case to an SWR requirement |
| Testing in development environment | "It works on my machine" | Use staging with production-like config |
| Skipping regression tests | "We only changed one thing" | Always run at least core regression |
| Not logging defects formally | "I'll just tell the developer" | Every defect gets a formal report. Verbal reports get lost. |
| Accepting flaky tests | "It usually passes" | Flaky tests are bugs. Fix them. |

---

## Phase Exit Criteria

Testing is complete when:

- [ ] All planned test cases executed
- [ ] All critical and high severity defects resolved
- [ ] Regression tests pass
- [ ] Performance benchmarks met (for releases)
- [ ] Security scan clean (for releases)
- [ ] Test summary report written and approved by QA Lead
- [ ] UAT sign-off obtained (for releases)
- [ ] No known critical or high severity defects remain open
