> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Test Cases -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-002 |
| **When to Use** | Documenting individual test cases for any test level |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 1 business day per test case |
| **Runbook** | [Write Integration Tests](../../phase-6-testing/runbooks/write-integration-tests.md), [Write System Tests](../../phase-6-testing/runbooks/write-system-tests.md) |
| **Last Verified** | 2026-03-05 |

---

## TC-001: Single-Phase Power Calculation

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-001 |
| **Title** | Single-phase power calculation returns correct kW for given amperage and power factor |
| **Test Level** | Unit |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-CALC-001 |
| **Module** | Calculations |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-10 |

### Preconditions

1. Python calculation engine is running and accessible.
2. Test database is seeded with standard test data.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Call `calculate_single_phase_kw()` function | `amperage=10, voltage=230, power_factor=0.8` | Returns `1.84` (kW) |
| 2 | Verify formula: kW = (A x V x PF) / 1000 | `(10 x 230 x 0.8) / 1000 = 1.84` | Calculation matches expected formula output |
| 3 | Call via API: POST `/api/calculations/single-phase` | `{ "amperage": 10, "voltage": 230, "power_factor": 0.8 }` | Response 200 with `{ "kw": 1.84 }` |
| 4 | Verify result is rounded to 2 decimal places | `amperage=7, voltage=230, power_factor=0.85` | Returns `1.37` (not 1.3685) |

### Expected Result

The single-phase calculation returns `1.84 kW` for 10A at 230V with PF 0.8. All results are rounded to 2 decimal places.

### Postconditions / Cleanup

1. No persistent data created; no cleanup required.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-10 | Ahmad Nasser | localhost:8000 | Pass | N/A |
| Run 2 | 2026-02-22 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-002: Three-Phase Power Calculation

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-002 |
| **Title** | Three-phase power calculation returns correct kW for given amperage and power factor |
| **Test Level** | Unit |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-CALC-002 |
| **Module** | Calculations |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-10 |

### Preconditions

1. Python calculation engine is running and accessible.
2. Test database is seeded with standard test data.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Call `calculate_three_phase_kw()` function | `amperage=50, voltage=400, power_factor=0.85` | Returns `29.44` (kW) |
| 2 | Verify formula: kW = (A x V x sqrt(3) x PF) / 1000 | `(50 x 400 x 1.7321 x 0.85) / 1000 = 29.44` | Calculation matches expected formula output |
| 3 | Call via API: POST `/api/calculations/three-phase` | `{ "amperage": 50, "voltage": 400, "power_factor": 0.85 }` | Response 200 with `{ "kw": 29.44 }` |
| 4 | Verify with high amperage boundary | `amperage=500, voltage=400, power_factor=0.9` | Returns `311.77` (kW) |

### Expected Result

The three-phase calculation returns `29.44 kW` for 50A at 400V with PF 0.85. Formula uses sqrt(3) = 1.7321 and rounds to 2 decimal places.

### Postconditions / Cleanup

1. No persistent data created; no cleanup required.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-10 | Ahmad Nasser | localhost:8000 | Pass | N/A |
| Run 2 | 2026-02-22 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-003: kW to kVA Conversion

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-003 |
| **Title** | kW to kVA conversion returns correct value for given power factor |
| **Test Level** | Unit |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-CALC-003 |
| **Module** | Calculations |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-10 |

### Preconditions

1. Python calculation engine is running and accessible.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Call `convert_kw_to_kva()` function | `kw=10, power_factor=0.8` | Returns `12.5` (kVA) |
| 2 | Verify formula: kVA = kW / PF | `10 / 0.8 = 12.5` | Calculation matches expected formula output |
| 3 | Call via API: POST `/api/calculations/kva` | `{ "kw": 10, "power_factor": 0.8 }` | Response 200 with `{ "kva": 12.5 }` |
| 4 | Test with PF = 1.0 (unity) | `kw=10, power_factor=1.0` | Returns `10.0` (kVA equals kW at unity PF) |
| 5 | Test with PF = 0.0 | `kw=10, power_factor=0.0` | Returns error: "Power factor must be between 0.01 and 1.0" |

### Expected Result

The kVA conversion returns `12.5 kVA` for 10 kW at PF 0.8. Division by zero is prevented by input validation rejecting PF = 0.

### Postconditions / Cleanup

1. No persistent data created; no cleanup required.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-10 | Ahmad Nasser | localhost:8000 | Fail | DEF-001 |
| Run 2 | 2026-02-16 | Ahmad Nasser | localhost:8000 | Pass | N/A |

### Actual Results (Run 1)

Step 5 returned `NaN` instead of a validation error. The function performed division by zero without input guard. See DEF-001.

---

## TC-004: Zero and Negative Input Validation

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-004 |
| **Title** | Calculation endpoints reject zero, negative, and out-of-range inputs |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-CALC-004 |
| **Module** | Calculations |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-11 |

### Preconditions

1. API server is running at localhost:8000.
2. User is authenticated with a valid JWT token.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/calculations/single-phase` with zero amperage | `{ "amperage": 0, "voltage": 230, "power_factor": 0.8 }` | 400 with error "Amperage must be greater than 0" |
| 2 | POST `/api/calculations/single-phase` with negative amperage | `{ "amperage": -5, "voltage": 230, "power_factor": 0.8 }` | 400 with error "Amperage must be greater than 0" |
| 3 | POST `/api/calculations/three-phase` with PF > 1 | `{ "amperage": 50, "voltage": 400, "power_factor": 1.5 }` | 400 with error "Power factor must be between 0.01 and 1.0" |
| 4 | POST `/api/calculations/single-phase` with missing voltage | `{ "amperage": 10, "power_factor": 0.8 }` | 400 with error "Voltage is required" |
| 5 | POST `/api/calculations/kva` with string input | `{ "kw": "ten", "power_factor": 0.8 }` | 400 with error "kW must be a number" |

### Expected Result

All invalid inputs are rejected with HTTP 400 and descriptive error messages. No calculation is attempted with invalid data.

### Postconditions / Cleanup

1. No persistent data created; no cleanup required.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-11 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-005: User Login with Valid Credentials

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-005 |
| **Title** | User can log in with valid email and password and receive a JWT token |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-AUTH-001 |
| **Module** | Auth |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-11 |

### Preconditions

1. User account exists: `engineer@glowpower.com` with bcrypt-hashed password for `TestPass123!`.
2. Account is not locked.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/auth/login` | `{ "email": "engineer@glowpower.com", "password": "TestPass123!" }` | 200 with JWT token in response body |
| 2 | Decode JWT payload | Token from step 1 | Contains `user_id`, `email`, `role`, `iat`, `exp` fields |
| 3 | Verify token expiry | Token `exp` field | Set to 1 hour from `iat` for standard session |
| 4 | Use token to access protected route: GET `/api/projects` | `Authorization: Bearer {token}` | 200 with project list |
| 5 | Verify password is not logged | Check application logs | No plaintext password appears in any log entry |

### Expected Result

User receives a valid JWT token upon successful login. Token contains correct claims and grants access to protected endpoints.

### Postconditions / Cleanup

1. No test data modified; no cleanup required.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-11 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-006: Account Lockout After 5 Failed Attempts

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-006 |
| **Title** | Account is locked for 15 minutes after 5 consecutive failed login attempts |
| **Test Level** | Integration |
| **Test Type** | Security |
| **Priority** | Critical |
| **Requirement** | SWR-AUTH-004 |
| **Module** | Auth |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-11 |

### Preconditions

1. User account exists: `locktest@glowpower.com` with known password `LockTest123!`.
2. Account has zero failed login attempts (counter reset).

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/auth/login` with wrong password (attempt 1) | `{ "email": "locktest@glowpower.com", "password": "wrong1" }` | 401 with "Invalid credentials" |
| 2 | POST `/api/auth/login` with wrong password (attempt 2) | `{ "email": "locktest@glowpower.com", "password": "wrong2" }` | 401 with "Invalid credentials" |
| 3 | POST `/api/auth/login` with wrong password (attempt 3) | `{ "email": "locktest@glowpower.com", "password": "wrong3" }` | 401 with "Invalid credentials" |
| 4 | POST `/api/auth/login` with wrong password (attempt 4) | `{ "email": "locktest@glowpower.com", "password": "wrong4" }` | 401 with "Invalid credentials" |
| 5 | POST `/api/auth/login` with wrong password (attempt 5) | `{ "email": "locktest@glowpower.com", "password": "wrong5" }` | 429 with "Account locked. Try again in 15 minutes." |
| 6 | POST `/api/auth/login` with correct password (during lockout) | `{ "email": "locktest@glowpower.com", "password": "LockTest123!" }` | 429 with "Account locked. Try again in 15 minutes." |
| 7 | Advance time by 15 minutes (mock clock or wait) | N/A | Lockout period expires |
| 8 | POST `/api/auth/login` with correct password (after lockout) | `{ "email": "locktest@glowpower.com", "password": "LockTest123!" }` | 200 with JWT token |

### Expected Result

After 5 failed login attempts, the account is locked for exactly 15 minutes. During lockout, even correct credentials are rejected. After 15 minutes, the account unlocks and the user can log in normally.

### Postconditions / Cleanup

1. Reset failed attempt counter for `locktest@glowpower.com`.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-12 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-007: Create Project with All Fields

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-007 |
| **Title** | User creates a new project with all required and optional fields |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-PROJ-001 |
| **Module** | Projects |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-11 |

### Preconditions

1. User is authenticated with a valid JWT token (role: engineer).
2. Client "Al-Faisal Construction" exists in the database (client_id: `cli-001`).

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/projects` | `{ "name": "Riyadh Metro Station 4 Power Plan", "client_id": "cli-001", "location": "Riyadh, KSA", "voltage_standard": "230/400V", "notes": "Phase 1 temporary power during excavation", "diversity_factor": 0.7 }` | 201 with project data including generated `id` |
| 2 | Verify project status | Response from step 1 | `status` is `"draft"` |
| 3 | Verify `created_at` timestamp | Response from step 1 | ISO 8601 timestamp within last 5 seconds |
| 4 | GET `/api/projects/{id}` | Project ID from step 1 | 200 with all fields matching step 1 input |
| 5 | Verify project appears in user's project list | GET `/api/projects` | List includes the newly created project |

### Expected Result

A new project is created with status "draft", all provided fields are persisted correctly, and the project is immediately visible in the user's project list.

### Postconditions / Cleanup

1. DELETE `/api/projects/{id}` to remove the test project.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-12 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-008: Add Load to Project and Verify Total Recalculation

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-008 |
| **Title** | Adding a load to a project triggers automatic recalculation of project totals |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-LOAD-001, SWR-CALC-005 |
| **Module** | Loads, Calculations |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-12 |

### Preconditions

1. User is authenticated with a valid JWT token.
2. Project "Test Project Alpha" exists (project_id: `proj-test-001`) with status "active" and no loads.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/loads` -- add first load | `{ "project_id": "proj-test-001", "name": "Site Lighting", "phase": "single", "amperage": 10, "voltage": 230, "power_factor": 0.8, "quantity": 4, "category": "lighting" }` | 201 with load data; `kw` = 1.84 per unit |
| 2 | GET `/api/projects/proj-test-001` | Auth header | `total_kw` = 7.36 (1.84 x 4), `total_kva` = 9.20 |
| 3 | POST `/api/loads` -- add second load | `{ "project_id": "proj-test-001", "name": "Tower Crane", "phase": "three", "amperage": 50, "voltage": 400, "power_factor": 0.85, "quantity": 1, "category": "tools" }` | 201 with load data; `kw` = 29.44 per unit |
| 4 | GET `/api/projects/proj-test-001` | Auth header | `total_kw` = 36.80 (7.36 + 29.44), `total_kva` = 44.34 |
| 5 | Verify diversity-adjusted total | Check `adjusted_kw` field | `adjusted_kw` = 36.80 x 0.7 (diversity factor) = 25.76 |

### Expected Result

Each time a load is added, the project totals (total_kw, total_kva, adjusted_kw) are automatically recalculated to include the new load.

### Postconditions / Cleanup

1. DELETE all loads for `proj-test-001`.
2. Verify project totals reset to 0.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-12 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-009: Submit Client Requirement via Public Form

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-009 |
| **Title** | External client submits a power requirement through the public submission form |
| **Test Level** | System |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-REQ-001 |
| **Module** | Requirements |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-15 |

### Preconditions

1. Application is running and the public requirement form is accessible at `/requirements/submit`.
2. No prior requirements exist for today's date with the test company name.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Navigate to `/requirements/submit` | Browser | Public form loads with fields: company name, contact person, email, phone, event name, event date, location, estimated power (kW), notes |
| 2 | Fill in all required fields | Company: "Desert Fest Events", Contact: "Mariam Zayed", Email: "mariam@desertfest.sa", Phone: "+966501234567", Event: "Desert Music Festival 2026", Date: "2026-04-15", Location: "AlUla, KSA", Estimated power: 250 kW | All fields accept input without errors |
| 3 | Submit the form | Click "Submit Requirement" button | Success message: "Your requirement has been submitted. Reference: PR{DDMMYYYY}-{seq}" |
| 4 | Verify requirement code format | Reference from step 3 | Matches pattern `PR05032026-001` (or appropriate sequence number) |
| 5 | Verify via API: GET `/api/requirements?company=Desert+Fest+Events` | Admin auth header | Requirement appears with status "pending" and all submitted data |

### Expected Result

The client requirement is submitted successfully, assigned a requirement code in the format PR{DDMMYYYY}-{seq}, stored with status "pending", and visible to admin users.

### Postconditions / Cleanup

1. DELETE the test requirement via admin API.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-15 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-010: Admin Approve Requirement and Verify Notification

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-010 |
| **Title** | Admin approves a pending client requirement and client receives email notification |
| **Test Level** | System |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-REQ-003 |
| **Module** | Requirements |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-15 |

### Preconditions

1. Admin user is authenticated with role "admin".
2. Pending requirement `PR05032026-001` exists from TC-009 (or equivalent test fixture).
3. Email service is configured to use a test mailbox (MailHog or equivalent).

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | GET `/api/requirements/PR05032026-001` | Admin auth header | 200 with requirement details, `status` = "pending" |
| 2 | PATCH `/api/requirements/PR05032026-001` | `{ "status": "approved", "admin_notes": "Approved. Assigned to Omar for site survey." }` | 200 with updated requirement, `status` = "approved" |
| 3 | Verify requirement status persisted | GET `/api/requirements/PR05032026-001` | `status` = "approved", `reviewed_by` populated, `reviewed_at` timestamp present |
| 4 | Check test mailbox for client notification | Query MailHog API for emails to `mariam@desertfest.sa` | Email received with subject containing "Requirement Approved" and reference code |
| 5 | Verify email content | Email body | Contains requirement code, approval status, and admin notes |

### Expected Result

The requirement transitions from "pending" to "approved", the reviewing admin and timestamp are recorded, and the client receives an email notification with the approval details.

### Postconditions / Cleanup

1. Clear test mailbox.
2. Reset requirement status to "pending" or delete.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-16 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-011: Generate PDF Report for Project with 10 Loads

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-011 |
| **Title** | PDF report generates correctly for a project containing 10 electrical loads |
| **Test Level** | System |
| **Test Type** | Functional |
| **Priority** | High |
| **Requirement** | SWR-PDF-001 |
| **Module** | Layout Builder |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-17 |

### Preconditions

1. User is authenticated with a valid JWT token.
2. Project "Jeddah Exhibition Hall" (proj-test-pdf) exists with 10 loads: 4 lighting (single-phase), 3 HVAC (three-phase), 2 tools (three-phase), 1 other (single-phase).
3. All loads have Arabic and English names (e.g., "Site Lighting / اضاءة الموقع").

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | POST `/api/projects/proj-test-pdf/report` | `{ "format": "pdf", "language": "en" }` | 200 with PDF binary in response; Content-Type: application/pdf |
| 2 | Verify PDF file size | Downloaded PDF | File size > 10 KB and < 5 MB |
| 3 | Extract text from PDF and verify project header | PDF content | Contains "Jeddah Exhibition Hall", client name, date |
| 4 | Verify all 10 loads listed in the load schedule table | PDF content | All 10 load names, amperages, phases, kW values present |
| 5 | Verify totals section | PDF content | Total kW, total kVA, adjusted kW (with diversity factor) match API values |
| 6 | Generate bilingual PDF | `{ "format": "pdf", "language": "ar" }` | PDF renders with Arabic load names correctly (RTL text) |
| 7 | Verify Arabic text rendering | PDF content | Arabic load names render without truncation or character substitution |

### Expected Result

PDF report is generated with all 10 loads listed, correct totals, and proper formatting. Arabic text renders correctly in the bilingual version.

### Postconditions / Cleanup

1. Delete generated PDF files from temp storage.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-17 | Ahmad Nasser | localhost:8000 | Fail | DEF-003 |
| Run 2 | 2026-02-25 | Ahmad Nasser | localhost:8000 | Fail | DEF-003 (still open) |

### Actual Results

Steps 1-5 passed. Steps 6-7 failed: Arabic load names are truncated after the 12th character in the PDF table cells. English-only PDF generation works correctly. See DEF-003.

---

## TC-012: Project Sharing Between Users

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-012 |
| **Title** | Project owner can share a project with another user and the recipient gains read access |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | Medium |
| **Requirement** | SWR-PROJ-004 |
| **Module** | Projects |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-15 |

### Preconditions

1. User A (owner) is authenticated: `ownerA@glowpower.com`.
2. User B (recipient) is authenticated: `engineerB@glowpower.com`.
3. Project "Shared Test Project" exists, owned by User A.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Verify User B cannot access the project initially | GET `/api/projects/{id}` with User B token | 403 Forbidden |
| 2 | Share project with User B | POST `/api/projects/{id}/share` with User A token, `{ "user_email": "engineerB@glowpower.com", "permission": "read" }` | 200 with share confirmation |
| 3 | Verify User B can now access the project | GET `/api/projects/{id}` with User B token | 200 with project data |
| 4 | Verify User B cannot modify the project | PUT `/api/projects/{id}` with User B token, `{ "name": "Modified Name" }` | 403 Forbidden |
| 5 | Revoke sharing | DELETE `/api/projects/{id}/share/engineerB@glowpower.com` with User A token | 200 with revocation confirmation |
| 6 | Verify User B can no longer access the project | GET `/api/projects/{id}` with User B token | 403 Forbidden |

### Expected Result

Project sharing grants the specified permission level. Read-only recipients can view but not modify the project. Revoking the share removes access immediately.

### Postconditions / Cleanup

1. Ensure share is revoked (step 5 handles this).

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-16 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-013: Session Timeout After 1 Hour Inactivity

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-013 |
| **Title** | User session expires after 1 hour of inactivity and requires re-authentication |
| **Test Level** | Integration |
| **Test Type** | Security |
| **Priority** | High |
| **Requirement** | SWR-AUTH-005 |
| **Module** | Auth |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-12 |

### Preconditions

1. User is authenticated and has a valid JWT token.
2. Test environment supports clock mocking or short-lived token overrides.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Login and obtain JWT token | POST `/api/auth/login` with valid credentials | 200 with token; `exp` set to 1 hour from now |
| 2 | Immediately access a protected route | GET `/api/projects` with token | 200 with project list |
| 3 | Advance mock clock by 59 minutes | N/A | Token should still be valid |
| 4 | Access protected route at 59 minutes | GET `/api/projects` with same token | 200 with project list |
| 5 | Advance mock clock to 61 minutes total | N/A | Token should now be expired |
| 6 | Access protected route at 61 minutes | GET `/api/projects` with same token | 401 with "Token expired" |
| 7 | Verify "remember me" extends session to 24 hours | Login with `{ ..., "remember_me": true }` and advance clock to 23 hours | 200 -- token still valid |
| 8 | Access at 25 hours with remember-me token | GET `/api/projects` with remember-me token | 401 with "Token expired" |

### Expected Result

Standard sessions expire after 1 hour. "Remember me" sessions expire after 24 hours. Expired tokens return 401 and require the user to re-authenticate.

### Postconditions / Cleanup

1. Reset mock clock to real time.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-12 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## TC-014: Concurrent Project Edits (Optimistic Locking)

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-014 |
| **Title** | Optimistic locking prevents silent data loss when two users edit the same project simultaneously |
| **Test Level** | Integration |
| **Test Type** | Functional |
| **Priority** | Medium |
| **Requirement** | SWR-PROJ-005 |
| **Module** | Projects |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-15 |

### Preconditions

1. User A and User B are both authenticated.
2. Both users have write access to project "Concurrent Test Project" (proj-concurrent).
3. Project has `version` field = 1.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | User A fetches the project | GET `/api/projects/proj-concurrent` (User A token) | 200 with `version: 1` |
| 2 | User B fetches the same project | GET `/api/projects/proj-concurrent` (User B token) | 200 with `version: 1` |
| 3 | User A updates the project name | PUT `/api/projects/proj-concurrent` with `{ "name": "Updated by A", "version": 1 }` (User A token) | 200 with `version: 2` |
| 4 | User B attempts to update with stale version | PUT `/api/projects/proj-concurrent` with `{ "name": "Updated by B", "version": 1 }` (User B token) | 409 Conflict with "Project has been modified. Please refresh and try again." |
| 5 | User B refreshes and retries | GET then PUT with `version: 2` | 200 with `version: 3` |

### Expected Result

The second update with a stale version number is rejected with HTTP 409. No data is silently overwritten. The user is prompted to refresh and retry.

### Postconditions / Cleanup

1. Reset project name and version.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-17 | Ahmad Nasser | localhost:8000 | Blocked | N/A |

### Notes

Blocked: SQLite does not reliably reproduce the concurrency scenario. This test case needs to be executed against PostgreSQL staging environment. Deferred to pre-production validation.

---

## TC-015: End-to-End -- Create Project, Add Loads, Calculate, Generate PDF

| Field | Value |
|-------|-------|
| **Test Case ID** | TC-015 |
| **Title** | Complete user journey: create a project, add loads, verify calculations, and generate a PDF report |
| **Test Level** | System |
| **Test Type** | Functional |
| **Priority** | Critical |
| **Requirement** | SWR-PROJ-001, SWR-LOAD-001, SWR-CALC-001, SWR-CALC-002, SWR-PDF-001 |
| **Module** | Projects, Loads, Calculations, Layout Builder |
| **Author** | Ahmad Nasser |
| **Date Created** | 2026-02-17 |

### Preconditions

1. User is authenticated with role "engineer".
2. Client "Al-Noor Industries" exists in the database.
3. Browser automation (Playwright) is configured.

### Test Steps

| Step | Action | Input / Data | Expected Result |
|------|--------|-------------|----------------|
| 1 | Navigate to "New Project" page | Click "New Project" in sidebar | Project creation form loads |
| 2 | Fill project details and save | Name: "Al-Noor Factory Expansion", Client: "Al-Noor Industries", Location: "Dammam, KSA", Voltage: "230/400V", Diversity factor: 0.8 | Project created with status "draft"; redirected to project detail page |
| 3 | Add single-phase load | Click "Add Load"; Name: "Office Lighting", Phase: Single, Amps: 10, PF: 0.8, Qty: 6 | Load added; individual kW = 1.84; subtotal = 11.04 kW |
| 4 | Add three-phase load | Click "Add Load"; Name: "Workshop Compressor", Phase: Three, Amps: 50, PF: 0.85, Qty: 2 | Load added; individual kW = 29.44; subtotal = 58.88 kW |
| 5 | Add another three-phase load | Click "Add Load"; Name: "HVAC Central Unit", Phase: Three, Amps: 80, PF: 0.9, Qty: 1 | Load added; individual kW = 49.88 kW |
| 6 | Verify project total calculations on screen | Read totals panel | Total kW = 119.80, Total kVA = 146.08, Adjusted kW = 95.84 (x 0.8 diversity) |
| 7 | Activate the project | Click "Activate Project" button | Project status changes from "draft" to "active" |
| 8 | Generate PDF report | Click "Generate Report" button | PDF downloads; file name includes project name and date |
| 9 | Open and verify PDF content | Open downloaded PDF | Contains project header, 3 loads in table, totals section, GlowPowerRental branding |
| 10 | Archive the project | Click "Archive Project" | Project status changes to "archived"; loads become read-only |

### Expected Result

The full user journey completes without errors. Each step produces the expected UI state and data. The PDF report accurately reflects all project data and calculations.

### Postconditions / Cleanup

1. Delete the test project and all associated loads.
2. Delete the generated PDF file.

### Test Execution Record

| Execution | Date | Tester | Environment | Result | Defect |
|-----------|------|--------|-------------|--------|--------|
| Run 1 | 2026-02-18 | Ahmad Nasser | localhost:8000 | Pass | N/A |
| Run 2 | 2026-02-23 | Ahmad Nasser | localhost:8000 | Pass | N/A |

---

## Completion Checklist

- [x] All 15 test cases documented with IDs following naming convention
- [x] Titles clearly describe what is being tested
- [x] Test levels and types specified for each case
- [x] Priorities assigned (6 Critical, 7 High, 2 Medium)
- [x] Requirement traceability linked (SWR-NNN)
- [x] Preconditions documented
- [x] Test steps written with actions, inputs, and expected results
- [x] Overall expected results stated
- [x] Postconditions / cleanup steps defined
- [x] Test execution records populated with actual results

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Write Integration Tests | [../../phase-6-testing/runbooks/write-integration-tests.md](../../phase-6-testing/runbooks/write-integration-tests.md) |
| Runbook | Write System Tests | [../../phase-6-testing/runbooks/write-system-tests.md](../../phase-6-testing/runbooks/write-system-tests.md) |
| Template | Test Case Template | [../../phase-6-testing/templates/test-case-template.md](../../phase-6-testing/templates/test-case-template.md) |
| Artifact | Test Plan | [test-plan.md](test-plan.md) |
| Artifact | Defect Reports | [defect-reports.md](defect-reports.md) |
| Artifact | Test Summary Report | [test-summary-report.md](test-summary-report.md) |
