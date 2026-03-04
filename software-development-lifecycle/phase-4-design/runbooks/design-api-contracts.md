# Design API Contracts

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P4-002 |
| **Owner** | Developer |
| **Accountable** | Tech Lead |
| **SLA** | 3 business days per API resource |
| **Escalation** | Tech Lead (technical), Product Owner (scope) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Architecture defines which component exposes which APIs
- [ ] SRS requirements mapped to this component
- [ ] API Design Standard reviewed
- [ ] API Specification Template obtained

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Component API ownership unclear in ADD | STOP. Clarify component boundaries | Tech Lead |
| Requirements not mapped to component | STOP. Complete requirement mapping | Tech Lead |
| API Design Standard not available | STOP. Obtain standard before proceeding | Tech Lead |
| Conflicting API contracts from another component | STOP. Resolve ownership conflict | Tech Lead |

---

## PROCEDURE

### Step 1: Identify Resources

| Action | Owner | SLA |
|--------|-------|-----|
| Map each SRS requirement to a REST resource | Developer | 2 hours |
| Define resource name, URL pattern, and description | Developer | 1 hour |

- [ ] Every requirement mapped to at least one resource
- [ ] Resource URLs follow API Design Standard naming conventions
- [ ] No duplicate resources across components

> **IF** requirement spans multiple resources **THEN** document all resources and their relationship
> **ELSE IF** requirement cannot map to a REST resource **THEN** escalate to Tech Lead for alternative pattern (event, RPC)
> **ELSE** proceed to Step 2

### Step 2: Define Endpoints per Resource

| Action | Owner | SLA |
|--------|-------|-----|
| List all CRUD endpoints per resource | Developer | 2 hours |
| List all action endpoints per resource | Developer | 1 hour |
| Assign required roles per endpoint | Developer | 1 hour |

- [ ] All CRUD operations defined (GET list, GET single, POST, PUT, PATCH, DELETE)
- [ ] Action endpoints defined for non-CRUD operations
- [ ] HTTP methods correct per API Design Standard
- [ ] Required roles assigned per endpoint

> **IF** resource needs only read operations **THEN** define GET endpoints only, document why writes are excluded
> **ELSE IF** resource needs custom actions (e.g., /return, /cancel) **THEN** use POST with action sub-resource
> **ELSE** define full CRUD set

### Step 3: Design Request/Response Schemas

| Action | Owner | SLA |
|--------|-------|-----|
| Define request body schema for each write endpoint | Developer | 3 hours |
| Define response body schema for each endpoint | Developer | 3 hours |
| Specify field types, required/optional, constraints | Developer | 2 hours |

- [ ] Request schema defined for every POST/PUT/PATCH endpoint
- [ ] Response schema defined for every endpoint
- [ ] Field types specified (string, number, UUID, ISO 8601 date, etc.)
- [ ] Required vs optional fields marked
- [ ] Constraints documented (max length, min/max value, regex pattern)
- [ ] Response includes standard fields (id, created_at, updated_at)

> **IF** response contains nested objects **THEN** define sub-schemas separately
> **ELSE IF** field type is ambiguous **THEN** clarify with Tech Lead before proceeding
> **ELSE** proceed to Step 4

### Step 4: Define Error Responses

| Action | Owner | SLA |
|--------|-------|-----|
| List all possible error conditions per endpoint | Developer | 2 hours |
| Map each error to HTTP status code and error code | Developer | 1 hour |

- [ ] 400 VALIDATION_ERROR defined for invalid input
- [ ] 401 AUTHENTICATION_REQUIRED defined for unauthenticated access
- [ ] 403 PERMISSION_DENIED defined for unauthorized roles
- [ ] 404 RESOURCE_NOT_FOUND defined for missing entities
- [ ] 409 CONFLICT defined for state conflicts
- [ ] 422 BUSINESS_RULE_VIOLATION defined for business rule failures
- [ ] Error response body follows API Design Standard format

> **IF** endpoint can produce 500-level errors **THEN** document recovery behavior and retry guidance
> **ELSE** proceed to Step 5

### Step 5: Document Query Parameters

| Action | Owner | SLA |
|--------|-------|-----|
| Define pagination parameters for list endpoints | Developer | 1 hour |
| Define filter parameters for list endpoints | Developer | 1 hour |
| Define sort parameters for list endpoints | Developer | 30 min |

- [ ] Pagination defined (page, per_page with defaults and max)
- [ ] Filter parameters defined with types and allowed values
- [ ] Sort parameter defined with allowed fields and default
- [ ] Date range filters defined where applicable

> **IF** endpoint has no list operation **THEN** skip this step
> **ELSE** proceed to Step 6

### Step 6: Document Authentication Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| Specify auth requirement per endpoint | Developer | 1 hour |
| Specify required roles per endpoint | Developer | 30 min |
| Document special headers (Idempotency-Key, etc.) | Developer | 30 min |

- [ ] Every endpoint has auth requirement documented (Yes/No)
- [ ] Every authenticated endpoint has allowed roles listed
- [ ] Special headers documented where required

### Step 7: Write OpenAPI Specification

| Action | Owner | SLA |
|--------|-------|-----|
| Produce OpenAPI 3.0 specification in YAML or JSON | Developer | 4 hours |
| Validate specification against API Design Standard | Developer | 1 hour |

- [ ] OpenAPI 3.0 spec produced
- [ ] All endpoints represented in spec
- [ ] All schemas represented in spec
- [ ] Spec validates without errors

> **IF** spec validation fails **THEN** fix errors and re-validate
> **ELSE** proceed to Step 8

### Step 8: Conduct Peer Review

| Action | Owner | SLA |
|--------|-------|-----|
| Share API specification with frontend developer or consumer team | Developer | 1 hour |
| Review for consistency, completeness, and usability | QA Lead | 2 business days |
| Confirm all SRS requirements covered | Developer | 2 hours |
| Update specification based on feedback | Developer | 1 business day |

- [ ] API spec shared with consumer team
- [ ] Consistency with API Design Standard verified
- [ ] Completeness verified (all requirements covered)
- [ ] Usability confirmed by consumer
- [ ] Feedback incorporated

> **IF** consumer requests breaking changes **THEN** assess impact and escalate to Tech Lead if scope changes
> **ELSE IF** consumer identifies missing endpoints **THEN** add endpoints and re-review
> **ELSE** proceed to Step 9

### Step 9: Create API Mock

| Action | Owner | SLA |
|--------|-------|-----|
| Set up mock server returning example responses per endpoint | Developer | 4 hours |
| Verify mock responses match OpenAPI spec | Developer | 1 hour |

- [ ] Mock server running and accessible
- [ ] Example responses match OpenAPI spec schemas
- [ ] Frontend team notified of mock availability

---

## EXIT CRITERIA

- [ ] All SRS requirements mapped to API resources
- [ ] All endpoints defined with methods, URLs, and roles
- [ ] Request/response schemas defined with types, required fields, constraints
- [ ] Error responses defined for every endpoint
- [ ] Query parameters documented for all list endpoints
- [ ] Authentication requirements documented per endpoint
- [ ] OpenAPI 3.0 specification written and validated
- [ ] Peer reviewed by API consumer
- [ ] API mock created and available for frontend development

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| API Specification Document | [API Specification Template](../templates/api-specification.md) | Project repository /docs/design/api/ |
| OpenAPI 3.0 Spec (YAML/JSON) | -- | Project repository /api/openapi/ |
| API Mock Server Config | -- | Project repository /mocks/ |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| API Design Standard | Standard | [../standards/api-design-standard.md](../standards/api-design-standard.md) |
| API Specification Template | Template | [../templates/api-specification.md](../templates/api-specification.md) |
| Create Detailed Design | Runbook | [create-detailed-design.md](create-detailed-design.md) |
| Design Data Models | Runbook | [design-data-models.md](design-data-models.md) |
| Conduct Design Review | Runbook | [conduct-design-review.md](conduct-design-review.md) |
