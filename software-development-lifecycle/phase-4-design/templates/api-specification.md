# API Specification

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-002 |
| **When to Use** | Defining REST API contracts for each resource |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per resource |
| **Runbook** | ../runbooks/design-api-contracts.md |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Query Parameters section optional; one example per endpoint sufficient
> **IF** medium project (3-5 devs) **THEN** All sections required; error responses can list top 3 codes only
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Resource: [Resource Name]

Base URL: `/api/v1/[resource-name]`

---

## [ ] Endpoints

### [ ] [METHOD] /api/v1/[resource-name]

| Field | Value |
|-------|-------|
| Description | [What this endpoint does] |
| Authentication | Required (JWT Bearer) |
| Roles | [admin, operator, readonly] |
| Idempotency Key | Required / Not required |

#### [ ] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| [param] | path/query/body | string/number/boolean | Yes/No | [Description] | [Min, max, pattern] |

#### [ ] Request Body Example

```json
{
  "field_name": "value"
}
```

#### [ ] Response (2XX)

| Field | Type | Description |
|-------|------|-------------|
| [field] | string/number/boolean | [Description] |

#### [ ] Response Example

```json
{
  "field_name": "value"
}
```

#### [ ] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 400 | VALIDATION_ERROR | [When this error occurs] |
| 404 | RESOURCE_NOT_FOUND | [When this error occurs] |

---

### [ ] [METHOD] /api/v1/[resource-name]/:id

[Repeat the above structure for each endpoint]

---

## [ ] Query Parameters (List Endpoint)

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| page | integer | 1 | Page number |
| per_page | integer | 25 | Items per page (max 100) |
| sort | string | -created_at | Sort field |
| [filter] | [type] | (none) | [Filter description] |

---

## [ ] Related Requirements

| Endpoint | Requirement |
|---------|-------------|
| [METHOD /path] | [SWR-XXX] |

---

## COMPLETION CHECKLIST

- [ ] Resource name and base URL defined
- [ ] All endpoints documented with method, path, and description
- [ ] Authentication and role requirements specified per endpoint
- [ ] Request parameters documented with types, constraints, and required flags
- [ ] Request body examples provided for POST/PUT/PATCH endpoints
- [ ] Response schemas and examples provided for all success codes
- [ ] Error responses listed with status codes and conditions
- [ ] Query parameters defined for list endpoints (pagination, sorting, filtering)
- [ ] Idempotency requirements specified for write operations
- [ ] All endpoints traced to SWR requirements
- [ ] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Parent component design | ./detailed-design-document.md |
| Data Model Document | Underlying data structures | ./data-model-document.md |
| Design Review Checklist | Review gate for API design | ./design-review-checklist.md |
| Design API Contracts Runbook | Step-by-step procedure | ../runbooks/design-api-contracts.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../../phase-2-requirements-engineering/templates/software-requirements-specification.md |
