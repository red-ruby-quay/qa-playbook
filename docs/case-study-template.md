# Case study template

Use this to write up a QA project for a portfolio, a review, or a presentation. Keep it factual and specific.

## Title

One line that names the outcome, for example: *Cut release regression from two days to four hours with a k6 and API smoke suite*.

## Context

- Product and team size.
- What was failing or slow before.
- Constraints: time, tools, access, budget.

## Problem

State the problem in measurable terms.

- Regression took two days per release.
- No performance baseline existed.
- Security scans were run manually and inconsistently.

## Approach

Describe the decisions, not just the tools.

1. Mapped critical journeys and risks.
2. Built a smoke suite for every deploy and a full suite for nightly runs.
3. Added k6 load tests with SLO thresholds.
4. Integrated a DAST baseline into the release checklist.

Explain *why* each choice was made and what was rejected.

## Implementation

- Repositories and key files.
- CI jobs and triggers.
- Environments and data.
- Dashboards and reports.

Include small, redacted code samples that show the important idea.

## Results

Use numbers with a baseline and a time window.

| Metric | Before | After |
| --- | --- | --- |
| Regression time | 2 days | 4 hours |
| Defect escape rate | 8% | 3% |
| p95 latency at peak | 2.1 s | 0.6 s |

## What I would do differently

A short, honest list. This section signals judgment.

## Evidence

- Links to repositories, reports, or dashboards.
- Screenshots with sensitive data removed.

## Scope note

State clearly what was not done, for example: no production load testing, no mobile clients.
