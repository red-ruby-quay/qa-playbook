# Automation decision guide

Not everything should be automated. Use this guide to decide what stays manual, what moves to CI, and what to skip.

## When to automate

Automate a check when most of these are true:

- It runs often, at least once per release.
- It is stable: the same input produces the same result.
- It is high value: failure is likely or expensive.
- It is mechanical: a human adds little judgment.
- It can run without a human at the keyboard.

## When to keep it manual

Keep a check manual when:

- It is exploratory or the product is changing quickly.
- It needs human judgment, such as visual design or usability.
- It runs once and will not be repeated.
- The cost to automate exceeds the cost of running it by hand.

## Pyramid, adapted

| Layer | Count | Speed | Confidence | Example |
| --- | --- | --- | --- | --- |
| Unit | Many | Milliseconds | Logic correctness | Price calculation |
| Integration | Some | Seconds | Component contracts | Service + database |
| API | Some | Seconds | Endpoint behavior | `/orders` contract |
| E2E | Few | Minutes | Critical journeys | Sign in, pay, confirm |

Favor the lower layers. Push checks down when possible; a calculation tested by a unit test does not need an E2E test.

## Test shapes, not just levels

- **Happy path:** one test per critical journey. Must always pass.
- **Boundary:** values at the edges of valid input.
- **Negative:** invalid input is rejected with a clear error.
- **Concurrency:** two users act at once without corrupting state.
- **Recovery:** the system survives a dependency failure.

## Tool selection

| Need | Reasonable default |
| --- | --- |
| Browser journeys | Playwright |
| HTTP and performance | k6 |
| API contract | Schema validation in the API suite |
| DAST baseline | OWASP ZAP |
| Load dashboards | k6 + InfluxDB + Grafana |

Choose tools your team can run locally. A tool nobody can debug is a liability.

## Making a suite trustworthy

- A test fails for exactly one reason.
- Failures include enough context to start debugging.
- Tests create and clean up their own data.
- Tests do not depend on execution order.
- Flaky tests are fixed or removed, not retried forever.

## Cost of ownership

Track:

- Runtime of the suite.
- Flake rate.
- Time spent maintaining selectors and fixtures.
- Number of checks that have never failed.

Delete or rewrite tests that fail these measures. A smaller, trusted suite beats a large, ignored one.

## Decision record

For each new area, record:

| Question | Answer |
| --- | --- |
| What is the risk? | |
| Automate or manual? | |
| Tool | |
| Where it runs | |
| Owner | |
| Review date | |
