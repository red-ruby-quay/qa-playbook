# Quality metrics

Measure what changes a decision. A metric that nobody acts on is noise.

## Release health

| Metric | Definition | Why it matters |
| --- | --- | --- |
| Defect escape rate | Defects found in production ÷ total defects | Shows how well testing caught problems early |
| Mean time to detect | Time from deploy to alert | Measures observation |
| Change failure rate | Deploys that cause a rollback or hotfix ÷ total deploys | Measures release quality |
| Rollback rate | Rollbacks ÷ deploys | Signals readiness gaps |

## Testing effectiveness

| Metric | Definition | Caution |
| --- | --- | --- |
| Automation pass rate | Passed automated checks ÷ total | 100% may mean tests are too weak |
| Flaky test rate | Tests with nondeterministic results ÷ total | Should trend toward zero |
| Coverage of critical journeys | Journeys with automated checks ÷ all critical journeys | Prefer this over line coverage |
| Defects found per test cycle | New defects ÷ cycle | Rising may mean scope grew |

## Speed

| Metric | Definition | Why it matters |
| --- | --- | --- |
| Test suite duration | Wall-clock time for CI suite | Long suites get skipped |
| Time to feedback | Commit to first failing check | Short feedback keeps quality in the loop |
| Lead time for changes | Commit to production | Connects QA to delivery |

## Product quality signals

| Metric | Definition |
| --- | --- |
| p95 latency | 95th percentile response time |
| Error rate | Failed requests ÷ total requests |
| Crash-free sessions | Sessions without a crash ÷ total |
| Support tickets per release | Volume tied to a release |

## Anti-patterns

- **Test count as a goal.** More tests can mean more maintenance, not more confidence.
- **Line coverage as a target.** A high number with no assertions proves little.
- **Bug count as a performance measure.** It punishes teams for finding problems.
- **Vanity dashboards.** If a chart has never triggered a decision, remove it.

## A small, useful set

Start with these four and add only when you need to answer a specific question:

1. Defect escape rate.
2. Change failure rate.
3. p95 latency against the SLO.
4. Automation pass rate for critical journeys.

## Reporting cadence

- Per release: pass/fail, open risks, and the release decision.
- Monthly: trends for the four core metrics with a short interpretation.
- Always include the data source and the time window.
