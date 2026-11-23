# Bug report guide

A good defect report lets a developer reproduce, understand, and fix the problem without asking you questions.

## Anatomy

| Field | What it answers |
| --- | --- |
| Title | What is broken, in one line |
| Environment | Where it happens: build, OS, browser, account |
| Preconditions | State required before the steps |
| Steps | Exact, minimal reproduction |
| Expected | What should happen |
| Actual | What does happen |
| Evidence | Screenshot, video, HAR, logs, request ID |
| Severity | How bad the effect is |
| Priority | How soon it should be fixed |
| Impact | Who is affected and how many |

## Title

Write the symptom, not the cause.

- Bad: `Bug in checkout`.
- Bad: `Button not working`.
- Good: `Checkout: applying a 100% coupon leaves the order total at 0 and blocks payment`.

## Steps to reproduce

Number each step and start from a known state.

1. Sign in as `qa.user@example.com`.
2. Add one item priced 25.00 to the cart.
3. Open checkout and apply coupon `FREE100`.
4. Click **Pay now**.

If a step is hard to follow, split it. If a step is not needed, remove it.

## Severity vs priority

| Severity | Meaning | Example |
| --- | --- | --- |
| S1 Critical | Data loss, security breach, or outage | Payment captures twice |
| S2 High | A core flow is broken with no workaround | Checkout cannot complete |
| S3 Medium | A flow works with a workaround | Wrong total after applying a coupon, fixed by refreshing |
| S4 Low | Cosmetic or minor | Misaligned label |

Priority reflects business urgency and may differ from severity. A cosmetic bug on the pricing page can be higher priority than a medium bug in an admin screen.

## Evidence

- Screenshot or short video of the failure.
- Browser console errors and the failing network request (HAR exports are ideal).
- Request ID or correlation ID from the response headers.
- Server logs for the same time window, if available.
- The exact build version, not "latest".

Redact tokens, cookies, and personal data before attaching anything.

## Writing style

- Lead with the impact.
- Use plain language, one idea per sentence.
- Say what you observed; do not guess the cause unless you have evidence.
- Link related tickets and duplicate reports.

## Template

```markdown
### Title

### Environment
- Build:
- OS/browser:
- Account:

### Preconditions

### Steps
1.

### Expected

### Actual

### Evidence

### Severity / Priority

### Impact
```

## Anti-patterns

- "Doesn't work" with no steps.
- A screenshot of an error with no context.
- Bundling several unrelated problems into one ticket.
- Claiming a root cause without evidence.
- Reporting a problem you have not retried once to rule out a fluke.
