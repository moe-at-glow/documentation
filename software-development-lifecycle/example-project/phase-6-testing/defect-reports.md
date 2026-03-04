> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Defect Reports -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-003 |
| **When to Use** | Reporting bugs found during any testing phase |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 4 hours for Critical/High, 1 business day for Medium/Low |
| **Runbook** | [Report and Track Defects](../../phase-6-testing/runbooks/report-and-track-defects.md) |
| **Last Verified** | 2026-03-05 |

---

## DEF-001: Power Calculation Returns NaN When Power Factor Is 0

| Field | Value |
|-------|-------|
| **Defect ID** | DEF-001 |
| **Title** | kVA calculation returns NaN when power factor is 0 (division by zero not guarded) |
| **Severity** | Critical |
| **Priority** | Urgent |
| **Status** | Closed |
| **Reporter** | Ahmad Nasser (QA Engineer) |
| **Date Reported** | 2026-02-10 |
| **Assigned To** | Omar Khalil (Developer) |
| **Module** | Calculations |
| **Environment** | Test (localhost:8000) |
| **Version / Branch** | `release/1.0.0` (commit 4a2f8c1) |
| **Related Ticket** | TICKET-078 |
| **Related Test Case** | TC-003 |

### Description

The `convert_kw_to_kva()` function in the Python calculation engine performs `kw / power_factor` without validating that `power_factor` is non-zero. When a user enters PF = 0 through the API, the function returns `NaN`, which propagates to the project totals and corrupts the load schedule display.

### Steps to Reproduce

1. Authenticate as any user.
2. POST `/api/calculations/kva` with body `{ "kw": 10, "power_factor": 0 }`.
3. Observe the response body.

**Reproduction rate:** Always

### Expected Result

The API returns HTTP 400 with an error message: "Power factor must be between 0.01 and 1.0".

### Actual Result

The API returns HTTP 200 with body `{ "kva": NaN }`. No validation error is raised.

### Evidence

#### API Request

```http
POST /api/calculations/kva HTTP/1.1
Host: localhost:8000
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
Content-Type: application/json

{ "kw": 10, "power_factor": 0 }
```

#### API Response

```json
{
  "kva": null
}
```

Note: `NaN` is serialised as `null` in JSON, but the Python function returns `float('nan')` internally.

#### Error Logs

```
[2026-02-10T09:32:14Z] WARN calc-engine: Division by zero in convert_kw_to_kva: kw=10, power_factor=0 -> result=nan
```

### Impact

Critical. If a user accidentally submits PF = 0 (e.g., leaves the field empty and the frontend defaults to 0), the entire project's totals become NaN. This corrupts saved project data and causes the PDF report generator to crash with an unhandled exception. Affects all users of the calculation feature.

### Workaround

Manually ensure power factor is never set to 0 before submitting. No frontend guard exists to prevent this.

### Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | Omar Khalil |
| **Fix Date** | 2026-02-11 |
| **Fix Description** | Added input validation in both the Python calculation engine (`calc_engine/validators.py`) and the Node.js API request schema (`api/schemas/calculations.js`). Power factor is now validated to be between 0.01 and 1.0 inclusive at both layers. Existing projects with NaN values are repaired by a data migration script. |
| **Fix Commit** | `fix(calc): add PF validation to prevent division by zero` (a7c3e9d) |

### Verification

| Field | Value |
|-------|-------|
| **Verified By** | Ahmad Nasser |
| **Verification Date** | 2026-02-12 |
| **Verification Result** | Passed |
| **Regression Check** | Passed -- all 14 calculation unit tests pass; TC-001, TC-002, TC-003 all pass |
| **Notes** | Verified PF = 0, PF = -1, PF = 1.5, and PF = 0.005 (below min). All correctly rejected with descriptive error messages. |

---

## DEF-002: Session Not Invalidated on Password Change

| Field | Value |
|-------|-------|
| **Defect ID** | DEF-002 |
| **Title** | Existing JWT sessions remain valid after user changes their password (security vulnerability) |
| **Severity** | High |
| **Priority** | High |
| **Status** | Closed |
| **Reporter** | Ahmad Nasser (QA Engineer) |
| **Date Reported** | 2026-02-13 |
| **Assigned To** | Omar Khalil (Developer) |
| **Module** | Auth |
| **Environment** | Test (localhost:8000) |
| **Version / Branch** | `release/1.0.0` (commit b1d4f6e) |
| **Related Ticket** | TICKET-082 |
| **Related Test Case** | TC-013 |

### Description

When a user changes their password through `/api/auth/change-password`, all previously issued JWT tokens remain valid until their natural expiry (1 hour or 24 hours for remember-me). This means that if an account is compromised and the legitimate user changes their password, the attacker's existing session continues to function.

### Steps to Reproduce

1. Login as User A and obtain JWT token (Token-1).
2. Use Token-1 to access GET `/api/projects` -- succeeds (200).
3. Change password via POST `/api/auth/change-password` with `{ "current_password": "OldPass123!", "new_password": "NewPass456!" }`.
4. Use Token-1 (issued before password change) to access GET `/api/projects`.
5. Observe the response.

**Reproduction rate:** Always

### Expected Result

Step 4 should return HTTP 401 with "Session invalidated. Please log in again." All tokens issued before the password change should be rejected.

### Actual Result

Step 4 returns HTTP 200 with project data. The old token continues to work as if the password was never changed.

### Evidence

#### API Request (Step 4, after password change)

```http
GET /api/projects HTTP/1.1
Host: localhost:8000
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiMSIsImlhdCI6MTcwOTI...
```

#### API Response

```json
{
  "data": [
    { "id": "proj-001", "name": "Test Project", "status": "active" }
  ]
}
```

### Impact

High security risk. If a user's credentials are compromised and they change their password to remediate, the attacker retains access for up to 24 hours (remember-me token). This violates security best practice and the SWR-AUTH-006 requirement for session invalidation on credential change.

### Workaround

Users can manually log out of all sessions via `/api/auth/logout-all` (which clears the token blacklist), but this is a separate action that most users would not think to perform.

### Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | Omar Khalil |
| **Fix Date** | 2026-02-15 |
| **Fix Description** | Added a `token_valid_after` timestamp column to the `users` table. On password change, this field is updated to the current time. The JWT verification middleware now checks that the token's `iat` (issued at) is after the user's `token_valid_after` timestamp. Tokens issued before the password change are automatically rejected. |
| **Fix Commit** | `fix(auth): invalidate existing sessions on password change` (c9e2a1b) |

### Verification

| Field | Value |
|-------|-------|
| **Verified By** | Ahmad Nasser |
| **Verification Date** | 2026-02-16 |
| **Verification Result** | Passed |
| **Regression Check** | Passed -- all auth integration tests pass; TC-005, TC-006, TC-013 all pass |
| **Notes** | Verified that: (a) old tokens are rejected immediately after password change, (b) new login with new password works, (c) other users' sessions are not affected, (d) admin password reset also triggers invalidation. |

---

## DEF-003: PDF Report Truncates Arabic Text in Load Names

| Field | Value |
|-------|-------|
| **Defect ID** | DEF-003 |
| **Title** | PDF report truncates Arabic text in load names after the 12th character in table cells |
| **Severity** | Medium |
| **Priority** | Medium |
| **Status** | Open |
| **Reporter** | Ahmad Nasser (QA Engineer) |
| **Date Reported** | 2026-02-17 |
| **Assigned To** | Omar Khalil (Developer) |
| **Module** | Layout Builder (PDF generation) |
| **Environment** | Test (localhost:8000) |
| **Version / Branch** | `release/1.0.0` (commit d3f5b8a) |
| **Related Ticket** | TICKET-091 |
| **Related Test Case** | TC-011 |

### Description

When generating a PDF report for a project that contains loads with Arabic names, the Arabic text is truncated after approximately 12 characters in the load schedule table. The remaining characters are replaced with an ellipsis. English load names of similar length render fully without truncation.

### Steps to Reproduce

1. Authenticate as any user.
2. Create a project with a load named "مكيف الهواء المركزي للمبنى" (Arabic for "Central air conditioning for the building" -- 25 characters).
3. POST `/api/projects/{id}/report` with `{ "format": "pdf", "language": "ar" }`.
4. Open the generated PDF.
5. Inspect the load name column in the load schedule table.

**Reproduction rate:** Always (for Arabic text longer than 12 characters)

### Expected Result

The full Arabic load name "مكيف الهواء المركزي للمبنى" is displayed in the table cell, wrapping to a second line if necessary.

### Actual Result

The load name is truncated to "مكيف الهواء ال..." in the table cell.

### Evidence

#### Screenshot

The PDF load schedule table shows:

| Load Name | Phase | Amps | kW |
|-----------|-------|------|----|
| مكيف الهواء ال... | Three | 80 | 49.88 |
| Site Lighting Panel Board | Single | 10 | 1.84 |

Note: The English name "Site Lighting Panel Board" (25 characters) renders fully, but the Arabic name of similar length is truncated.

### Impact

Medium. Affects all Saudi-market clients who use Arabic load names in their reports. The truncated names make the PDF report less useful for on-site reference. Approximately 40% of GlowPowerRental clients use Arabic load names.

### Workaround

Use shortened Arabic load names (under 12 characters), or generate the English-only version of the PDF report and manually annotate Arabic names.

### Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | -- |
| **Fix Date** | -- |
| **Fix Description** | Under investigation. Root cause appears to be the PDF library's text measurement function using byte length instead of character count for RTL text. A fix requires updating the PDF generation library or implementing a custom text measurement function for Arabic script. |
| **Fix Commit** | -- |

### Verification

| Field | Value |
|-------|-------|
| **Verified By** | -- |
| **Verification Date** | -- |
| **Verification Result** | -- |
| **Regression Check** | -- |
| **Notes** | Scheduled for fix in patch release 1.0.1. UAT conditionally approved with this as a known issue. |

---

## DEF-004: Tooltip Text Overlaps on Mobile Viewport

| Field | Value |
|-------|-------|
| **Defect ID** | DEF-004 |
| **Title** | Tooltip text for calculation help icons overlaps adjacent form fields on mobile viewport (< 768px) |
| **Severity** | Low |
| **Priority** | Low |
| **Status** | Deferred |
| **Reporter** | Khalid Barakat (Field Engineer, UAT) |
| **Date Reported** | 2026-02-24 |
| **Assigned To** | -- |
| **Module** | Layout Builder (UI) |
| **Environment** | Test (localhost:8000), Chrome mobile emulation (iPhone 14 Pro, 393x852) |
| **Version / Branch** | `release/1.0.0` (commit e6a1c4d) |
| **Related Ticket** | TICKET-095 |
| **Related Test Case** | TC-016 |

### Description

On mobile viewports (screen width below 768px), the tooltip that appears when tapping the "?" help icon next to the power factor input field overlaps the amperage input field below it. The tooltip content is readable but covers the adjacent input, making it difficult to tap the next field without first dismissing the tooltip.

### Steps to Reproduce

1. Open Power Atlas in a mobile browser or Chrome DevTools mobile emulation (iPhone 14 Pro, 393px width).
2. Navigate to the "Add Load" form within any project.
3. Tap the "?" help icon next to the "Power Factor" input field.
4. Observe the tooltip position relative to the "Amperage" input field below.

**Reproduction rate:** Always (on viewports < 768px wide)

### Expected Result

The tooltip displays above or to the side of the help icon without overlapping adjacent input fields. On narrow viewports, the tooltip should reposition itself or use a modal/bottom-sheet pattern.

### Actual Result

The tooltip renders directly below the help icon, overlapping approximately 60% of the amperage input field. The tooltip does not auto-reposition on narrow viewports.

### Evidence

#### Screenshot Description

On iPhone 14 Pro viewport (393px):
- The power factor help tooltip appears as a white box with grey border
- It extends 120px below the help icon
- The amperage input field starts 80px below the help icon
- The overlap region is approximately 40px, covering the top portion of the amperage field label and input

### Impact

Low. Cosmetic issue that does not prevent task completion. Users can dismiss the tooltip by tapping elsewhere before interacting with the amperage field. Only affects mobile users who access the help tooltips.

### Workaround

Tap anywhere outside the tooltip to dismiss it before proceeding to the next input field.

### Resolution

| Field | Value |
|-------|-------|
| **Fixed By** | -- |
| **Fix Date** | -- |
| **Fix Description** | Deferred to Release 1.1. Planned fix: implement responsive tooltip positioning using Floating UI library with viewport boundary detection and fallback to bottom-sheet pattern on mobile. |
| **Fix Commit** | -- |

### Verification

| Field | Value |
|-------|-------|
| **Verified By** | -- |
| **Verification Date** | -- |
| **Verification Result** | -- |
| **Regression Check** | -- |
| **Notes** | Accepted as known limitation for Release 1.0. Low user impact based on analytics showing < 5% of sessions use mobile viewport. |

---

## Completion Checklist

- [x] All defect IDs assigned following naming convention (DEF-001 through DEF-004)
- [x] Titles are clear and specific
- [x] Severity and priority assessed for each defect
- [x] Steps to reproduce are exact and repeatable
- [x] Expected and actual results documented
- [x] Evidence attached (API logs, screenshots, error logs as applicable)
- [x] Impact described with affected scope
- [x] Workaround documented (or "None" stated)
- [x] Related tickets and test cases linked
- [x] Resolution section completed for fixed defects (DEF-001, DEF-002)
- [x] Verification section completed for fixed defects (DEF-001, DEF-002)

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Report and Track Defects | [../../phase-6-testing/runbooks/report-and-track-defects.md](../../phase-6-testing/runbooks/report-and-track-defects.md) |
| Template | Defect Report Template | [../../phase-6-testing/templates/defect-report-template.md](../../phase-6-testing/templates/defect-report-template.md) |
| Artifact | Test Cases | [test-cases.md](test-cases.md) |
| Artifact | Test Plan | [test-plan.md](test-plan.md) |
| Artifact | Test Summary Report | [test-summary-report.md](test-summary-report.md) |
