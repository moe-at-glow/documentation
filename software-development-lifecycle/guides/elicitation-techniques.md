# Elicitation Techniques -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P2-001 |
| **Use When** | Selecting elicitation techniques for a requirements phase |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Stakeholder analysis is complete before starting elicitation
- [ ] At least three techniques are planned for comprehensive coverage
- [ ] Interview questions are prepared in advance (not ad-hoc)
- [ ] Sessions will be recorded or documented (with permission)
- [ ] "What not how" rule is enforced -- no solutioning during elicitation
- [ ] All Power/Interest grid quadrants have representation
- [ ] Survey tested with 2-3 people before broad distribution

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Techniques | Avoid |
|-----------|----------------------|-------|
| New project, unknown domain | Interviews + Observation + Document Analysis | Surveys alone (insufficient depth) |
| Replacing existing system | Document Analysis + Observation + Interviews | Skipping document analysis (miss existing constraints) |
| User-facing application | Interviews + Prototyping + Use Case Analysis | Skipping prototyping (ambiguous UX requirements) |
| Large user base (50+) | Surveys + Workshops + User Story Mapping | Individual interviews for everyone (does not scale) |
| Regulatory/compliance requirements | Document Analysis + Interviews (with compliance officer) | Relying on assumptions about regulations |
| Agile delivery | User Story Mapping + Workshops + Prototyping | Use cases without acceptance criteria supplements |
| Cross-departmental system | Workshops + Interviews + Use Case Analysis | Single-department elicitation |
| Sensitive topics | Structured Interviews (1-on-1) | Group workshops (stakeholders will not speak freely) |
| Stakeholders cannot articulate needs | Observation + Prototyping | Surveys or interviews alone |

---

## QUICK-REFERENCE TABLE

| Technique | Best For | Effort | Output Quality | Key Output |
|-----------|----------|--------|---------------|------------|
| Structured Interviews | Deep individual stakeholder needs | Medium | High | Interview notes, attributed requirements |
| Workshops (JAD) | Cross-functional alignment, conflict resolution | High | High | Prioritized requirement list, action items |
| Observation | Actual workflows vs. stated workflows | Medium | High | Process flows, pain point list, as-is state |
| Document Analysis | Existing system constraints, business rules | Low | Medium | Extracted requirements list, document reference log |
| Prototyping | UI/UX requirements, user feedback | High | High | Wireframes, annotated mockups, feedback notes |
| Surveys | Large groups, quantitative priority data | Low | Medium | Statistical analysis, feature priority ranking |
| Use Case Analysis | System interactions, behavioral requirements | Medium | High | Use case documents, actor list, use case diagram |
| User Story Mapping | Agile backlog, feature prioritization | Medium | Medium | Story map, epic/feature/story hierarchy |

### Document Analysis Sources

| Document Type | What to Extract |
|--------------|----------------|
| Existing system documentation | Current features, data models, integrations |
| Contracts and SLAs | Performance requirements, compliance obligations |
| Regulations | Mandatory requirements (data retention, reporting) |
| Help desk tickets | Common user complaints and feature requests |
| Training materials | Expected workflows and user procedures |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Extract Business Requirements | Runbook | [../runbooks/extract-business-requirements.md](../runbooks/extract-business-requirements.md) |
| Use Case Template | Template | [../templates/use-case-template.md](../templates/use-case-template.md) |
| For background | Training | [training/requirements-engineering-overview.md](training/requirements-engineering-overview.md) |
