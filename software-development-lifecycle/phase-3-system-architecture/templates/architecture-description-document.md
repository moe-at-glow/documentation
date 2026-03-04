# Architecture Description Document

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-002 |
| **When to Use** | Documenting the full system architecture for a project (one per project) |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect, Product Owner, QA Lead |
| **SLA** | 5 business days for initial draft |
| **Runbook** | [Create Architecture Description](../runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 6 (Process View), 8 (Development View), and 14 (Appendices) optional; Sections 9 quality attributes reduced to Performance and Security only
> **IF** medium project (3-5 devs) **THEN** All sections required; Appendices optional
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Document Title | [Project Name] -- Architecture Description Document |
| Version | 1.0 |
| Status | Draft / Under Review / Approved |
| Author | [Name] |
| Date Created | YYYY-MM-DD |
| Last Updated | YYYY-MM-DD |
| Related SRS | [SRS document reference and version] |

### [ ] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | YYYY-MM-DD | [Name] | Initial draft |

### [ ] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| [Name] | System Architect / Tech Lead | | |
| [Name] | Product Owner | | |
| [Name] | QA Lead | | |

---

## [ ] 1. Executive Summary

[2-3 paragraphs: system purpose, key architectural approach, architecture style, primary technology stack.]

---

## [ ] 2. Architecture Goals and Constraints

### [ ] Goals

| ID | Goal | Priority |
|----|------|----------|
| AG-001 | [Architecture goal] | High/Medium/Low |

### [ ] Constraints

| ID | Constraint | Type | Impact |
|----|-----------|------|--------|
| AC-001 | [Constraint description] | Technical/Budget/Regulatory/Infrastructure | [How it limits architectural choices] |

---

## [ ] 3. Architecture-Significant Requirements

| Requirement ID | Description | Category | Architecture Impact |
|---------------|-------------|----------|-------------------|
| [SWR-XXX] | [Requirement text] | Functional/Performance/Security/Scalability | [How it drives architecture] |

---

## [ ] 4. System Context View

### [ ] System Context Diagram

```
[Insert system context diagram here]

+-----------+          +------------------+          +-----------+
| [Actor 1] |  [proto] |                  | [proto]  | [System]  |
|           +--------->+   [System Name]  +--------->+           |
+-----------+          |                  |          +-----------+
                       +------------------+
```

### [ ] External Entities

| Entity | Type | Protocol | Data Exchanged | Direction |
|--------|------|----------|---------------|-----------|
| [Entity name] | Human/System | HTTP/REST/MQTT/SMTP | [Data description] | Inbound/Outbound/Both |

---

## [ ] 5. Logical/Functional View

### [ ] Component Diagram

```
[Insert component diagram here]
```

### [ ] Component Descriptions

| Component | Responsibility | Owned Data | Exposed Interface | Dependencies |
|-----------|---------------|------------|------------------|-------------|
| [Component name] | [One-sentence responsibility] | [Tables/collections owned] | [API endpoints or events published] | [Components it depends on] |

---

## [ ] 6. Process/Runtime View

### [ ] Key Scenarios

#### [ ] Scenario 1: [Scenario Name]

```
[Insert sequence diagram here]
```

#### [ ] Scenario 2: [Scenario Name]

[Repeat for top 5 scenarios]

### [ ] Scheduled Jobs

| Job Name | Schedule | Components Involved | Data Processed | Duration Target |
|----------|---------|--------------------|--------------------|----------------|
| [Job name] | [Cron expression or frequency] | [Components] | [What it processes] | [Max duration] |

---

## [ ] 7. Deployment View

### [ ] Deployment Diagram

```
[Insert deployment diagram here]
```

### [ ] Infrastructure Components

| Component | Specification | Purpose | Location |
|-----------|--------------|---------|----------|
| [Server/service name] | [CPU/RAM/Storage] | [What it runs] | [Cloud provider/region] |

### [ ] Network Topology

| From | To | Protocol | Port | Encrypted |
|------|-----|----------|------|-----------|
| [Source] | [Destination] | [Protocol] | [Port] | Yes/No |

---

## [ ] 8. Development View

### [ ] Repository Structure

```
[Insert directory structure here]
```

### [ ] Build Pipeline

```
[Insert pipeline diagram here]
```

### [ ] Module Mapping

| Logical Component | Code Module/Package | Repository |
|------------------|--------------------|-----------|
| [Component name] | [src/modules/xxx] | [Repo name] |

---

## [ ] 9. Quality Attribute Approaches

### [ ] Performance

| NFR | Approach | Implementation |
|-----|----------|---------------|
| [SWR-NFR-PXXX] | [Architecture approach] | [Specific technology/technique] |

### [ ] Security

| NFR | Approach | Implementation |
|-----|----------|---------------|
| [SWR-NFR-SXXX] | [Architecture approach] | [Specific technology/technique] |

### [ ] Scalability

| NFR | Approach | Implementation |
|-----|----------|---------------|
| [SWR-NFR-SCXXX] | [Architecture approach] | [Specific technology/technique] |

### [ ] Reliability

| NFR | Approach | Implementation |
|-----|----------|---------------|
| [SWR-NFR-RXXX] | [Architecture approach] | [Specific technology/technique] |

---

## [ ] 10. Technology Stack

| Technology | Version | Purpose | License | ADR Reference |
|-----------|---------|---------|---------|---------------|
| [Technology] | [Version] | [Purpose] | [License] | ADR-XXX |

---

## [ ] 11. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk description] | High/Medium/Low | High/Medium/Low | [Mitigation approach] |

---

## [ ] 12. Architecture Decision Records

| ADR | Title | Status |
|-----|-------|--------|
| ADR-001 | [Decision title] | Accepted |
| ADR-002 | [Decision title] | Accepted |

Full ADRs are located in `architecture/decisions/`.

---

## [ ] 13. Traceability

| SWR ID | Architecture Component | Viewpoint | ADR Reference |
|--------|----------------------|-----------|---------------|
| [SWR-XXX] | [Component name] | [Viewpoint] | [ADR-XXX] |

Full traceability: [Link to RTM]

---

## [ ] 14. Appendices

### [ ] Appendix A: Glossary

| Term | Definition |
|------|-----------|
| [Term] | [Definition] |

### [ ] Appendix B: References

| Document | Version | Date |
|----------|---------|------|
| [SRS title] | [Version] | [Date] |

---

## COMPLETION CHECKLIST

- [ ] Document Control filled in with version, author, and SRS reference
- [ ] Approvers identified
- [ ] Executive Summary written
- [ ] Architecture Goals and Constraints documented
- [ ] Architecture-Significant Requirements listed with traceability
- [ ] System Context View diagram and external entities table completed
- [ ] Component Diagram and descriptions completed
- [ ] Process/Runtime View covers top scenarios
- [ ] Deployment View with infrastructure and network topology
- [ ] Development View with repo structure and module mapping
- [ ] Quality Attribute Approaches for Performance, Security, Scalability, Reliability
- [ ] Technology Stack table completed with ADR references
- [ ] Risks and Mitigations identified
- [ ] ADR index populated
- [ ] Traceability matrix linked
- [ ] Reviewed by System Architect, Product Owner, and QA Lead

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Decision Records | [architecture-decision-record.md](architecture-decision-record.md) | ADRs support decisions in this document |
| Component Diagram | [component-diagram.md](component-diagram.md) | Detailed component view for Section 5 |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Detailed context view for Section 4 |
| Software Requirements Specification | Phase 2 SRS | Source requirements driving the architecture |
| Requirements Traceability Matrix | Phase 2 RTM | Full traceability from requirements to components |
| Runbook | [Create Architecture Description](../runbooks/create-architecture-description.md) | Step-by-step procedure |
