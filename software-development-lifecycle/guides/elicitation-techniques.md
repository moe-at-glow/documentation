# Elicitation Techniques

Guide to requirements elicitation techniques and when to use each one.

---

## Technique Summary

| Technique | Best For | Effort | Output Quality |
|-----------|----------|--------|---------------|
| Structured Interviews | Deep understanding of individual stakeholder needs | Medium | High |
| Workshops (JAD) | Cross-functional alignment and conflict resolution | High | High |
| Observation | Understanding actual workflows vs. stated workflows | Medium | High |
| Document Analysis | Existing system constraints and business rules | Low | Medium |
| Prototyping | UI/UX requirements and user feedback | High | High |
| Surveys | Large stakeholder groups with similar questions | Low | Medium |
| Use Case Analysis | System interactions and behavioral requirements | Medium | High |
| User Story Mapping | Agile backlog creation and feature prioritization | Medium | Medium |

---

## 1. Structured Interviews

One-on-one or small group conversations with a prepared question framework.

**When to use:**
- Key stakeholders with high power/interest.
- Sensitive topics that stakeholders will not discuss in groups.
- Initial discovery phase.

**Advantages:**
- Deep insight into individual perspectives.
- Builds rapport and trust with stakeholders.
- Can explore unexpected topics as they arise.

**Disadvantages:**
- Time-intensive (45-60 minutes per stakeholder).
- May surface conflicting views that need separate resolution.
- Interviewer bias can influence responses.

**Output artifacts:** Interview notes, recorded requirements attributed to stakeholder.

**Tips:**
- Prepare questions in advance. Use the interview framework in the [Extract Business Requirements](../runbooks/extract-business-requirements.md) runbook.
- Record sessions (with permission).
- Send summary back to interviewee for confirmation within 48 hours.

---

## 2. Workshops (JAD Sessions)

Facilitated group sessions to elicit, discuss, and prioritize requirements.

**When to use:**
- Multiple stakeholder groups need to align on shared requirements.
- Conflicting needs exist between departments.
- Prioritization decisions require group consensus.

**Advantages:**
- Resolves conflicts in real time.
- Builds shared understanding across groups.
- Efficient for covering broad scope.

**Disadvantages:**
- Requires skilled facilitator.
- Dominant personalities can suppress input from quieter stakeholders.
- Scheduling many stakeholders is difficult.

**Output artifacts:** Workshop minutes, prioritized requirement list, action items.

**Facilitation tips:**
- Set ground rules at the start (one speaker, no solutioning, all perspectives valid).
- Use parking lot for off-topic items.
- Time-box each discussion topic.
- Use silent writing before group discussion to capture all perspectives.

---

## 3. Observation

Watching users perform their actual work to understand real processes and pain points.

**When to use:**
- Replacing or improving an existing process.
- Stakeholders have difficulty articulating their needs.
- You suspect the stated process differs from the actual process.

**Advantages:**
- Reveals unstated requirements and workarounds.
- Identifies pain points users have normalized.
- Provides context that interviews miss.

**Disadvantages:**
- Users may change behavior when observed (Hawthorne effect).
- Time-consuming for complex processes.
- Observer may misinterpret actions without context.

**Output artifacts:** Process flow documentation, pain point list, as-is state description.

**Tips:**
- Observe multiple users performing the same task.
- Ask clarifying questions during or immediately after observation.
- Document workarounds -- they indicate unmet needs.

---

## 4. Document Analysis

Reviewing existing documentation to extract requirements and constraints.

**When to use:**
- Existing systems are being replaced or enhanced.
- Regulatory or contractual requirements exist.
- Historical data on current system behavior is available.

**Sources to review:**

| Document Type | What to Extract |
|--------------|----------------|
| Existing system documentation | Current features, data models, integrations |
| Contracts and SLAs | Performance requirements, compliance obligations |
| Regulations | Mandatory requirements (data retention, reporting) |
| Help desk tickets | Common user complaints and feature requests |
| Training materials | Expected workflows and user procedures |

**Advantages:**
- Low effort, can be done independently.
- Surfaces requirements stakeholders may forget to mention.
- Provides objective evidence.

**Disadvantages:**
- Documentation may be outdated or incomplete.
- Does not capture unstated needs or new requirements.
- Requires validation against current reality.

**Output artifacts:** Extracted requirements list, document reference log.

---

## 5. Prototyping

Creating mockups or wireframes to elicit feedback on user interface and workflow requirements.

**When to use:**
- User-facing applications where UX is critical.
- Stakeholders need to "see it" before they can define what they want.
- Validating workflow assumptions.

**Advantages:**
- Concrete visual reduces ambiguity.
- Users provide more specific feedback on something tangible.
- Identifies usability requirements early.

**Disadvantages:**
- Risk of stakeholders focusing on UI details instead of business needs.
- Prototype may set expectations about final design.
- Requires design skills and tools.

**Output artifacts:** Wireframes, annotated mockups, user feedback notes.

**Tips:**
- Use low-fidelity wireframes (paper or simple digital) to avoid design fixation.
- Explicitly state "this is not the final design."
- Focus feedback sessions on workflows, not visual aesthetics.

---

## 6. Surveys and Questionnaires

Structured questions distributed to a large group of stakeholders.

**When to use:**
- Large user base with similar roles (e.g., 50+ rental desk operators).
- Validating priorities across a broad group.
- Gathering quantitative data on feature importance.

**Advantages:**
- Scales to large groups efficiently.
- Produces quantifiable results.
- Reduces interviewer bias.

**Disadvantages:**
- Cannot explore unexpected topics.
- Low response rates are common.
- Poorly designed questions produce poor data.

**Output artifacts:** Survey results, statistical analysis, feature priority ranking.

**Tips:**
- Keep surveys under 15 minutes.
- Use a mix of closed (rating scale) and open (free text) questions.
- Test the survey with 2-3 people before distributing.

---

## 7. Use Case Analysis

Identifying actors and their interactions with the system to define behavioral requirements.

**When to use:**
- Defining system behavior and interactions.
- Multiple actors interact with the same features.
- Need to capture main flow, alternate flows, and exception handling.

**Advantages:**
- Captures complete interaction scenarios including error cases.
- Clear structure that developers and testers understand.
- Naturally identifies system boundaries.

**Disadvantages:**
- Can become overly detailed too early.
- Not well suited for non-functional requirements.
- Requires understanding of system boundaries.

**Output artifacts:** Use case documents (use [Use Case Template](../templates/use-case-template.md)), actor list, use case diagram.

---

## 8. User Story Mapping

Organizing requirements as user stories and mapping them to a release plan.

**When to use:**
- Agile execution model.
- Need to plan incremental delivery.
- Prioritizing features across releases.

**Format:** As a [role], I want [capability], so that [business value].

**Advantages:**
- Connects requirements directly to user value.
- Natural input for sprint planning.
- Easy to prioritize and estimate.

**Disadvantages:**
- May lack the specificity needed for complex systems.
- Not sufficient as standalone requirements documentation (must be supplemented with acceptance criteria).
- Can miss system-level and non-functional requirements.

**Output artifacts:** User story map, epic/feature/story hierarchy, story acceptance criteria.

---

## Technique Selection Decision Matrix

| Situation | Recommended Techniques |
|-----------|----------------------|
| New project, unknown domain | Interviews + Observation + Document Analysis |
| Replacing existing system | Document Analysis + Observation + Interviews |
| User-facing application | Interviews + Prototyping + Use Case Analysis |
| Large user base | Surveys + Workshops + User Story Mapping |
| Regulatory/compliance requirements | Document Analysis + Interviews (with compliance officer) |
| Agile delivery | User Story Mapping + Workshops + Prototyping |
| Cross-departmental system | Workshops + Interviews + Use Case Analysis |

In most GlowPowerRental projects, use a combination of at least three techniques to ensure comprehensive coverage.
