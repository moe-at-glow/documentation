# RACI Matrix -- Requirements Engineering

Responsibility assignment for requirements engineering activities.

---

## Legend

| Code | Meaning |
|------|---------|
| R | **Responsible** -- Does the work |
| A | **Accountable** -- Owns the outcome, has final authority |
| C | **Consulted** -- Provides input before the work is done |
| I | **Informed** -- Notified after the work is done |

Each activity has exactly one **A** (Accountable). Multiple roles may be **R**, **C**, or **I**.

---

## Matrix

| Activity | Project Sponsor | Product Owner | Business Analyst | Tech Lead | Developer | QA Lead | Domain Expert |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Stakeholder Analysis | I | A | R | C | -- | -- | C |
| Business Requirements Elicitation | C | A | R | C | -- | -- | R |
| Requirements Workshop Facilitation | I | C | R/A | C | -- | -- | R |
| BRD Authoring | -- | A | R | C | -- | I | C |
| Requirements Decomposition (STK/SYS/SWR) | -- | I | R | R/A | C | C | C |
| SRS Authoring | -- | I | R | A | C | C | -- |
| Requirements Review | I | R | R | R | C | R | C |
| Requirements Validation | I | A | R | R | -- | R | C |
| Traceability Matrix Maintenance | -- | I | R/A | C | I | C | -- |
| Change Request Processing | I | A | R | C | I | C | -- |
| Baseline Approval | A | R | I | R | I | R | -- |

---

## Role Definitions (in Requirements Engineering Context)

| Role | Focus Area |
|------|-----------|
| Project Sponsor | Approves business case and baseline. Resolves escalations. Final authority on scope. |
| Product Owner | Defines business priorities. Accepts requirements. Decides on change requests. |
| Business Analyst | Facilitates elicitation. Authors BRD and SRS. Maintains RTM. Coordinates reviews. |
| Tech Lead | Reviews technical feasibility. Decomposes system/software requirements. Approves SRS. |
| Developer | Provides implementation perspective during decomposition and review. |
| QA Lead | Reviews testability. Defines test approach. Participates in validation. |
| Domain Expert | Provides subject matter knowledge during elicitation, workshops, and reviews. |
