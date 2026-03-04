# Coding Standards

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P5-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Code Review / CI Pipeline / Linter |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Linter enforcement only; manual review of security practices
> **IF** medium project (3-5 devs) **THEN** Linter + CI enforcement; peer review of all rules
> **IF** large project (6+ devs) **THEN** Full compliance required; automated gates on all rules

---

## COMPLIANCE REQUIREMENTS

### CR-1: File Structure

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Module directory: `src/modules/[module-name]/` | All TS projects | [ ] Directory structure matches convention | Reject PR |
| 2 | Required files per module: `[module].controller.ts`, `[module].service.ts`, `[module].repository.ts`, `[module].entity.ts`, `[module].dto.ts`, `[module].validator.ts`, `[module].events.ts`, `[module].types.ts` | All modules | [ ] Module contains required files | Reject PR |
| 3 | Tests in `__tests__/` subdirectory per module | All modules | [ ] Test files in correct location | Reject PR |

### CR-2: Naming Conventions

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Files: kebab-case (`rental-service.ts`) | All files | [ ] Linter rule enforced | Reject PR |
| 2 | Classes: PascalCase (`RentalService`) | All classes | [ ] Linter rule enforced | Reject PR |
| 3 | Interfaces: PascalCase (`PaymentGateway`) | All interfaces | [ ] Linter rule enforced | Reject PR |
| 4 | Functions/Methods: camelCase (`calculateLateFee`) | All functions | [ ] Linter rule enforced | Reject PR |
| 5 | Variables: camelCase (`rentalAgreement`) | All variables | [ ] Linter rule enforced | Reject PR |
| 6 | Constants: SCREAMING_SNAKE_CASE (`MAX_RETRY_ATTEMPTS`) | All constants | [ ] Linter rule enforced | Reject PR |
| 7 | Enums: PascalCase name, SCREAMING_SNAKE_CASE values (`RentalStatus.ACTIVE`) | All enums | [ ] Linter rule enforced | Reject PR |
| 8 | Booleans: is/has/can/should prefix (`isOverdue`, `hasLateFee`) | All booleans | [ ] Code review check | Reject PR |
| 9 | Private fields: underscore prefix or # (`_repository`, `#cache`) | All private fields | [ ] Linter rule enforced | Reject PR |

### CR-3: Formatting

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Indentation: 2 spaces | All files | [ ] Prettier/ESLint enforced | Auto-fix in CI |
| 2 | Line length: 100 characters maximum | All files | [ ] Linter enforced | Auto-fix in CI |
| 3 | Semicolons: required | All files | [ ] Linter enforced | Auto-fix in CI |
| 4 | Quotes: single quotes for strings | All files | [ ] Linter enforced | Auto-fix in CI |
| 5 | Trailing commas: required in multiline objects/arrays | All files | [ ] Linter enforced | Auto-fix in CI |
| 6 | Braces: same line (K&R style) | All files | [ ] Linter enforced | Auto-fix in CI |

### CR-4: TypeScript Strictness

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | `strict: true` in tsconfig.json | All TS projects | [ ] CI compilation check | Build failure |
| 2 | `noImplicitAny: true` | All TS projects | [ ] CI compilation check | Build failure |
| 3 | `strictNullChecks: true` | All TS projects | [ ] CI compilation check | Build failure |
| 4 | `noUnusedLocals: true` | All TS projects | [ ] CI compilation check | Build failure |
| 5 | `noUnusedParameters: true` | All TS projects | [ ] CI compilation check | Build failure |

### CR-5: Import Ordering

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Order: (1) Node.js built-ins, (2) External packages, (3) Internal modules (absolute), (4) Local modules (relative) | All TS files | [ ] Linter rule enforced | Reject PR |

### CR-6: Error Handling

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Use specific error types with meaningful messages | All code | [ ] Code review check | Reject PR |
| 2 | Re-throw known errors; wrap unknown errors with context | All catch blocks | [ ] Code review check | Reject PR |
| 3 | Never silently swallow errors (empty catch blocks) | All code | [ ] Linter rule enforced | Reject PR |
| 4 | Log unknown errors with structured context before wrapping | All catch blocks | [ ] Code review check | Reject PR |

### CR-7: Async Patterns

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Use async/await, not raw `.then()` chains | All async code | [ ] Linter rule enforced | Reject PR |
| 2 | Use `Promise.all()` for independent parallel operations | All async code | [ ] Code review check | Request change |

### CR-8: Environment Variables

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Naming: SCREAMING_SNAKE_CASE (`DATABASE_URL`, `MQTT_BROKER_HOST`) | All env vars | [ ] Code review check | Reject PR |
| 2 | `.env` file never committed to git | All repos | [ ] `.gitignore` check | Reject PR immediately |
| 3 | `.env.example` checked into git with placeholder values | All repos | [ ] File existence check | Reject PR |
| 4 | Read env vars at startup, inject into config module | All apps | [ ] Code review check | Reject PR |
| 5 | Never log, expose in API, or include secrets in error messages | All code | [ ] Code review check | Reject PR; security escalation |

### CR-9: Logging

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | ERROR: operation failed, requires attention | All code | [ ] Code review check | Request change |
| 2 | WARN: unexpected but recoverable condition | All code | [ ] Code review check | Request change |
| 3 | INFO: significant business events only | All code | [ ] Code review check | Request change |
| 4 | DEBUG: detailed diagnostic information | All code | [ ] Code review check | Request change |
| 5 | Use structured logging with context objects (no string concatenation) | All log calls | [ ] Linter rule enforced | Reject PR |
| 6 | Never log: passwords, tokens, credit cards, full PII, env secrets, sensitive request bodies | All code | [ ] Code review check | Reject PR; security escalation |

### CR-10: Security Coding Practices

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Validate all external inputs at controller/boundary level | All endpoints | [ ] Code review check | Reject PR |
| 2 | Use parameterized queries; never concatenate user input into SQL | All DB queries | [ ] Code review + SAST | Reject PR; security escalation |
| 3 | Sanitize user-generated content before rendering in HTML | All UI output | [ ] Code review check | Reject PR |
| 4 | Run `npm audit` weekly; fix critical/high vulnerabilities immediately | All repos | [ ] CI pipeline check | Block deployment |
| 5 | Use environment variables for secrets; never hardcode in source | All code | [ ] Code review + secret scanner | Reject PR; security escalation |
| 6 | Verify JWT on every authenticated endpoint; check token expiry | All auth endpoints | [ ] Code review check | Reject PR |
| 7 | Check user role server-side before processing; never trust client-side claims | All authorized endpoints | [ ] Code review check | Reject PR |

### CR-11: Dependency Management

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Justify new dependencies in PR description | All PRs adding deps | [ ] Code review check | Reject PR |
| 2 | Use exact versions in package.json (no ^ or ~) for production deps | All production deps | [ ] CI check | Reject PR |
| 3 | Run `npm audit` in CI; fail build on critical vulnerabilities | All builds | [ ] CI pipeline check | Build failure |
| 4 | Evaluate bundle size impact for frontend dependencies; prefer tree-shakeable | Frontend deps | [ ] Code review check | Request change |
| 5 | Allowed licenses: MIT, Apache 2.0, BSD, ISC only; GPL requires legal review | All deps | [ ] License scanner in CI | Reject PR |

---

## COMPLIANCE CHECKLIST

- [ ] All files use kebab-case naming
- [ ] All classes, interfaces use PascalCase; functions, variables use camelCase
- [ ] Constants use SCREAMING_SNAKE_CASE
- [ ] Boolean variables have is/has/can/should prefix
- [ ] Formatting rules enforced by Prettier/ESLint (2-space indent, 100-char lines, single quotes, semicolons, trailing commas, K&R braces)
- [ ] TypeScript strict mode enabled with all strict flags
- [ ] Imports ordered: Node built-ins > external > internal absolute > local relative
- [ ] No empty catch blocks; all errors handled with specific types and context
- [ ] async/await used instead of .then() chains
- [ ] Environment variables in SCREAMING_SNAKE_CASE; .env excluded from git; .env.example committed
- [ ] Secrets never logged, exposed in API, or hardcoded
- [ ] Structured logging used with correct log levels
- [ ] No PII, passwords, tokens, or secrets in log output
- [ ] All external inputs validated at boundary
- [ ] Parameterized queries used for all database access
- [ ] JWT verified on all authenticated endpoints; roles checked server-side
- [ ] New dependencies justified in PR; exact versions pinned; license compliant
- [ ] `npm audit` passes with no critical/high vulnerabilities

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Implement Feature | Runbook | ../runbooks/implement-feature.md |
| Setup Development Environment | Runbook | ../runbooks/setup-development-environment.md |
| Conduct Code Review | Runbook | ../runbooks/conduct-code-review.md |
| Manage Technical Debt | Runbook | ../runbooks/manage-technical-debt.md |
| Pull Request Template | Template | ../templates/pull-request-template.md |
| Code Review Checklist | Template | ../templates/code-review-checklist.md |
| Technical Debt Register | Template | ../templates/technical-debt-register.md |
