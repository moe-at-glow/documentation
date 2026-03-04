# Requirements Classification Standard

How to classify requirements at GlowPowerRental.

---

## Functional vs Non-Functional

| Type | Definition | Example |
|------|-----------|---------|
| Functional | What the system must do (behavior, features, operations) | The system shall generate an invoice when equipment is returned late |
| Non-Functional | How the system must perform (quality attributes, constraints) | The invoice generation API shall respond within 500ms under normal load |

Every requirement must be classified as either functional or non-functional.

---

## Non-Functional Requirement Categories

| Category | Definition | Example Requirement |
|----------|-----------|-------------------|
| Performance | Response time, throughput, resource usage | API response time under 200ms for 95th percentile |
| Security | Authentication, authorization, data protection, audit | All API endpoints require JWT authentication |
| Usability | Learnability, accessibility, user experience | New users complete equipment booking in under 3 minutes without training |
| Reliability | Availability, fault tolerance, recoverability | System availability of 99.5% measured monthly |
| Scalability | Load handling, growth accommodation | System handles 500 concurrent users without degradation |
| Maintainability | Modularity, testability, modifiability | Code coverage above 80% for all business logic modules |
| Compliance | Regulatory, legal, contractual obligations | System retains rental records for 7 years per Saudi commercial law |

---

## Priority Classification (MoSCoW)

| Priority | Code | Definition | Rule |
|----------|------|-----------|------|
| Must Have | M | Essential for the release to be viable. Without it, the system does not function or meet core business needs. | Cannot be descoped. Failure to deliver is a project failure. |
| Should Have | S | Important but not critical. The system works without it but with significant limitations. | Can be deferred to next release if necessary, but only with Product Owner approval. |
| Could Have | C | Desirable. Enhances user experience or operational efficiency but is not required. | Included only if time and budget allow. |
| Won't Have | W | Explicitly excluded from this release. Acknowledged as valid but not planned. | Documented to prevent scope creep and set expectations. |

Distribution guideline: approximately 60% Must Have, 20% Should Have, 20% Could Have.

---

## Risk Classification

| Risk Level | Definition | Action Required |
|------------|-----------|-----------------|
| High | Requirement is technically complex, depends on external systems, or has significant unknowns | Spike or proof of concept required before committing. Architecture review mandatory. |
| Medium | Requirement involves moderate complexity or some uncertainty | Tech lead review required. Identify mitigation plan. |
| Low | Requirement is well understood with established patterns | Standard development and review process. |

---

## Source Classification

| Source | Definition | Example |
|--------|-----------|---------|
| Stakeholder | Originates from a person or group with interest in the system | Operations manager requests overdue rental dashboard |
| Regulatory | Required by law, regulation, or industry standard | Data retention per Saudi commercial code |
| Technical | Arises from technical constraints or architecture decisions | Database must support Arabic character sets (UTF-8) |
| Business | Derived from business strategy, goals, or market requirements | Online booking to increase rental conversion rate by 15% |

Every requirement must have at least one source classification.
