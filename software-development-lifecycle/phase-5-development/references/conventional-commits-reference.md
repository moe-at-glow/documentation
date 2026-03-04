# Conventional Commits Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P5-002 |
| **Use When** | Writing commit messages, reviewing commit history, determining version bumps |
| **Last Updated** | 2026-03-04 |

---

## FORMAT

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

---

## TYPES

| Type | When to Use | Bumps Version | Example |
|------|-------------|---------------|---------|
| `feat` | New feature or capability | Minor (1.x.0) | `feat(billing): add late fee calculation` |
| `fix` | Bug fix | Patch (1.0.x) | `fix(billing): correct rounding in fee calc` |
| `docs` | Documentation only | None | `docs(api): update rental endpoint examples` |
| `style` | Formatting, whitespace, semicolons (no logic change) | None | `style(billing): fix indentation in calculator` |
| `refactor` | Code change that neither fixes a bug nor adds a feature | None | `refactor(billing): extract fee rate to config` |
| `test` | Adding or updating tests | None | `test(billing): add edge case for zero-day fee` |
| `chore` | Build, tooling, CI, dependencies | None | `chore(deps): update jest to v30` |
| `perf` | Performance improvement | Patch (1.0.x) | `perf(rentals): add index on customer_id` |
| `ci` | CI/CD configuration changes | None | `ci: add lint step to PR pipeline` |
| `build` | Build system or external dependency changes | None | `build: update typescript to 5.4` |
| `revert` | Reverts a previous commit | Depends | `revert: feat(billing): add late fee calculation` |

---

## SCOPES

| Scope | Area |
|-------|------|
| `billing` | Invoicing, payments, fees |
| `rentals` | Rental agreements, lifecycle |
| `fleet` | Equipment, maintenance |
| `customers` | Customer management |
| `auth` | Authentication and authorization |
| `iot` | IoT telemetry, MQTT |
| `api` | General API changes |
| `db` | Database migrations, schema |
| `deps` | Dependency updates |
| `config` | Configuration changes |

If a change spans multiple scopes, use the primary scope or omit the scope.

---

## DESCRIPTION RULES

| Rule | Example |
|------|---------|
| Use imperative mood | "add late fee calculation" not "added" or "adds" |
| Lowercase first letter | "add late fee" not "Add late fee" |
| No period at end | "add late fee calculation" not "add late fee calculation." |
| Max 72 characters | Keep it concise |
| Explain what, not how | "add late fee calculation" not "create LateFeeCalculator class" |

---

## FOOTER TOKENS

| Footer | Purpose | Example |
|--------|---------|---------|
| `Refs: TICKET-NNN` | Links to the project tracker ticket | `Refs: TICKET-123` |
| `BREAKING CHANGE: <description>` | Indicates a breaking API change (bumps major version) | `BREAKING CHANGE: rental response now uses snake_case` |
| `Co-authored-by: Name <email>` | Credit co-authors | `Co-authored-by: Ali <ali@glowpower.sa>` |
| `Reviewed-by: Name <email>` | Credit reviewers | `Reviewed-by: Sara <sara@glowpower.sa>` |

---

## BREAKING CHANGES

Two ways to indicate (bumps **major** version X.0.0):

**Option 1 — Footer:**
```
feat(api): change rental response format

BREAKING CHANGE: All response fields now use snake_case instead of camelCase.
```

**Option 2 — Exclamation mark:**
```
feat(api)!: change rental response format
```

---

## SEMANTIC VERSIONING SUMMARY

| Version Part | Trigger | Example |
|-------------|---------|---------|
| Major (X.0.0) | `BREAKING CHANGE` or `!` after type | 1.0.0 → 2.0.0 |
| Minor (0.X.0) | `feat` type | 1.0.0 → 1.1.0 |
| Patch (0.0.X) | `fix` or `perf` type | 1.0.0 → 1.0.1 |
| None | `docs`, `style`, `refactor`, `test`, `chore`, `ci`, `build` | No version change |

---

## COMMON MISTAKES

| Mistake | Problem | Correct |
|---------|---------|---------|
| `Fixed the bug` | Past tense, no type/scope | `fix(billing): correct rounding error` |
| `feat: stuff` | Vague description | `feat(billing): add late fee calculation` |
| `feat(billing): Add Late Fee.` | Capital letter, period | `feat(billing): add late fee` |
| `update code` | No type, vague | `refactor(rentals): simplify status check` |
| `WIP` | Not a valid commit message | Do not commit WIP. Use branches. |

---

## DECISION TREE

### Which commit type should I use?

```
START — What does your change do?
  │
  ├─ IF it adds new functionality visible to users
  │    THEN use `feat`
  │    IF it also breaks existing API contracts
  │      THEN add `!` after type OR add BREAKING CHANGE footer
  │
  ├─ IF it fixes incorrect behavior (bug)
  │    THEN use `fix`
  │
  ├─ IF it improves performance without changing behavior
  │    THEN use `perf`
  │
  ├─ IF it restructures code without changing behavior or fixing a bug
  │    THEN use `refactor`
  │
  ├─ IF it only changes formatting / whitespace / semicolons
  │    THEN use `style`
  │
  ├─ IF it adds or modifies tests only
  │    THEN use `test`
  │
  ├─ IF it only changes documentation
  │    THEN use `docs`
  │
  ├─ IF it changes CI/CD pipeline configuration
  │    THEN use `ci`
  │
  ├─ IF it changes build system or external dependencies
  │    THEN use `build`
  │
  ├─ IF it updates tooling, deps, or other maintenance tasks
  │    THEN use `chore`
  │
  └─ IF it reverts a previous commit
       THEN use `revert`
       AND reference the original commit in the body
```

### Do I need a body?

```
START
  │
  ├─ IF the description line fully explains the change
  │    THEN body is optional
  │
  ├─ IF the change addresses multiple requirements
  │    THEN include body listing each requirement
  │
  ├─ IF the approach is non-obvious
  │    THEN include body explaining rationale
  │
  └─ IF there is a breaking change
       THEN include body describing migration steps
```

### Which scope should I use?

```
START — Which module does the change primarily affect?
  │
  ├─ IF it touches invoicing, payments, or fees → `billing`
  ├─ IF it touches rental agreements or lifecycle → `rentals`
  ├─ IF it touches equipment or maintenance → `fleet`
  ├─ IF it touches customer management → `customers`
  ├─ IF it touches auth or authorization → `auth`
  ├─ IF it touches IoT telemetry or MQTT → `iot`
  ├─ IF it touches general API layer → `api`
  ├─ IF it touches database migrations or schema → `db`
  ├─ IF it updates dependencies → `deps`
  ├─ IF it changes configuration → `config`
  │
  └─ IF it spans multiple scopes equally
       THEN use the primary scope OR omit scope entirely
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Implement Feature | Runbook | `../runbooks/implement-feature.md` |
| Git Workflow Standard | Standard | `../standards/git-workflow-standard.md` |
| Git Branching Strategy | Guide | `../guides/git-branching-strategy.md` |
| Development Artifacts Checklist | Reference | `./development-artifacts-checklist.md` |
| Pull Request Template | Template | `../templates/pull-request-template.md` |
