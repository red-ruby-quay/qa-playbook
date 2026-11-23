# Test strategy

Use this template to align scope, risk, and evidence before any execution starts. A strategy answers *why* and *what*; a plan answers *when* and *who*.

## 1. Context

| Field | Value |
| --- | --- |
| Product or service | |
| Release or milestone | |
| Business owner | |
| Test lead | |
| Date | |

## 2. Goals

State 2–4 outcomes, not activities.

- Reduce the chance that a failed payment reaches production.
- Give the release owner evidence that critical journeys work on the target environment.
- Cut regression time by moving stable checks into CI.

## 3. Scope

### In scope

- Critical user journeys: sign-in, checkout, account recovery.
- Public API endpoints under `/api/v1`.
- Non-functional checks: p95 latency under expected load, no high-severity DAST findings.

### Out of scope

- Load beyond 2× expected peak.
- Third-party payment provider internals.
- Native mobile clients.

## 4. Quality attributes

| Attribute | Target | How we verify |
| --- | --- | --- |
| Functional correctness | Critical journeys pass | Exploratory + automated E2E |
| Performance | p95 < 800 ms at expected load | k6 load test |
| Security | No high findings | ZAP baseline scan + manual review |
| Accessibility | No critical axe violations | axe scan on key pages |
| Reliability | No data loss on retry | Fault injection on the payment callback |

## 5. Risk assessment

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Checkout fails under load | Medium | High | Load test 10 → 20 VUs | QA |
| Auth bypass | Low | Critical | DAST + access-control tests | Security |
| Stale cache after deploy | Medium | Medium | Smoke test on the deployed build | Dev |

Prioritize work by multiplying likelihood and impact, then test high-risk areas first and deepest.

## 6. Test levels and types

| Level | What runs | Where | Trigger |
| --- | --- | --- | --- |
| Unit | Pure logic | Developer machine | Commit |
| Integration | Service + database | CI | Pull request |
| API | Contract and behavior | CI | Pull request |
| E2E | Critical journeys | Staging | Nightly |
| Performance | Load and stress | Staging | Before release |
| Security | DAST baseline | Staging | Before release |

## 7. Environments and data

- Environments: local, CI, staging. Production is read-only for testing unless explicitly approved.
- Test data is synthetic. Never copy production personal data into a test environment.
- Each environment runs the same container images as production.

## 8. Automation strategy

Automate checks that are stable, high-value, and run often. Keep exploratory testing for new and ambiguous areas. See [automation-decision.md](automation-decision.md) for the decision rules.

## 9. Entry and exit criteria

### Entry

- The build is deployed to staging and the version is recorded.
- Test data is seeded.
- Known blockers are documented.

### Exit

- All critical and high-risk checks pass.
- No open critical defects.
- Performance and security results are attached to the release record.

## 10. Metrics

Track a small set that informs decisions. See [metrics.md](metrics.md).

## 11. Roles and communication

| Role | Responsibility |
| --- | --- |
| Test lead | Owns the strategy, plan, and report |
| Developers | Fix defects, own unit and integration checks |
| Product owner | Accepts risk and signs off |

Report status in one place. State what passed, what failed, what is blocked, and what risk remains.

## 12. Assumptions and dependencies

- Staging matches production configuration.
- The team has access to logs and metrics during the test window.

## 13. Sign-off

| Name | Role | Decision | Date |
| --- | --- | --- | --- |
| | Test lead | | |
| | Product owner | | |
