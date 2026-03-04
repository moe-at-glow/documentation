# HTTP Status Codes Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P4-003 |
| **Use When** | Selecting the correct HTTP status code for an API response |
| **Last Updated** | 2026-03-04 |

---

## 2xx Success

| Code | Name | When to Use | GlowPowerRental Example |
|------|------|------------|------------------------|
| 200 | OK | Successful GET, PUT, PATCH, or action endpoint | GET /api/v1/rentals/ra-042 returns rental details |
| 201 | Created | Successful POST that creates a resource | POST /api/v1/rentals creates new rental, returns created object |
| 202 | Accepted | Request accepted for async processing | POST /api/v1/reports/generate accepted, report will be generated in background |
| 204 | No Content | Successful DELETE or action with no response body | DELETE /api/v1/rentals/ra-042 soft-deletes rental, no body returned |

## 3xx Redirection

| Code | Name | When to Use | GlowPowerRental Example |
|------|------|------------|------------------------|
| 301 | Moved Permanently | Resource URL has permanently changed | API version v1 endpoint moved to v2 |
| 304 | Not Modified | Conditional GET: resource has not changed since If-None-Match | Cached equipment list has not changed |

## 4xx Client Error

| Code | Name | When to Use | GlowPowerRental Example |
|------|------|------------|------------------------|
| 400 | Bad Request | Malformed request syntax or invalid parameters | Missing required field, invalid date format |
| 401 | Unauthorized | No authentication token or token is invalid/expired | Request without JWT, expired token |
| 403 | Forbidden | Valid token but insufficient permissions | Readonly user tries to create a rental |
| 404 | Not Found | Resource does not exist | GET /api/v1/rentals/ra-999 where ra-999 does not exist |
| 409 | Conflict | Action conflicts with current state | Canceling an already-returned rental, equipment double-booked |
| 422 | Unprocessable Entity | Request is syntactically valid but violates business rules | end_date before start_date, negative daily_rate |
| 429 | Too Many Requests | Rate limit exceeded | More than 100 requests per minute from same client |

## 5xx Server Error

| Code | Name | When to Use | GlowPowerRental Example |
|------|------|------------|------------------------|
| 500 | Internal Server Error | Unhandled server error (catch-all) | Null pointer, unhandled exception. Log full error server-side. |
| 502 | Bad Gateway | Upstream service returned invalid response | SAP B1 API returns malformed response |
| 503 | Service Unavailable | System is temporarily unable to handle requests | Database connection pool exhausted, maintenance window |

---

## RULES

1. Never return 200 for an error. Use 4xx or 5xx.
2. Never return 500 for a client error. Use 4xx.
3. Always include an error response body with code and message for 4xx and 5xx.
4. Log 5xx errors server-side with full stack trace. Never expose stack traces to clients.
5. Return the most specific applicable status code. Prefer 422 over 400 for business rule violations.

---

## DECISION TREE

### Which HTTP status code to return?

```
IF request succeeded
  IF request was GET, PUT, or PATCH
    THEN return 200 OK
  ELSE IF request was POST that created a resource
    THEN return 201 Created
  ELSE IF request was accepted for async processing
    THEN return 202 Accepted
  ELSE IF request was DELETE or action with no response body
    THEN return 204 No Content

ELSE IF error is caused by the CLIENT
  IF request is malformed (bad syntax, invalid parameters)
    THEN return 400 Bad Request
  ELSE IF no auth token or token is invalid/expired
    THEN return 401 Unauthorized
  ELSE IF valid token but insufficient permissions
    THEN return 403 Forbidden
  ELSE IF resource does not exist
    THEN return 404 Not Found
  ELSE IF action conflicts with current resource state
    THEN return 409 Conflict
  ELSE IF request is syntactically valid but violates business rules
    THEN return 422 Unprocessable Entity
  ELSE IF rate limit exceeded
    THEN return 429 Too Many Requests

ELSE IF error is caused by the SERVER
  IF upstream service returned invalid response
    THEN return 502 Bad Gateway
  ELSE IF system temporarily unavailable (DB pool exhausted, maintenance)
    THEN return 503 Service Unavailable
  ELSE
    THEN return 500 Internal Server Error (catch-all)
```

### 400 vs 422: Which one?

```
IF request cannot be parsed (malformed JSON, wrong content type, missing required field)
  THEN return 400 Bad Request
ELSE IF request parses correctly but violates business rules (invalid date range, negative amount)
  THEN return 422 Unprocessable Entity
```

### 401 vs 403: Which one?

```
IF caller has no token or token is invalid/expired
  THEN return 401 Unauthorized
ELSE IF caller has a valid token but lacks permission for this action
  THEN return 403 Forbidden
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Detailed Design | Runbook | ../runbooks/create-detailed-design.md |
| Design API Contracts | Runbook | ../runbooks/design-api-contracts.md |
| Design Data Models | Runbook | ../runbooks/design-data-models.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
