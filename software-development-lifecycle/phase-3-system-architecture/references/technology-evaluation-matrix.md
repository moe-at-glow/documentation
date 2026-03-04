# Technology Evaluation Matrix

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P3-003 |
| **Use When** | Evaluating and comparing technology options (database, framework, library, service) for an architecture decision |
| **Last Updated** | 2026-03-04 |

---

## Evaluation Criteria

| Criterion | Weight | Description | How to Assess |
|-----------|--------|-------------|---------------|
| Requirements Fit | Critical | Does it satisfy the specific requirements driving the decision? | Map each ASR to the technology's capabilities |
| Team Expertise | High | Does the team have experience with this technology? | Survey team members; rate as Strong/Moderate/None |
| Maturity | High | Is the technology production-proven and stable? | Check version history, major users, years in production |
| Community & Support | High | Is there an active community, documentation, and support? | Check GitHub stars, Stack Overflow questions, release frequency |
| Performance | Medium | Does it meet performance requirements under expected load? | Run benchmarks or reference published benchmarks |
| Operational Complexity | Medium | How difficult is it to deploy, monitor, and maintain? | Assess deployment process, monitoring tools, upgrade path |
| Security | Medium | Does it have a good security track record? Are there known CVEs? | Check CVE database, security advisories, update frequency |
| Licensing | Medium | Is the license compatible with commercial use? | Review license type (MIT, Apache, GPL, proprietary) |
| Scalability | Medium | Can it scale to meet future growth requirements? | Review horizontal/vertical scaling options |
| Cost | Low-Medium | What are the direct and indirect costs? | License fees, infrastructure requirements, training costs |
| Learning Curve | Low | How long to become productive? | Estimate ramp-up time for an average developer |

---

## Scoring Method

| Score | Meaning |
|-------|---------|
| 5 | Excellent fit. Fully meets or exceeds the criterion. |
| 4 | Good fit. Meets the criterion with minor limitations. |
| 3 | Adequate. Meets the criterion but with notable limitations. |
| 2 | Poor fit. Significant gaps or concerns. |
| 1 | Unacceptable. Does not meet the criterion. |

Weight values: Critical = 5, High = 4, Medium = 3, Low = 1.

Weighted score = Score x Weight. Sum all weighted scores for final ranking.

---

## Example: Message Broker for IoT Telemetry

**Context:** GlowPowerRental needs to ingest telemetry data from 500+ IoT sensors mounted on rental equipment. Sensors send data every 60 seconds over cellular connections with intermittent connectivity. (Ref: SWR-301, SWR-COM-001)

| Criterion | Weight | Mosquitto (MQTT) | RabbitMQ (AMQP) | Apache Kafka |
|-----------|--------|-----------------|-----------------|--------------|
| Requirements Fit | 5 | 5 - Purpose-built for IoT, QoS levels, persistent sessions | 3 - General messaging, not IoT-specific, can work with MQTT plugin | 4 - Excellent throughput but overkill for 500 devices |
| Team Expertise | 4 | 3 - Some MQTT experience from prior IoT work | 2 - No team experience | 1 - No team experience |
| Maturity | 4 | 5 - 10+ years, Eclipse Foundation project | 5 - 15+ years, widely deployed | 5 - 10+ years, Apache Foundation |
| Community & Support | 4 | 4 - Active community, good docs | 5 - Large community, commercial support | 5 - Very large community, Confluent support |
| Performance | 3 | 4 - Handles 100K+ connections, low overhead | 4 - High throughput with AMQP | 5 - Highest throughput of all options |
| Operational Complexity | 3 | 5 - Single binary, minimal configuration | 3 - Erlang runtime, more complex ops | 1 - Requires ZooKeeper/KRaft, JVM tuning, complex ops |
| Security | 3 | 4 - TLS, ACLs, username/password, plugin auth | 5 - TLS, SASL, fine-grained permissions | 4 - TLS, SASL, ACLs |
| Licensing | 3 | 5 - Eclipse Public License (free) | 5 - Mozilla Public License (free) | 5 - Apache License (free) |
| Scalability | 3 | 3 - Clustering available but limited compared to Kafka | 4 - Good clustering, federation | 5 - Designed for horizontal scaling |
| Cost | 1 | 5 - No cost | 5 - No cost | 3 - Higher infra requirements |
| Learning Curve | 1 | 4 - Simple concepts, quick to learn | 3 - More concepts (exchanges, bindings) | 2 - Steep learning curve |

**Weighted Scores:**

| Technology | Weighted Score |
|-----------|---------------|
| Mosquitto | 143 |
| RabbitMQ | 121 |
| Apache Kafka | 109 |

**Decision:** Mosquitto. Best fit for IoT use case, lowest operational complexity, team has some experience. Documented in ADR-001.

---

## Blank Evaluation Template

| Criterion | Weight | Option A | Option B | Option C |
|-----------|--------|----------|----------|----------|
| Requirements Fit | 5 | | | |
| Team Expertise | 4 | | | |
| Maturity | 4 | | | |
| Community & Support | 4 | | | |
| Performance | 3 | | | |
| Operational Complexity | 3 | | | |
| Security | 3 | | | |
| Licensing | 3 | | | |
| Scalability | 3 | | | |
| Cost | 1 | | | |
| Learning Curve | 1 | | | |
| **Weighted Total** | | | | |

---

## DECISION TREE

### Do I need a formal technology evaluation?

```
IF selecting a new technology not already in the approved stack
  THEN YES — complete the full evaluation matrix with at least 2 options

IF replacing an existing technology
  THEN YES — complete the full evaluation matrix comparing current vs. proposed

IF selecting between versions of an already-approved technology
  THEN NO — document version rationale in the ADR only

IF using a minor library (< 500 lines of integration code, easily replaceable)
  THEN NO — document choice in the Technology Stack Document only
```

### How to interpret weighted scores

```
IF winning option leads by >= 20 points
  THEN selection is clear — document in ADR and proceed

IF top two options are within 20 points
  THEN conduct a proof-of-concept (PoC) for both
  THEN re-score after PoC with updated Team Expertise and Performance scores

IF all options score below 100 (out of max 170)
  THEN no option is a strong fit
  THEN revisit requirements — consider expanding search or adjusting constraints
```

### Which criteria matter most for my scenario?

```
IF team is small (< 5 developers)
  THEN prioritize: Team Expertise, Operational Complexity, Learning Curve

IF system is customer-facing with SLA requirements
  THEN prioritize: Performance, Security, Maturity

IF project is a prototype or internal tool
  THEN prioritize: Requirements Fit, Learning Curve, Cost

IF system handles sensitive data (PII, financial)
  THEN Security weight MUST be elevated to Critical (weight = 5)
```

### Licensing red flags

```
IF license = GPL or AGPL
  THEN consult legal — copyleft may affect proprietary code

IF license = SSPL (Server Side Public License)
  THEN consult legal — restrictions on offering as a service

IF license = MIT, Apache 2.0, or BSD
  THEN safe for commercial use — proceed

IF license = Proprietary
  THEN evaluate cost and vendor lock-in risk before proceeding
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Architecture Description | Runbook | ../runbooks/create-architecture-description.md |
| Conduct Architecture Review | Runbook | ../runbooks/conduct-architecture-review.md |
| Write Architecture Decision Record | Runbook | ../runbooks/write-architecture-decision-record.md |
