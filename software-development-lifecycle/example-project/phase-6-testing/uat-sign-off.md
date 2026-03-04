> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# UAT Sign-Off -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-005 |
| **When to Use** | User Acceptance Testing sign-off before production release |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 2 business days after UAT completion |
| **Runbook** | [Execute Test Cycle](../../phase-6-testing/runbooks/execute-test-cycle.md) |
| **Last Verified** | 2026-03-05 |

---

## UAT Information

| Field | Value |
|-------|-------|
| Project | Power Atlas -- GlowPowerRental |
| Release | Release 1.0.0 |
| UAT Period | 2026-02-24 to 2026-02-26 |
| Environment | Test environment at localhost:8000 (mirroring staging configuration) |
| UAT Lead | Fatima Hassan (Product Owner) |
| Date | 2026-02-27 |

### UAT Participants

| Name | Role | Department | Availability |
|------|------|-----------|-------------|
| Fatima Hassan | Product Owner | Product | Full 3 days |
| Khalid Barakat | Senior Field Engineer | Operations (Riyadh) | 2 days (Feb 24-25) |
| Yusuf Darwish | Field Engineer | Operations (Jeddah) | 2 days (Feb 24-25) |
| Layla Omari | Field Engineer | Operations (Dammam) | 2 days (Feb 25-26) |

---

## 1. Features Tested

| Feature | Ticket | Acceptance Criteria | Result |
|---------|--------|-------------------|--------|
| User authentication and access control | TICKET-045 | Users can register, login, reset password; roles enforced; lockout works | Accepted |
| Project creation and lifecycle management | TICKET-052 | Projects can be created, activated, archived; all fields persist | Accepted |
| Electrical load management | TICKET-058 | Loads added/edited/removed; categories assigned; quantities supported | Accepted |
| Power calculations (single-phase, three-phase, kVA) | TICKET-061 | Formulas produce correct results; totals auto-update; diversity factor applied | Accepted |
| Client requirement submission and admin workflow | TICKET-067 | Public form works; codes generated; approve/reject flow completes; notifications sent | Accepted |
| PDF report generation | TICKET-073 | English PDF generates correctly with all data; download works | Conditionally Accepted |
| Project sharing | TICKET-076 | Owner shares with other users; read access works; revocation works | Accepted |
| Layout builder drag-and-drop | TICKET-080 | Generators can be placed on site map; cable runs calculated | Accepted |

---

## 2. Acceptance Criteria Verification

### Feature: User Authentication and Access Control

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | User can register with email, name, and password | Yes | Registration flow smooth; password strength indicator helpful |
| 2 | User can login with email/password and receive session | Yes | Login response time under 1 second |
| 3 | Account locks after 5 failed login attempts for 15 minutes | Yes | Tested by Khalid -- lockout message is clear |
| 4 | Session times out after 1 hour of inactivity | Yes | Timeout redirects to login with "session expired" message |
| 5 | "Remember me" extends session to 24 hours | Yes | Verified by Fatima over overnight test |

### Feature: Project Creation and Lifecycle Management

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | User can create a new project with name, client, location, voltage standard | Yes | Form is intuitive; client dropdown loads quickly |
| 2 | New projects start in "draft" status | Yes | Confirmed on 3 new project creations |
| 3 | User can activate a draft project | Yes | Status transition works; loads become editable |
| 4 | User can archive an active project | Yes | Archived projects become read-only as expected |
| 5 | Project list shows status filters (draft / active / archived) | Yes | Filters work correctly; count badges accurate |

### Feature: Power Calculations

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | Single-phase: kW = (A x 230 x PF) / 1000 produces correct result | Yes | Khalid verified with his field calculator -- results match exactly |
| 2 | Three-phase: kW = (A x 400 x sqrt(3) x PF) / 1000 produces correct result | Yes | Yusuf tested with 5 different load configurations from real projects |
| 3 | kVA = kW / PF produces correct result | Yes | Layla confirmed against her standard conversion chart |
| 4 | Totals update automatically when loads are added or removed | Yes | Real-time update; no need to refresh the page |
| 5 | Diversity factor is applied to the adjusted total | Yes | Tested with factors 0.5, 0.7, 0.8, 1.0 -- all correct |

### Feature: Client Requirement Submission

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | External client can access public requirement form without login | Yes | Form accessible at /requirements/submit |
| 2 | Requirement code generated in format PR{DDMMYYYY}-{seq} | Yes | Codes generated correctly for multiple submissions |
| 3 | Admin can view, approve, or reject pending requirements | Yes | Fatima tested full workflow as admin |
| 4 | Client receives email notification on approval/rejection | Yes | Email received within 30 seconds during testing |

### Feature: PDF Report Generation

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | PDF report includes project header, load schedule, and totals | Yes | English PDF is complete and well-formatted |
| 2 | PDF includes GlowPowerRental branding and date | Yes | Logo and date in header; company info in footer |
| 3 | PDF can be downloaded and opened in standard PDF readers | Yes | Tested in Adobe Reader, Chrome, and iOS Preview |
| 4 | Arabic load names render correctly in PDF | No | Arabic text truncated after ~12 characters (DEF-003). This is a blocking condition for full acceptance. |

### Feature: Project Sharing

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | Owner can share a project with another user by email | Yes | Sharing dialog is straightforward |
| 2 | Shared user has read-only access | Yes | Confirmed -- edit buttons hidden for shared users |
| 3 | Owner can revoke sharing | Yes | Access removed immediately on revocation |

### Feature: Layout Builder

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | User can drag generators onto site map canvas | Yes | Drag-and-drop works smoothly; snap-to-grid helpful |
| 2 | System suggests appropriate generator size based on load | Yes | Suggestions are reasonable for typical configurations |
| 3 | Cable run distances are calculated between generator and load points | Yes | Distances accurate; cable size recommendations appropriate |

---

## 3. UAT Test Results

| Metric | Count |
|--------|-------|
| Total scenarios tested | 8 |
| Passed | 7 |
| Failed | 0 |
| Conditionally Accepted | 1 |
| Deferred | 0 |

---

## 4. Issues Found During UAT

| # | Description | Severity | Resolution |
|---|------------|----------|-----------|
| 1 | Arabic text truncation in PDF load schedule table (DEF-003) | Medium | Deferred -- fix required before go-live for Arabic-language clients. English PDF works correctly. Condition placed on sign-off. |
| 2 | Tooltip overlaps form field on mobile phone (DEF-004) | Low | Accepted -- cosmetic issue; field engineers primarily use tablets and laptops on-site |
| 3 | Generator auto-sizing recommends 100 kVA unit when 80 kVA would suffice for adjusted load of 62 kW | Low | Accepted -- conservative sizing is safer in the field; Khalid noted this matches their current manual practice of rounding up to the next available unit |

---

## 5. Known Limitations

| # | Limitation | Impact | Workaround |
|---|-----------|--------|-----------|
| 1 | Arabic text truncated in PDF reports (DEF-003) | Medium -- affects Arabic-language PDF reports | Use English-only PDF or shorten Arabic load names to < 12 characters |
| 2 | Concurrent editing not fully validated (SQLite test limitation) | Low -- potential conflict if two users edit the same project simultaneously | Coordinate edits verbally during Release 1.0; full optimistic locking validated against PostgreSQL in staging before enabling multi-user edit |
| 3 | PDF page break may split a table row for projects with 50+ loads (DEF-008) | Low -- rare for typical projects | Break large projects into sub-sections with fewer than 50 loads each |

---

## 6. Business Readiness

| Item | Ready? | Notes |
|------|--------|-------|
| User documentation updated | Yes | User guide v1.0 covers all 6 modules; includes screenshots and calculation examples |
| Training completed | Yes | 2-hour training session conducted on 2026-02-23 for 8 field engineers + 3 project managers |
| Support team briefed | Yes | Technical support team received walkthrough on 2026-02-24; escalation path documented |
| Data migration verified | N/A | Greenfield deployment; no data migration required |
| Rollback plan reviewed | Yes | Rollback procedure documented: revert to previous version via deployment script; database backup taken pre-deployment |

---

## 7. Sign-Off Decision

### Decision

- [ ] **ACCEPTED** -- The release meets acceptance criteria and is approved for production deployment.
- [x] **CONDITIONALLY ACCEPTED** -- The release is approved with the conditions listed below.
- [ ] **REJECTED** -- The release does not meet acceptance criteria. Issues listed above must be resolved.

### Conditions

1. **Arabic PDF rendering fix (DEF-003) must be delivered in patch Release 1.0.1 within 2 weeks of go-live.** Arabic-speaking clients must not receive truncated reports. Until the fix is deployed, the operations team will generate English-only PDFs and manually attach Arabic annotations for affected clients.
2. **Concurrency test cases (TC-014 and related) must be validated against PostgreSQL staging before enabling the multi-user project editing feature flag in production.** The feature flag `ENABLE_MULTI_USER_EDIT` must remain disabled until validation is complete.

---

## 8. Approvals

| Role | Name | Decision | Signature | Date |
|------|------|----------|-----------|------|
| Product Owner | Fatima Hassan | Conditionally Accepted | F. Hassan | 2026-02-27 |
| Senior Field Engineer | Khalid Barakat | Accepted | K. Barakat | 2026-02-26 |
| Field Engineer | Yusuf Darwish | Accepted | Y. Darwish | 2026-02-26 |
| Field Engineer | Layla Omari | Accepted | L. Omari | 2026-02-26 |
| Tech Lead | Omar Khalil | Acknowledged | O. Khalil | 2026-02-27 |
| QA Lead | Nadia Al-Rashid | Acknowledged | N. Al-Rashid | 2026-02-27 |

---

**By signing this document, the undersigned confirm that the software has been tested against the defined acceptance criteria and the decision above reflects the assessment of the testing team and business stakeholders.**

---

## Completion Checklist

- [x] UAT Information filled in with release and environment details
- [x] All features listed with acceptance criteria results
- [x] Each feature's acceptance criteria individually verified
- [x] UAT test results tallied
- [x] Issues found during UAT documented with resolution status
- [x] Known limitations listed with workarounds
- [x] Business readiness items assessed
- [x] Sign-off decision selected (Conditionally Accepted)
- [x] Conditions listed for conditional acceptance
- [x] All required approvals obtained with signatures and dates

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Execute Test Cycle | [../../phase-6-testing/runbooks/execute-test-cycle.md](../../phase-6-testing/runbooks/execute-test-cycle.md) |
| Template | UAT Sign-Off Template | [../../phase-6-testing/templates/uat-sign-off-template.md](../../phase-6-testing/templates/uat-sign-off-template.md) |
| Artifact | Test Plan | [test-plan.md](test-plan.md) |
| Artifact | Test Cases | [test-cases.md](test-cases.md) |
| Artifact | Defect Reports | [defect-reports.md](defect-reports.md) |
| Artifact | Test Summary Report | [test-summary-report.md](test-summary-report.md) |
