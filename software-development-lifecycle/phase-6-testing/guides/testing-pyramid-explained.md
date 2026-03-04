# Testing Pyramid -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P6-001 |
| **Use When** | Deciding which test level to write for a feature or bug fix |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Most tests are at the unit level (not integration or system)
- [ ] No edge-case logic is tested only at the system/E2E level
- [ ] Unit test suite runs in < 30 seconds
- [ ] Integration test suite runs in < 5 minutes
- [ ] No calculation or validation logic tested exclusively through system tests
- [ ] No manual-only test coverage for automatable scenarios

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Testing a single function or class in isolation | Unit test | Using a real database or API call |
| Testing business logic / calculations | Unit test with multiple edge cases | Writing one system test instead |
| Testing API endpoint + service + database together | Integration test | Testing every edge case at this level |
| Testing authentication / authorization enforcement | Integration test | Relying only on unit-level mock checks |
| Testing database constraints (unique, FK, not null) | Integration test | Mocking the database |
| Testing a multi-step business workflow | System test (staging) | Duplicating logic already covered by unit tests |
| Testing cross-module interactions | System test | Testing individual function logic at this level |
| External service integration (payment, email) | System test in staging | Calling external services in unit/integration tests |
| Test suite is slow (10+ min) | Push tests down the pyramid; minimize data | Adding more system tests |
| Many system tests for one feature | Refactor: move edge cases to unit tests | Leaving the ice cream cone anti-pattern in place |

---

## QUICK-REFERENCE TABLE

### Test Level Characteristics

| Level | Speed | Reliability | Maintenance Cost | Catches |
|-------|-------|-------------|-----------------|----------------|
| Unit | Milliseconds | Very high (deterministic) | Low | Logic errors, edge cases, calculation bugs |
| Integration | Seconds | High | Medium | API contract issues, data flow, auth gaps |
| System/E2E | Minutes | Lower (more moving parts) | High | Workflow breaks, cross-module issues |

### Target Distribution

| Level | Quantity | Total Time |
|-------|----------|------------|
| Unit | ~200-500 tests | < 30 seconds |
| Integration | ~50-100 tests | < 5 minutes |
| System | ~20-30 tests | < 30 minutes |

### Where Should This Test Go?

| Question | If Yes | If No |
|----------|--------|-------|
| Can I test this with just the function/class? | Unit test | Continue below |
| Does it need a real database or API? | Integration test | Continue below |
| Does it span multiple modules or API calls? | System test | Unit or integration |
| Does it need external services (payment, email)? | System test (staging) | Integration test with mocks |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/testing-phase-overview.md](training/testing-phase-overview.md) |
| Test data setup | Quick Reference | [test-data-management-guide.md](test-data-management-guide.md) |
| Common pitfalls | Quick Reference | [common-testing-pitfalls.md](common-testing-pitfalls.md) |
