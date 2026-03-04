> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Pull Request #42

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P5-001 |
| **Project** | Power Atlas -- GlowPowerRental |
| **Repository** | github.com/glowpowerrental/power-atlas |
| **Author** | Layla Haddad (Developer) |
| **Reviewer** | Mohammad Al-Farsi (Tech Lead) |
| **Date Submitted** | 2026-02-18 |
| **Branch** | `feature/power-calculation-engine` |
| **Base Branch** | `develop` |
| **Last Verified** | 2026-03-05 |

---

## Scaling Decision Gate

| PR Size | Action |
|---------|--------|
| **< 100 lines** | Single reviewer, fast-track |
| **100-400 lines** | Standard review, one reviewer minimum |
| **400-800 lines** | Two reviewers required, split if possible |
| **> 800 lines** | STOP. Split into smaller PRs before submitting |

**This PR: ~320 lines changed -- Standard review, one reviewer minimum.**

---

## [x] PR Title

```
feat(calc): implement power calculation engine with unit conversions
```

---

## [x] Description

### [x] What

Implements the `PowerCalculator` class providing single-phase power calculation, three-phase power calculation, and bidirectional kW-to-kVA / kVA-to-kW conversions with configurable power factor. Includes both the frontend JavaScript module and a mirrored Python API endpoint for server-side validation.

### [x] Why

The power calculation engine is the core computation layer for Power Atlas. Every project estimate, generator recommendation, and load summary depends on accurate power math. Without this module, no downstream feature (load scheduling, generator sizing, distribution planning) can function.

Refs: SWR-CALC-001, SWR-CALC-002, SWR-CALC-003, SWR-CALC-004, SWR-CALC-005, SWR-CALC-006

### [x] How

- Created a stateless `PowerCalculator` class in `power-calculations.js` with pure functions for each formula. All conversions use IEEE-standard formulas with sqrt(3) for three-phase calculations.
- Power factor defaults to 0.8 (industry standard for mixed resistive/inductive event loads) but is configurable per call.
- Mirrored the calculation logic in `server/api/calculations.py` so the backend can independently validate client-submitted values before persisting.
- All inputs are validated: negative values, zero values, NaN, and non-numeric types throw descriptive errors.

---

## [x] Changes

### Frontend -- `src/modules/power-calculations.js` (new file, +142 lines)

- [x] `PowerCalculator` class with static methods
- [x] `singlePhase(voltage, current, powerFactor)` -- returns watts
- [x] `threePhase(voltage, current, powerFactor)` -- returns watts using V * I * sqrt(3) * PF
- [x] `kWToKVA(kw, powerFactor)` -- converts kilowatts to kilovolt-amps
- [x] `kVAToKW(kva, powerFactor)` -- converts kilovolt-amps to kilowatts
- [x] `totalLoad(loads[])` -- sums an array of load objects, returns aggregate kW and kVA
- [x] Input validation on all public methods (throws `PowerCalculationError` for invalid inputs)

### Frontend Tests -- `test/power-calculations.test.js` (new file, +98 lines)

- [x] Unit tests for `singlePhase` with known voltage/current/PF combinations
- [x] Unit tests for `threePhase` with standard 208V and 480V three-phase scenarios
- [x] Unit tests for `kWToKVA` and `kVAToKW` round-trip consistency
- [x] Edge case tests: zero voltage, zero current, power factor of 0, power factor of 1
- [x] Error tests: negative values throw `PowerCalculationError`, NaN inputs throw, string inputs throw
- [x] Large load tests: values up to 10 MW to verify no overflow or precision loss

### Backend -- `server/api/calculations.py` (new file, +52 lines)

- [x] `POST /api/calculations/single-phase` endpoint
- [x] `POST /api/calculations/three-phase` endpoint
- [x] `POST /api/calculations/convert` endpoint (kW/kVA bidirectional)
- [x] Input validation using Flask request JSON schema
- [x] JWT authentication required on all endpoints

### Backend Tests -- `test/test_calculations.py` (new file, +28 lines)

- [x] Parameterized tests mirroring frontend test cases
- [x] Tests for unauthenticated access (401 response)
- [x] Tests for malformed JSON payloads (400 response)

---

## [x] Related Documents

- DDD: `docs/design/power-calculation-ddd.md` (Detailed Design Document for calculation module)
- API Spec: `docs/api/calculations-api.yaml` (OpenAPI spec for calculation endpoints)
- ADR: `docs/adr/ADR-003-stateless-calculator.md` (Decision to use stateless pure functions over class instances)

---

## [x] Test Plan

### [x] Automated Tests

- [x] Unit tests for all five calculator functions with known-good input/output pairs
- [x] Edge case tests for zero values, boundary values, and maximum expected load sizes
- [x] Error handling tests for negative values, NaN, undefined, string inputs
- [x] Round-trip tests: kWToKVA then kVAToKW returns original value (within floating-point tolerance)
- [x] Backend endpoint tests: valid requests return correct JSON, invalid requests return 400, unauthenticated requests return 401

### [x] Manual Testing

1. Start the development server: `npm run dev` and `flask run`
2. Open the browser console on the Power Atlas dashboard
3. Run `PowerCalculator.singlePhase(120, 15, 0.8)` -- expect `1440` (watts)
4. Run `PowerCalculator.threePhase(480, 100, 0.85)` -- expect `70692.2` (watts, approx)
5. Run `PowerCalculator.kWToKVA(50, 0.8)` -- expect `62.5`
6. Verify: all results match hand-calculated values using standard electrical formulas

### [x] Test Results

```
$ npm test -- power-calculations

 PASS  test/power-calculations.test.js
  PowerCalculator
    singlePhase
      ✓ calculates single-phase power for 120V 15A PF=0.8 (1 ms)
      ✓ calculates single-phase power for 240V 30A PF=1.0 (< 1 ms)
      ✓ returns 0 for zero current (< 1 ms)
      ✓ throws PowerCalculationError for negative voltage (1 ms)
      ✓ throws PowerCalculationError for NaN input (< 1 ms)
    threePhase
      ✓ calculates three-phase power for 208V 50A PF=0.8 (< 1 ms)
      ✓ calculates three-phase power for 480V 100A PF=0.85 (< 1 ms)
      ✓ throws PowerCalculationError for negative current (< 1 ms)
    kWToKVA
      ✓ converts 50kW at PF=0.8 to 62.5kVA (< 1 ms)
      ✓ throws PowerCalculationError for power factor of 0 (< 1 ms)
      ✓ throws PowerCalculationError for power factor > 1 (< 1 ms)
    kVAToKW
      ✓ converts 62.5kVA at PF=0.8 to 50kW (< 1 ms)
      ✓ round-trip kW -> kVA -> kW preserves value (< 1 ms)
    totalLoad
      ✓ sums array of load objects correctly (1 ms)
      ✓ handles empty load array (< 1 ms)
      ✓ handles very large loads up to 10MW (< 1 ms)

Tests:  16 passed, 16 total
Time:   0.34s
Coverage: 100% statements, 100% branches, 100% functions, 100% lines
```

```
$ python -m pytest test/test_calculations.py -v

test/test_calculations.py::test_single_phase_valid PASSED
test/test_calculations.py::test_three_phase_valid PASSED
test/test_calculations.py::test_convert_kw_to_kva PASSED
test/test_calculations.py::test_convert_kva_to_kw PASSED
test/test_calculations.py::test_unauthenticated_returns_401 PASSED
test/test_calculations.py::test_malformed_json_returns_400 PASSED
test/test_calculations.py::test_negative_values_returns_400 PASSED

7 passed in 0.42s
```

---

## [x] Author Checklist

- [x] I have read the ticket and the related DDD
- [x] My code matches the approved design
- [x] I have written tests first (TDD)
- [x] All tests pass (`npm test`)
- [x] Linter passes (`npm run lint`)
- [x] I have self-reviewed my diff (`git diff develop`)
- [x] No debug code, console.log, or commented-out code
- [x] No hardcoded configuration values
- [x] No secrets or sensitive data in code
- [x] Commit messages follow conventional commit format
- [x] PR is under 400 lines of diff

## [ ] Reviewer Checklist

- [ ] PR description is clear and complete
- [ ] Tests reviewed first (understood expected behavior)
- [ ] Implementation matches the linked DDD
- [ ] Security concerns checked (input validation, auth, SQL injection)
- [ ] Performance concerns checked (N+1, pagination, indexes)
- [ ] Error handling is appropriate
- [ ] Naming follows coding standards

---

## [x] Screenshots / Diagrams

Not applicable -- this PR contains no UI changes. The `PowerCalculator` is a computation-only module consumed by other UI components.

---

## [x] Notes for Reviewer

**Suggested reading order:**

1. Start with frontend tests: `test/power-calculations.test.js` -- understand what the calculator is expected to do
2. Read the implementation: `src/modules/power-calculations.js` -- verify the formulas
3. Compare backend tests: `test/test_calculations.py` -- confirm parity with frontend
4. Read backend endpoints: `server/api/calculations.py` -- verify input validation and auth

**Areas of concern:**

- Floating-point precision: I used standard IEEE 754 doubles. For the load sizes Power Atlas handles (up to ~2 MW), precision is more than adequate. However, if we ever need financial-grade precision for billing calculations, we may want to revisit this with a decimal library. Flagging this as a known trade-off.
- Power factor validation: I enforce 0 < PF <= 1.0. A power factor of exactly 0 is physically meaningless (purely reactive load with zero real power) and would cause a division-by-zero in kW-to-kVA conversion, so it is rejected.

---

## Completion Checklist

- [x] PR title follows conventional commit format
- [x] Description (what, why, how) filled in
- [x] Changes listed
- [x] Related documents linked
- [x] Test plan documented with results
- [x] Author checklist completed -- all items checked
- [x] Screenshots attached (if UI/architecture change)
- [x] Reviewer notes provided
- [x] PR submitted and reviewer assigned

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Code Review Record | [code-review-record.md](code-review-record.md) | Review of this PR |
| Technical Debt Register | [technical-debt-entry.md](technical-debt-entry.md) | Debt identified during this PR |
| Git Workflow Example | [git-workflow-example.md](git-workflow-example.md) | Branching strategy used for this PR |
| PR Template | [../../phase-5-development/templates/pull-request-template.md](../../phase-5-development/templates/pull-request-template.md) | Template this artifact is based on |
