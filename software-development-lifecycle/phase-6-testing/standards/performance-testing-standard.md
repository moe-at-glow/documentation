# Performance Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P6-003 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead |
| **Verification Method** | Test Review / CI Pipeline |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Load test on critical endpoints only; response time targets apply; stress/spike/endurance tests not required
> **IF** medium project (3-5 devs) **THEN** Load test + stress test required pre-release; all response time and throughput targets apply
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Response Time Targets

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Health check: p95 < 50ms, p99 < 100ms | All projects | [ ] Performance test report | Optimization required |
| 2 | Single resource GET: p95 < 200ms, p99 < 500ms | All projects | [ ] Performance test report | Optimization required |
| 3 | List endpoint with pagination: p95 < 500ms, p99 < 1s | All projects | [ ] Performance test report | Optimization required |
| 4 | Create/update operations (POST, PUT, PATCH): p95 < 300ms, p99 < 1s | All projects | [ ] Performance test report | Optimization required |
| 5 | Search with filters: p95 < 500ms, p99 < 1.5s | All projects | [ ] Performance test report | Optimization required |
| 6 | Report generation: p95 < 2s, p99 < 5s | Medium+ projects | [ ] Performance test report | Optimization required |
| 7 | File upload: p95 < 3s, p99 < 10s | Medium+ projects | [ ] Performance test report | Optimization required |

### Throughput Targets

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 8 | Support 100 concurrent users (normal load) | All projects | [ ] Load test report | Release blocked |
| 9 | Support 500 concurrent users (peak load) | Medium+ projects | [ ] Stress test report | Release blocked |
| 10 | 200 requests/second (normal load) | All projects | [ ] Load test report | Release blocked |
| 11 | 1,000 requests/second (peak load) | Medium+ projects | [ ] Stress test report | Release blocked |
| 12 | Error rate < 0.1% under normal load | All projects | [ ] Load test report | Release blocked |
| 13 | Error rate < 1% under peak load | Medium+ projects | [ ] Stress test report | Release blocked |

### Resource Utilization Limits

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 14 | CPU: < 50% normal, < 80% peak | All projects | [ ] Resource monitoring report | Optimization required |
| 15 | Memory: < 60% normal, < 85% peak | All projects | [ ] Resource monitoring report | Optimization required |
| 16 | Database connections: < 50% of pool normal, < 80% of pool peak | All projects | [ ] Resource monitoring report | Optimization required |
| 17 | Disk I/O: < 40% normal, < 70% peak | Medium+ projects | [ ] Resource monitoring report | Optimization required |

### Load Test Parameters

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 18 | Duration: 30 minutes | All projects | [ ] Test execution log | Re-run required |
| 19 | Ramp-up: 5 minutes to reach target load | All projects | [ ] Test execution log | Re-run required |
| 20 | Concurrent users: 100 | All projects | [ ] Test execution log | Re-run required |
| 21 | Scenario mix: 70% read, 30% write operations | All projects | [ ] Test scenario config | Re-run required |
| 22 | Pass criteria: response times within p95 targets, error rate < 0.1% | All projects | [ ] Load test report | Release blocked |

### Stress Test Parameters

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 23 | Duration: 60 minutes | Medium+ projects | [ ] Test execution log | Re-run required |
| 24 | Ramp-up: gradual increase from 100 to 1,000+ users | Medium+ projects | [ ] Test execution log | Re-run required |
| 25 | Identify maximum sustainable load and degradation behavior | Medium+ projects | [ ] Stress test report | Report must document findings |

### Spike Test Parameters

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 26 | Baseline: 100 concurrent users for 10 minutes | Large projects | [ ] Test execution log | Re-run required |
| 27 | Spike: jump to 500 users for 5 minutes | Large projects | [ ] Test execution log | Re-run required |
| 28 | Recovery: drop to 100 users for 10 minutes | Large projects | [ ] Test execution log | Re-run required |
| 29 | Pass criteria: system recovers to normal response times within 2 minutes after spike | Large projects | [ ] Spike test report | Optimization required |

### Endurance (Soak) Test Parameters

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 30 | Duration: 4-8 hours | Large projects | [ ] Test execution log | Re-run required |
| 31 | Concurrent users: 50 (moderate steady load) | Large projects | [ ] Test execution log | Re-run required |
| 32 | Pass criteria: no memory growth trend, stable response times, no connection pool exhaustion | Large projects | [ ] Soak test report | Optimization required |

### Standard Load Mix

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 33 | Load mix: List rentals 20%, View rental 15%, List equipment 15%, View equipment 10%, Create rental 10%, Update rental 5%, List invoices 10%, View invoice 5%, Process payment 5%, Health check 5% | All projects | [ ] Test scenario config | Config correction required |

### Critical Path Scenarios

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 34 | Late fee calculation batch tested under load | Medium+ projects | [ ] Test execution log | Release blocked |
| 35 | Invoice generation batch tested under load | Medium+ projects | [ ] Test execution log | Release blocked |
| 36 | Equipment status update via IoT (high-frequency MQTT) tested under load | Large projects | [ ] Test execution log | Release blocked |
| 37 | Search with multiple filters tested under load | Medium+ projects | [ ] Test execution log | Release blocked |

### Test Data

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 38 | Production-like volume: 10K+ customers, 50K+ equipment, 200K+ rentals | All projects | [ ] Test data audit | Re-run with correct data |
| 39 | Realistic distribution of statuses, dates, amounts | All projects | [ ] Test data audit | Re-run with correct data |
| 40 | Pre-warmed cache: run warm-up requests before measuring | All projects | [ ] Test execution log | Re-run required |
| 41 | Database restored to known state before each test | All projects | [ ] Test setup verification | Re-run required |

### Reporting

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 42 | Report includes: summary (pass/fail, key metrics, comparison to targets) | All projects | [ ] Report review | Report revision required |
| 43 | Report includes: response times (p50, p95, p99 per endpoint) | All projects | [ ] Report review | Report revision required |
| 44 | Report includes: throughput (RPS over time) | All projects | [ ] Report review | Report revision required |
| 45 | Report includes: error rate (percentage and types) | All projects | [ ] Report review | Report revision required |
| 46 | Report includes: resource utilization (CPU, memory, DB connections over time) | All projects | [ ] Report review | Report revision required |
| 47 | Report includes: bottlenecks identified with recommendations | All projects | [ ] Report review | Report revision required |
| 48 | Report includes: trends (comparison to previous test runs) | Medium+ projects | [ ] Report review | Report revision required |

### Execution Triggers

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 49 | Pre-release: load test + stress test | All projects | [ ] Test execution log | Release blocked |
| 50 | Major database changes: load test | All projects | [ ] Test execution log | Merge blocked |
| 51 | New endpoint added: load test for the new endpoint | All projects | [ ] Test execution log | PR blocked |
| 52 | Performance-related defect: targeted load test to verify fix | All projects | [ ] Test execution log | Defect remains open |
| 53 | Quarterly: full suite (load + stress + spike + endurance) | Large projects | [ ] Quarterly test schedule | Escalation to QA Lead |

---

## COMPLIANCE CHECKLIST

- [ ] Response time targets defined and measured (p95 and p99)
- [ ] Throughput targets met at normal load (100 users, 200 RPS, < 0.1% errors)
- [ ] Throughput targets met at peak load (500 users, 1000 RPS, < 1% errors)
- [ ] Resource utilization within limits (CPU, memory, DB connections, disk I/O)
- [ ] Load test executed (30 min, 100 users, 70/30 read/write mix)
- [ ] Stress test executed (60 min, ramp to 1000+ users)
- [ ] Spike test executed (baseline -> 500 users -> recovery within 2 min)
- [ ] Endurance test executed (4-8 hours, 50 users, no memory growth)
- [ ] Standard load mix percentages followed
- [ ] Critical path scenarios tested under load (late fees, invoices, IoT, search)
- [ ] Test data is production-like volume with realistic distribution
- [ ] Cache pre-warmed before measurement
- [ ] Performance test report includes all required sections
- [ ] Trends compared to previous test runs
- [ ] All execution triggers followed (pre-release, DB changes, new endpoints, quarterly)

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Report and Track Defects | Runbook | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Perform Regression Testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Test Plan Template | Template | [../templates/test-plan-template.md](../templates/test-plan-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
