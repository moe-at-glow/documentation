> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# API Specification

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-002 |
| **When to Use** | Defining REST API contracts for each resource |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per resource |
| **Runbook** | ../runbooks/design-api-contracts.md |
| **Last Verified** | 2025-10-10 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Query Parameters section optional; one example per endpoint sufficient
> **IF** medium project (3-5 devs) **THEN** All sections required; error responses can list top 3 codes only
> **IF** large project (6+ devs) **THEN** Full template required

**Selected:** Small project (1-2 devs)

---

## [x] Resource: Authentication

Base URL: `/api/auth`

---

### [x] POST /api/auth/login

| Field | Value |
|-------|-------|
| Description | Authenticate a user and return a JWT access token |
| Authentication | Not required (public endpoint) |
| Roles | N/A |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| username | body | string | Yes | User's username | 3-50 characters |
| password | body | string | Yes | User's password | 8-128 characters |

#### [x] Request Body Example

```json
{
  "username": "rami.haddad",
  "password": "S3cur3P@ssw0rd!"
}
```

#### [x] Response (200 OK)

| Field | Type | Description |
|-------|------|-------------|
| token | string | JWT access token (1 hour expiry) |
| user | object | Authenticated user details |
| user.user_id | integer | User's unique identifier |
| user.username | string | Username |
| user.email | string | User's email address |
| user.role | string | User role: `admin`, `operator`, or `readonly` |

#### [x] Response Example

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6InJhbWkuaGFkZGFkIiwicm9sZSI6ImFkbWluIiwiZXhwIjoxNjk3MDQ1NjAwfQ.abc123signature",
  "user": {
    "user_id": 1,
    "username": "rami.haddad",
    "email": "rami.haddad@glowpowerrental.com",
    "role": "admin"
  }
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 401 | INVALID_CREDENTIALS | Username or password is incorrect |
| 422 | VALIDATION_ERROR | Missing or malformed username/password fields |
| 429 | ACCOUNT_LOCKED | 5 failed login attempts within 15 minutes; account locked for 15 minutes |

**Error Response Example (401):**

```json
{
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "The username or password you entered is incorrect."
  }
}
```

**Error Response Example (429):**

```json
{
  "error": {
    "code": "ACCOUNT_LOCKED",
    "message": "Account locked due to 5 failed login attempts. Try again after 15 minutes.",
    "retry_after": 900
  }
}
```

---

## [x] Resource: Projects

Base URL: `/api/projects`

---

### [x] GET /api/projects

| Field | Value |
|-------|-------|
| Description | List all projects owned by the authenticated user, with optional filters |
| Authentication | Required (JWT Bearer) |
| Roles | admin, operator, readonly |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| Authorization | header | string | Yes | Bearer token | `Bearer {jwt}` |
| status | query | string | No | Filter by project status | One of: `draft`, `active`, `archived` |
| client_id | query | integer | No | Filter by associated client | Valid client_id |
| page | query | integer | No | Page number | Default: 1, min: 1 |
| per_page | query | integer | No | Results per page | Default: 25, max: 100 |

#### [x] Response (200 OK)

| Field | Type | Description |
|-------|------|-------------|
| projects | array | List of project summary objects |
| projects[].project_id | integer | Project unique identifier |
| projects[].project_name | string | Project name |
| projects[].prn | string | Power Rental Number |
| projects[].client_id | integer | Associated client ID |
| projects[].status | string | `draft`, `active`, or `archived` |
| projects[].voltage_level | string | Voltage level (e.g., `"400"`) |
| projects[].total_kw | number | Computed total load in kW |
| projects[].load_count | integer | Number of loads in the project |
| projects[].created_at | string | ISO 8601 timestamp |
| projects[].updated_at | string | ISO 8601 timestamp |
| pagination | object | Pagination metadata |
| pagination.page | integer | Current page number |
| pagination.per_page | integer | Items per page |
| pagination.total | integer | Total matching projects |
| pagination.pages | integer | Total pages |

#### [x] Response Example

```json
{
  "projects": [
    {
      "project_id": 42,
      "project_name": "Dubai Marina Festival 2025",
      "prn": "PRN-2025-0042",
      "client_id": 7,
      "status": "active",
      "voltage_level": "400",
      "total_kw": 1250.50,
      "load_count": 18,
      "created_at": "2025-09-15T08:30:00Z",
      "updated_at": "2025-10-01T14:22:00Z"
    },
    {
      "project_id": 38,
      "project_name": "Abu Dhabi Construction Site B",
      "prn": "PRN-2025-0038",
      "client_id": 3,
      "status": "draft",
      "voltage_level": "400",
      "total_kw": 0.0,
      "load_count": 0,
      "created_at": "2025-09-10T11:00:00Z",
      "updated_at": "2025-09-10T11:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "per_page": 25,
    "total": 2,
    "pages": 1
  }
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 401 | UNAUTHORIZED | Missing or expired JWT token |
| 422 | VALIDATION_ERROR | Invalid query parameter value (e.g., `status=invalid`) |

---

### [x] POST /api/projects

| Field | Value |
|-------|-------|
| Description | Create a new power project |
| Authentication | Required (JWT Bearer) |
| Roles | admin, operator |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| Authorization | header | string | Yes | Bearer token | `Bearer {jwt}` |
| project_name | body | string | Yes | Name of the project | 1-200 characters |
| prn | body | string | No | Power Rental Number | Pattern: `PRN-YYYY-NNNN` |
| client_id | body | integer | No | Associated client | Must be valid client_id |
| voltage_level | body | string | No | System voltage | Default: `"400"` |
| frequency | body | string | No | System frequency (Hz) | Default: `"50"` |
| power_factor | body | number | No | Default power factor | Default: 0.8, range: 0.01-1.0 |
| demand_factor | body | number | No | Demand factor | Default: 1.0, range: 0.01-1.0 |
| diversity_factor | body | number | No | Diversity factor | Default: 1.0, range: 0.01-1.0 |
| folder_id | body | integer | No | Folder to place project in | Must be valid folder owned by user |

#### [x] Request Body Example

```json
{
  "project_name": "Sharjah Expo Hall Power Plan",
  "prn": "PRN-2025-0051",
  "client_id": 12,
  "voltage_level": "400",
  "frequency": "50",
  "power_factor": 0.85,
  "demand_factor": 0.9,
  "diversity_factor": 0.8,
  "folder_id": 5
}
```

#### [x] Response (201 Created)

| Field | Type | Description |
|-------|------|-------------|
| project_id | integer | Newly created project ID |
| project_name | string | Project name |
| prn | string | Power Rental Number |
| client_id | integer | Associated client ID |
| voltage_level | string | Voltage level |
| frequency | string | Frequency |
| power_factor | number | Power factor |
| demand_factor | number | Demand factor |
| diversity_factor | number | Diversity factor |
| status | string | Always `"draft"` for new projects |
| folder_id | integer | Folder ID (nullable) |
| created_at | string | ISO 8601 timestamp |
| updated_at | string | ISO 8601 timestamp |

#### [x] Response Example

```json
{
  "project_id": 51,
  "project_name": "Sharjah Expo Hall Power Plan",
  "prn": "PRN-2025-0051",
  "client_id": 12,
  "voltage_level": "400",
  "frequency": "50",
  "power_factor": 0.85,
  "demand_factor": 0.9,
  "diversity_factor": 0.8,
  "status": "draft",
  "folder_id": 5,
  "created_at": "2025-10-10T09:15:00Z",
  "updated_at": "2025-10-10T09:15:00Z"
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 401 | UNAUTHORIZED | Missing or expired JWT token |
| 403 | FORBIDDEN | User role is `readonly` -- cannot create projects |
| 409 | DUPLICATE_PROJECT_NAME | User already has a project with this name |
| 422 | VALIDATION_ERROR | Invalid or missing required fields |

---

## [x] Resource: Loads

Base URL: `/api/loads`

---

### [x] POST /api/loads

| Field | Value |
|-------|-------|
| Description | Create a new electrical load within a project |
| Authentication | Required (JWT Bearer) |
| Roles | admin, operator |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| Authorization | header | string | Yes | Bearer token | `Bearer {jwt}` |
| project_id | body | integer | Yes | Project to add load to | Must be valid project owned by user |
| load_name | body | string | Yes | Name/description of the load | 1-200 characters |
| load_type | body | string | Yes | Type of load | One of: `lighting`, `motor`, `hvac`, `appliance`, `it_equipment`, `other` |
| quantity | body | integer | No | Number of identical loads | Default: 1, min: 1, max: 9999 |
| power_kw | body | number | No | Power in kilowatts | min: 0 |
| power_kva | body | number | No | Power in kVA | min: 0 |
| current_a | body | number | No | Current in amps | min: 0 |
| voltage_v | body | number | No | Voltage in volts | Default: 400, min: 1 |
| power_factor | body | number | No | Load power factor | Default: project PF, range: 0.01-1.0 |
| is_critical | body | boolean | No | Whether the load is critical | Default: false |

#### [x] Request Body Example

```json
{
  "project_id": 42,
  "load_name": "Stage Lighting Rig A",
  "load_type": "lighting",
  "quantity": 4,
  "current_a": 32,
  "voltage_v": 400,
  "power_factor": 0.95,
  "is_critical": true
}
```

**Note:** When `current_a` is provided but `power_kw` is not, the server computes:
- Three-phase kW = (32 x 400 x 1.732 x 0.95) / 1000 = **21.09 kW**
- kVA = 21.09 / 0.95 = **22.20 kVA**

#### [x] Response (201 Created)

| Field | Type | Description |
|-------|------|-------------|
| load_id | integer | Newly created load ID |
| project_id | integer | Parent project ID |
| load_name | string | Load name |
| load_type | string | Load type |
| quantity | integer | Quantity |
| power_kw | number | Computed or provided kW |
| power_kva | number | Computed or provided kVA |
| current_a | number | Current in amps |
| voltage_v | number | Voltage in volts |
| power_factor | number | Power factor |
| is_critical | boolean | Critical load flag |
| created_at | string | ISO 8601 timestamp |

#### [x] Response Example

```json
{
  "load_id": 187,
  "project_id": 42,
  "load_name": "Stage Lighting Rig A",
  "load_type": "lighting",
  "quantity": 4,
  "power_kw": 21.09,
  "power_kva": 22.20,
  "current_a": 32.0,
  "voltage_v": 400.0,
  "power_factor": 0.95,
  "is_critical": true,
  "created_at": "2025-10-10T09:30:00Z"
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 401 | UNAUTHORIZED | Missing or expired JWT token |
| 403 | FORBIDDEN | User does not own the project and is not admin |
| 404 | PROJECT_NOT_FOUND | Specified project_id does not exist |
| 422 | VALIDATION_ERROR | Invalid field values or missing required fields |

---

## [x] Resource: Client Requirements

Base URL: `/api/requirements`

---

### [x] POST /api/requirements/submit

| Field | Value |
|-------|-------|
| Description | Submit a new client power requirement (public-facing endpoint for client self-service) |
| Authentication | Not required (public endpoint) |
| Roles | N/A |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| client_name | body | string | Yes | Client company name | 1-200 characters |
| client_email | body | string | Yes | Client contact email | Valid email format |
| client_phone | body | string | No | Client phone number | 7-20 characters |
| event_name | body | string | Yes | Event or site name | 1-200 characters |
| event_date | body | string | Yes | Event date | ISO 8601 date (YYYY-MM-DD) |
| event_location | body | string | Yes | Event location | 1-300 characters |
| estimated_power_kw | body | number | No | Estimated total power needed | min: 0 |
| voltage_requirement | body | string | No | Voltage level needed | Default: `"400"` |
| description | body | string | No | Additional details | max: 5000 characters |

#### [x] Request Body Example

```json
{
  "client_name": "Al Habtoor Events LLC",
  "client_email": "events@alhabtoor.ae",
  "client_phone": "+971-4-555-0199",
  "event_name": "Dubai Winter Gala 2025",
  "event_date": "2025-12-15",
  "event_location": "Al Habtoor City, Sheikh Zayed Road, Dubai",
  "estimated_power_kw": 500,
  "voltage_requirement": "400",
  "description": "Outdoor gala event requiring stage lighting (200kW), sound systems (50kW), HVAC for tented areas (150kW), and catering equipment (100kW). Critical loads: stage lighting and sound."
}
```

#### [x] Response (201 Created)

| Field | Type | Description |
|-------|------|-------------|
| requirement_code | string | Unique code in format `PR{DDMMYYYY}-{seq}` |
| status | string | Always `"submitted"` |
| message | string | Confirmation message |

#### [x] Response Example

```json
{
  "requirement_code": "PR10102025-001",
  "status": "submitted",
  "message": "Your power requirement has been submitted successfully. Use code PR10102025-001 to track your request."
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 422 | VALIDATION_ERROR | Missing required fields or invalid format |

---

### [x] PUT /api/requirements/{id}/approve

| Field | Value |
|-------|-------|
| Description | Approve a submitted client requirement and optionally link to a project |
| Authentication | Required (JWT Bearer) |
| Roles | admin only |
| Idempotency Key | Not required |

#### [x] Request

| Parameter | Location | Type | Required | Description | Constraints |
|-----------|----------|------|----------|-------------|-------------|
| Authorization | header | string | Yes | Bearer token | `Bearer {jwt}` |
| id | path | integer | Yes | Requirement ID | Must exist |
| project_id | body | integer | No | Project to link this requirement to | Must be valid project_id |
| notes | body | string | No | Approval notes | max: 2000 characters |

#### [x] Request Body Example

```json
{
  "project_id": 51,
  "notes": "Approved. Created project PRN-2025-0051 for this requirement. Power estimate looks reasonable for outdoor gala scope."
}
```

#### [x] Response (200 OK)

| Field | Type | Description |
|-------|------|-------------|
| requirement_id | integer | Requirement ID |
| requirement_code | string | Requirement tracking code |
| status | string | Now `"approved"` |
| approved_by | integer | User ID of the approver |
| approved_at | string | ISO 8601 timestamp |
| project_id | integer | Linked project ID (nullable) |
| notes | string | Approval notes |

#### [x] Response Example

```json
{
  "requirement_id": 15,
  "requirement_code": "PR10102025-001",
  "status": "approved",
  "approved_by": 1,
  "approved_at": "2025-10-11T08:45:00Z",
  "project_id": 51,
  "notes": "Approved. Created project PRN-2025-0051 for this requirement. Power estimate looks reasonable for outdoor gala scope."
}
```

#### [x] Error Responses

| Status | Error Code | Condition |
|--------|-----------|-----------|
| 401 | UNAUTHORIZED | Missing or expired JWT token |
| 403 | FORBIDDEN | User role is not `admin` |
| 404 | REQUIREMENT_NOT_FOUND | Specified requirement ID does not exist |
| 409 | INVALID_STATUS | Requirement is not in `submitted` status (already approved/rejected) |

---

## [x] Standard Error Response Format

All error responses follow this structure:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error description.",
    "details": {}
  }
}
```

The `details` field is optional and included when validation errors provide field-level information:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed.",
    "details": {
      "project_name": "This field is required.",
      "power_factor": "Must be between 0.01 and 1.0."
    }
  }
}
```

---

## [x] Related Requirements

| Endpoint | Requirement |
|---------|-------------|
| POST /api/auth/login | SWR-001 (User authentication) |
| GET /api/projects | SWR-020 (List projects with computed totals) |
| POST /api/projects | SWR-022 (Create project with default status draft) |
| POST /api/loads | SWR-010, SWR-011 (Power calculations on load creation) |
| POST /api/requirements/submit | SWR-030 (Public requirement submission) |
| PUT /api/requirements/{id}/approve | SWR-031 (Admin requirement approval) |

---

## COMPLETION CHECKLIST

- [x] Resource name and base URL defined
- [x] All endpoints documented with method, path, and description
- [x] Authentication and role requirements specified per endpoint
- [x] Request parameters documented with types, constraints, and required flags
- [x] Request body examples provided for POST/PUT/PATCH endpoints
- [x] Response schemas and examples provided for all success codes
- [x] Error responses listed with status codes and conditions
- [x] Query parameters defined for list endpoints (pagination, sorting, filtering)
- [x] Idempotency requirements specified for write operations
- [x] All endpoints traced to SWR requirements
- [x] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Parent component design | ./detailed-design.md |
| Data Model Document | Underlying data structures | ./data-model.md |
| Design Review Checklist | Review gate for API design | ./design-review-checklist.md |
| Design API Contracts Runbook | Step-by-step procedure | ../../../phase-4-design/runbooks/design-api-contracts.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../../phase-2-requirements-engineering/software-requirements-specification.md |
