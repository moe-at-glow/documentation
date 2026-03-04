# Pull Request Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P5-001 |
| **When to Use** | Creating a pull request for any code change |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 30 minutes to submit; review within 4 hours |
| **Runbook** | [Implement Feature Runbook](../runbooks/implement-feature.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| PR Size | Action |
|---------|--------|
| **< 100 lines** | Single reviewer, fast-track |
| **100-400 lines** | Standard review, one reviewer minimum |
| **400-800 lines** | Two reviewers required, split if possible |
| **> 800 lines** | STOP. Split into smaller PRs before submitting |

---

## [ ] PR Title

```
<type>(<scope>): <short description>
```

Example: `feat(billing): add late fee calculation`

---

## [ ] Description

### [ ] What

<!-- What does this PR do? One or two sentences. -->


### [ ] Why

<!-- What ticket, requirement, or problem does this address? -->

Refs: TICKET-NNN

### [ ] How

<!-- Brief summary of the approach. Highlight any non-obvious decisions. -->


---

## [ ] Changes

<!-- List the key changes. Group by file or area if helpful. -->

- [ ] Change 1
- [ ] Change 2
- [ ] Change 3

---

## [ ] Related Documents

<!-- Link to the relevant design documents. -->

- DDD: <!-- link or path -->
- API Spec: <!-- link or path -->
- ADR: <!-- link or path, if applicable -->

---

## [ ] Test Plan

### [ ] Automated Tests

<!-- What tests were added or modified? -->

- [ ] Unit tests for <!-- describe what is tested -->
- [ ] Edge case tests for <!-- describe edge cases -->

### [ ] Manual Testing

<!-- Steps to manually verify, if applicable. -->

1. Start the development server: `npm run dev`
2. <!-- Step 2 -->
3. <!-- Step 3 -->
4. Verify: <!-- expected result -->

### [ ] Test Results

```
<!-- Paste test output or coverage summary -->
npm test

Tests:  X passed, X total
Coverage: XX% statements, XX% branches, XX% functions, XX% lines
```

---

## [ ] Author Checklist

- [ ] I have read the ticket and the related DDD
- [ ] My code matches the approved design
- [ ] I have written tests first (TDD)
- [ ] All tests pass (`npm test`)
- [ ] Linter passes (`npm run lint`)
- [ ] I have self-reviewed my diff (`git diff develop`)
- [ ] No debug code, console.log, or commented-out code
- [ ] No hardcoded configuration values
- [ ] No secrets or sensitive data in code
- [ ] Commit messages follow conventional commit format
- [ ] PR is under 400 lines of diff

## [ ] Reviewer Checklist

- [ ] PR description is clear and complete
- [ ] Tests reviewed first (understood expected behavior)
- [ ] Implementation matches the linked DDD
- [ ] Security concerns checked (input validation, auth, SQL injection)
- [ ] Performance concerns checked (N+1, pagination, indexes)
- [ ] Error handling is appropriate
- [ ] Naming follows coding standards

---

## [ ] Screenshots / Diagrams

<!-- If this PR includes UI changes or architecture changes, include screenshots or diagrams. -->

---

## [ ] Notes for Reviewer

<!-- Any specific areas you want the reviewer to focus on? Any concerns or trade-offs? -->

<!-- Suggested reading order: -->
<!-- 1. Start with tests: `src/modules/.../tests/...` -->
<!-- 2. Then read implementation: `src/modules/.../...` -->

---

## Completion Checklist

- [ ] PR title follows conventional commit format
- [ ] Description (what, why, how) filled in
- [ ] Changes listed
- [ ] Related documents linked
- [ ] Test plan documented with results
- [ ] Author checklist completed — all items checked
- [ ] Screenshots attached (if UI/architecture change)
- [ ] Reviewer notes provided
- [ ] PR submitted and reviewer assigned

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Implement Feature Runbook | [../runbooks/implement-feature.md](../runbooks/implement-feature.md) | Parent runbook |
| Code Review Checklist | [code-review-checklist.md](code-review-checklist.md) | Reviewer uses this during review |
| Technical Debt Register | [technical-debt-register.md](technical-debt-register.md) | Log debt identified during PR |
