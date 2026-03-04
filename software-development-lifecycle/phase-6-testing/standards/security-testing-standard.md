# Security Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P6-004 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead |
| **Verification Method** | Test Review / CI Pipeline |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Authentication, authorization, input validation, and dependency scanning required; penetration testing optional; OWASP checklist review at release only
> **IF** medium project (3-5 devs) **THEN** All categories required; penetration testing at major releases; quarterly dependency audit
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Authentication Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Login with valid credentials returns JWT with correct claims | All projects | [ ] Test execution log | PR blocked |
| 2 | Login with invalid credentials returns 401, no token, no information leakage | All projects | [ ] Test execution log | PR blocked |
| 3 | Login with SQL injection in credentials returns 401, no SQL execution | All projects | [ ] Test execution log | Release blocked |
| 4 | Expired tokens return 401 | All projects | [ ] Test execution log | PR blocked |
| 5 | Modified/tampered tokens return 401 | All projects | [ ] Test execution log | PR blocked |
| 6 | Missing token on protected endpoint returns 401 | All projects | [ ] Test execution log | PR blocked |
| 7 | Account locks after 5 failed login attempts | All projects | [ ] Test execution log | Release blocked |
| 8 | Password requirements enforced (minimum length, complexity) | All projects | [ ] Test execution log | PR blocked |

### Authorization Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 9 | User accessing own data returns 200 | All projects | [ ] Test execution log | PR blocked |
| 10 | User accessing another user's data returns 403 | All projects | [ ] Test execution log | PR blocked |
| 11 | Regular user accessing admin endpoint returns 403 | All projects | [ ] Test execution log | PR blocked |
| 12 | Horizontal privilege escalation blocked (changing ID in URL) | All projects | [ ] Test execution log | Release blocked |
| 13 | Vertical privilege escalation blocked (changing role claim in token) | All projects | [ ] Test execution log | Release blocked |
| 14 | IDOR prevented (cannot access resources by guessing IDs) | All projects | [ ] Test execution log | Release blocked |

### Input Validation Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 15 | SQL injection: parameterized queries prevent execution | All projects | [ ] Test execution log | Release blocked |
| 16 | XSS: output encoded, scripts not executed | All projects | [ ] Test execution log | Release blocked |
| 17 | Command injection: user input never reaches shell commands | All projects | [ ] Test execution log | Release blocked |
| 18 | Path traversal: cannot access files outside intended directory | All projects | [ ] Test execution log | Release blocked |
| 19 | Request size limits enforced; oversized requests rejected | All projects | [ ] Test execution log | PR blocked |
| 20 | Content-Type validation: only expected content types accepted | All projects | [ ] Test execution log | PR blocked |
| 21 | Malformed JSON returns 400, does not crash | All projects | [ ] Test execution log | PR blocked |

### Data Protection Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 22 | Passwords stored as hashes (bcrypt or argon2), not plaintext or MD5 | All projects | [ ] Code review + DB audit | Immediate remediation |
| 23 | No passwords, tokens, or PII in log output | All projects | [ ] Log audit | Immediate remediation |
| 24 | No password hashes, internal IDs, or stack traces in API responses | All projects | [ ] Test execution log | PR blocked |
| 25 | HTTPS enforced: HTTP redirects to HTTPS, HSTS header present | All projects | [ ] Security header scan | Deployment blocked |
| 26 | Secure cookies: HttpOnly, Secure, SameSite flags set | All projects | [ ] Security header scan | Deployment blocked |
| 27 | Data at rest encryption enabled for sensitive columns | Medium+ projects | [ ] Database config audit | Release blocked |

### API Security Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Rate limiting: excessive requests return 429 | All projects | [ ] Test execution log | Release blocked |
| 29 | CORS: only allowed origins accepted | All projects | [ ] Security header scan | Deployment blocked |
| 30 | Security headers present: X-Content-Type-Options, X-Frame-Options, CSP | All projects | [ ] Security header scan | Deployment blocked |
| 31 | Error responses contain no stack traces, internal paths, or system info | All projects | [ ] Test execution log | PR blocked |
| 32 | Only documented HTTP methods allowed (405 for others) | All projects | [ ] Test execution log | PR blocked |
| 33 | Old API versions properly deprecated or disabled | Medium+ projects | [ ] API version audit | Release blocked |

### Dependency Vulnerability Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 34 | `npm audit` reports no critical/high vulnerabilities | All projects | [ ] CI pipeline `npm audit` | PR blocked |
| 35 | Dependencies within supported versions | All projects | [ ] Dependency version audit | Sprint backlog item |
| 36 | No GPL or restricted licenses in production dependencies | All projects | [ ] License scan | PR blocked |

### OWASP Top 10 Coverage

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 37 | A01 Broken Access Control: authorization + IDOR tests pass | All projects | [ ] Test execution log | Release blocked |
| 38 | A02 Cryptographic Failures: data protection + password storage tests pass | All projects | [ ] Test execution log | Release blocked |
| 39 | A03 Injection: SQL injection + command injection + XSS tests pass | All projects | [ ] Test execution log | Release blocked |
| 40 | A04 Insecure Design: architecture review completed (Phase 3) | Medium+ projects | [ ] Phase 3 review artifact | Release blocked |
| 41 | A05 Security Misconfiguration: headers + CORS + error handling verified | All projects | [ ] Security scan | Release blocked |
| 42 | A06 Vulnerable Components: dependency scanning pass | All projects | [ ] CI pipeline report | Release blocked |
| 43 | A07 Auth Failures: authentication + brute force tests pass | All projects | [ ] Test execution log | Release blocked |
| 44 | A08 Data Integrity Failures: input validation + deserialization tests pass | All projects | [ ] Test execution log | Release blocked |
| 45 | A09 Logging Failures: log review + sensitive data in logs check pass | All projects | [ ] Log audit | Release blocked |
| 46 | A10 SSRF: server-side request validation verified | Medium+ projects | [ ] Test execution log | Release blocked |

### Automated Security Tests (CI)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 47 | `npm audit --production` runs on every PR | All projects | [ ] CI pipeline config | CI pipeline rework |
| 48 | ESLint security plugin runs on every PR | All projects | [ ] CI pipeline config | CI pipeline rework |

### Manual Security Testing

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 49 | OWASP checklist review: every release (QA Engineer + Tech Lead) | All projects | [ ] Review artifact | Release blocked |
| 50 | Penetration testing: quarterly or major release (security specialist) | Medium+ projects | [ ] Pentest report | Release blocked |
| 51 | Dependency audit review: every sprint (developer) | All projects | [ ] Sprint review notes | Backlog item created |
| 52 | Security header verification: every deployment (DevOps) | All projects | [ ] Deployment checklist | Deployment blocked |

### Severity Classification and SLAs

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 53 | Critical (active exploitation possible, data breach risk): fix immediately (< 4 hours) | All projects | [ ] Defect tracker SLA report | Escalation to management |
| 54 | High (significant vulnerability, exploitation requires effort): fix within 1 business day | All projects | [ ] Defect tracker SLA report | Escalation to Tech Lead |
| 55 | Medium (vulnerability exists, exploitation limited): fix within current sprint | All projects | [ ] Sprint review | Carry to next sprint with justification |
| 56 | Low (minor concern, defense-in-depth): fix in next sprint | All projects | [ ] Backlog review | Accepted |

### Security Test Data Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 57 | Use OWASP testing guide payloads for injection tests | All projects | [ ] Test payload review | Test rework |
| 58 | Never test against production; use staging or dedicated security test environment | All projects | [ ] Environment audit | Immediate escalation |
| 59 | Document all test payloads with results | All projects | [ ] Test documentation review | Report revision required |
| 60 | No real credentials in tests; use test accounts only | All projects | [ ] Test code review | Immediate remediation |

### Security Finding Report Format

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 61 | Each finding includes: Finding ID (SEC-NNN), OWASP category, severity, description, steps to reproduce, impact, recommendation, status | All projects | [ ] Finding report review | Report revision required |

---

## COMPLIANCE CHECKLIST

- [ ] Authentication tests pass (valid/invalid credentials, token expiration, tampering, brute force)
- [ ] Authorization tests pass (own data, other user's data, admin endpoints, IDOR)
- [ ] Input validation tests pass (SQL injection, XSS, command injection, path traversal)
- [ ] Passwords stored as bcrypt/argon2 hashes
- [ ] No sensitive data in logs or API responses
- [ ] HTTPS enforced with HSTS header
- [ ] Secure cookie flags set (HttpOnly, Secure, SameSite)
- [ ] Rate limiting returns 429 on excessive requests
- [ ] CORS configured for allowed origins only
- [ ] Security headers present (X-Content-Type-Options, X-Frame-Options, CSP)
- [ ] `npm audit --production` reports no critical/high vulnerabilities
- [ ] No GPL/restricted licenses in production dependencies
- [ ] All OWASP Top 10 categories tested
- [ ] No critical or high severity findings open
- [ ] Medium/low findings documented with fix plan or accepted risk rationale
- [ ] OWASP checklist reviewed by QA Engineer + Tech Lead
- [ ] Penetration test completed (quarterly/major release)
- [ ] Security headers verified on deployment
- [ ] All findings reported in SEC-NNN format

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Report and Track Defects | Runbook | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Perform Regression Testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Test Plan Template | Template | [../templates/test-plan-template.md](../templates/test-plan-template.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
