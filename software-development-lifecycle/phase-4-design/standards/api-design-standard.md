# API Design Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P4-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Design Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** URL structure, HTTP methods, error format required; idempotency keys optional
> **IF** medium project (3-5 devs) **THEN** Full compliance; versioning support window may be reduced to 3 months
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### URL Structure

URL pattern: `https://{host}/api/v{version}/{resource}`

| Element | Convention | Example |
|---------|-----------|---------|
| Base path | /api/v{N}/ | /api/v1/ |
| Resource name | Plural noun, kebab-case | /api/v1/rental-agreements |
| Resource instance | /{resource}/{id} | /api/v1/rental-agreements/ra-001 |
| Sub-resource | /{resource}/{id}/{sub-resource} | /api/v1/rental-agreements/ra-001/line-items |
| Action (non-CRUD, use sparingly) | /{resource}/{id}/{action} | /api/v1/rental-agreements/ra-001/cancel |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Resource names are plural nouns in kebab-case | All endpoints | [ ] URL audit against convention table | Reject API spec |
| 2 | Base path includes version: /api/v{N}/ | All endpoints | [ ] Version prefix present | Reject API spec |
| 3 | Non-CRUD actions used sparingly and documented | Action endpoints | [ ] Justification for each action endpoint | Rework API spec |

### HTTP Methods

| Method | Purpose | Idempotent | Request Body | Response Code |
|--------|---------|-----------|-------------|---------------|
| GET | Retrieve resource(s) | Yes | No | 200 |
| POST | Create a new resource | No | Yes | 201 |
| PUT | Replace resource entirely | Yes | Yes | 200 |
| PATCH | Update specific fields | No | Yes (partial) | 200 |
| DELETE | Remove a resource | Yes | No | 204 |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 4 | HTTP methods match purpose per table above | All endpoints | [ ] Method/purpose alignment checked | Reject API spec |
| 5 | Response codes match table above | All endpoints | [ ] Status codes verified | Reject API spec |

### Request/Response Format

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 6 | All JSON fields use snake_case | All request/response bodies | [ ] Field naming audit | Reject API spec |
| 7 | Dates use ISO 8601 (date: `2026-03-01`, datetime: `2026-03-01T08:00:00Z` UTC, duration: `P14D`) | All date/time fields | [ ] Date format validated | Reject API spec |
| 8 | All list endpoints support pagination (`page`, `per_page`) | All list endpoints | [ ] Pagination params present | Reject API spec |
| 9 | Pagination defaults: page=1, per_page=25, max per_page=100 | All list endpoints | [ ] Defaults documented | Reject API spec |
| 10 | Response includes pagination metadata (page, per_page, total_items, total_pages) | All list responses | [ ] Metadata in response schema | Reject API spec |
| 11 | Filtering via query parameters | All list endpoints | [ ] Filter params documented | Rework API spec |
| 12 | Sorting via `sort` parameter, prefix `-` for descending | All list endpoints | [ ] Sort param documented | Rework API spec |

### Error Response Format

Structure:

```json
{
  "error": {
    "code": "SCREAMING_SNAKE_CASE",
    "message": "Human-readable description",
    "details": [{"field": "...", "message": "..."}]
  }
}
```

| Field | Required |
|-------|----------|
| error.code | Yes |
| error.message | Yes |
| error.details | No (for validation failures) |

### Standard Error Codes

| HTTP Status | Error Code | When to Use |
|------------|-----------|-------------|
| 400 | VALIDATION_ERROR | Request body fails validation |
| 400 | INVALID_PARAMETER | Query parameter is invalid |
| 401 | AUTHENTICATION_REQUIRED | No valid JWT token provided |
| 403 | PERMISSION_DENIED | Valid token, insufficient permissions |
| 404 | RESOURCE_NOT_FOUND | Resource does not exist |
| 409 | CONFLICT | Action conflicts with current state |
| 422 | BUSINESS_RULE_VIOLATION | Request violates business rule |
| 429 | RATE_LIMIT_EXCEEDED | Too many requests |
| 500 | INTERNAL_ERROR | Unhandled server error |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 13 | Error responses follow standard structure (code, message, optional details) | All error responses | [ ] Error schema validated | Reject API spec |
| 14 | Error codes use SCREAMING_SNAKE_CASE from standard codes table | All error responses | [ ] Error codes match table | Reject API spec |

### Authentication and Authorization

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 15 | All endpoints require JWT in Authorization header (`Bearer {token}`) | All endpoints | [ ] Auth header required in spec | Block deployment |
| 16 | Public endpoints (health check, login) explicitly whitelisted | Public endpoints | [ ] Whitelist documented | Block deployment |
| 17 | Each endpoint documents required role(s) | All endpoints | [ ] Roles specified per endpoint | Reject API spec |

### Versioning

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 18 | Version in URL path: /api/v1/, /api/v2/ | All endpoints | [ ] Version in path | Reject API spec |
| 19 | Increment version only for breaking changes (removing fields, changing types, removing endpoints) | Version changes | [ ] Breaking change justified | Reject version bump |
| 20 | Non-breaking changes (adding optional fields, new endpoints) do NOT increment version | Additive changes | [ ] No unnecessary version bump | Revert version change |
| 21 | Previous version supported for 6 months after new version release | Deprecated versions | [ ] Support window documented | Escalate to Tech Lead |
| 22 | Deprecated endpoints include `Deprecation` response header | Deprecated endpoints | [ ] Header present | Block deployment |

### Idempotency

| Method | Naturally Idempotent | Idempotency Key Required |
|--------|---------------------|-------------------------|
| GET | Yes | No |
| PUT | Yes | No |
| DELETE | Yes | No |
| POST | No | Yes, for financial operations |
| PATCH | No | Recommended for critical operations |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 23 | POST endpoints for financial operations (invoices, payments) require `Idempotency-Key` header | Financial POST endpoints | [ ] Idempotency-Key in spec | Block deployment |
| 24 | PATCH endpoints for critical operations include Idempotency-Key recommendation | Critical PATCH endpoints | [ ] Idempotency-Key documented | Rework API spec |

---

## COMPLIANCE CHECKLIST

- [ ] All URLs follow `/api/v{N}/{resource}` pattern with plural kebab-case nouns
- [ ] HTTP methods and response codes match standard table
- [ ] All JSON fields use snake_case
- [ ] All dates/times use ISO 8601 (UTC for datetimes)
- [ ] All list endpoints support pagination with metadata
- [ ] Filtering and sorting parameters documented
- [ ] Error responses follow standard structure with standard error codes
- [ ] All endpoints require JWT (public endpoints explicitly whitelisted)
- [ ] Required roles documented per endpoint
- [ ] API version in URL path
- [ ] Breaking changes increment version; non-breaking changes do not
- [ ] Deprecated endpoints include Deprecation header
- [ ] Financial POST endpoints require Idempotency-Key header

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Design API Contracts | Runbook | ../runbooks/design-api-contracts.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
| API Specification | Template | ../templates/api-specification.md |
| Design Review Checklist | Template | ../templates/design-review-checklist.md |
