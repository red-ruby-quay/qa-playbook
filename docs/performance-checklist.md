# Performance testing checklist

Use this before and during a load test so the result means something.

## Before the test

- [ ] Define the question: capacity, regression, or a specific bottleneck.
- [ ] Record the target SLOs (p95 latency, error rate, throughput).
- [ ] Use an environment that mirrors production in size and configuration.
- [ ] Seed a realistic data set; do not test against an empty database.
- [ ] Confirm no other load is running on the environment.
- [ ] Record the build version and infrastructure settings.
- [ ] Verify the load generator is not the bottleneck (CPU, network, file descriptors).

## Metrics to collect

| Metric | Why it matters | Typical target |
| --- | --- | --- |
| Requests per second | Throughput | Matches expected peak |
| p50 / p95 / p99 latency | Typical and tail experience | p95 under SLO |
| Error rate | Correctness under load | < 1% |
| Virtual users | Load level | Matches the test plan |
| CPU and memory | Headroom | Below 80% at peak |
| DB connections and slow queries | Hidden bottleneck | No connection saturation |
| Business errors | Correct responses, not just HTTP 200 | < 1% |

## Test shapes

| Test | Shape | Question |
| --- | --- | --- |
| Smoke | 1–5 VUs, 1–2 minutes | Does the flow work at all? |
| Load | Ramp to expected peak | Do SLOs hold at peak? |
| Stress | Ramp beyond peak | Where does it break? |
| Soak | Steady peak for hours | Do leaks or degradation appear? |
| Spike | Sudden jump | Does it recover? |

## During the test

- Watch server CPU, memory, and database metrics live.
- Note the time when thresholds are crossed.
- Capture logs for the failure window.
- Stop the test if it could damage shared data.

## After the test

- [ ] Compare results with the baseline, not just against thresholds.
- [ ] Separate client-side from server-side costs.
- [ ] Identify the first metric that degraded; that is the bottleneck.
- [ ] Attach the summary, graphs, and raw results to the report.
- [ ] Record what changed since the last run.
- [ ] File defects for regressions with reproduction steps.

## Interpreting results

- A latency curve that stays flat then jumps indicates a resource limit, not a linear slowdown.
- A rising error rate with flat latency usually means saturation at a downstream dependency.
- High p99 with normal p50 points to GC pauses, locks, or a slow minority path.
- Throughput that plateaus while latency climbs means the system is saturated.

## Common mistakes

- Testing an empty database and declaring success.
- Measuring only averages.
- Ignoring business errors because the HTTP status is 200.
- Running the load generator on the same host as the application.
- Comparing runs from different environments or data sets.
