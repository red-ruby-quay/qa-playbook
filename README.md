# QA Playbook

A practical, reusable QA knowledge base for planning, executing, and communicating quality work. It is intentionally tool-agnostic: the same checklists work for a web app, an API, or a data pipeline.

## Who it is for

- QA engineers who need a starting point for a test strategy or release plan.
- Developers who own quality for their services.
- Teams that want a shared definition of done and release readiness.

## How to use it

1. Copy the relevant document into your project.
2. Fill in the placeholders.
3. Delete what does not apply.
4. Link the filled document from the project README or ticket.

## Contents

| Area | Document |
| --- | --- |
| Strategy | [Test strategy](docs/test-strategy.md) |
| Planning | [Test plan](docs/test-plan.md) |
| Defects | [Bug report](docs/bug-report.md) |
| Performance | [Performance checklist](docs/performance-checklist.md) |
| Security | [Security checklist](docs/security-checklist.md) |
| API | [API checklist](docs/api-checklist.md) |
| Release | [Release readiness](docs/release-readiness.md) |
| Measurement | [Quality metrics](docs/metrics.md) |
| Automation | [Automation decision guide](docs/automation-decision.md) |
| Interviews | [Case study template](docs/case-study-template.md) |

## Principles

- **Risk first.** Spend effort where failure hurts the most.
- **Evidence over opinion.** Every finding has a reproduction and a result.
- **Reproducibility.** A test that only works on one laptop is not a test.
- **Clear communication.** A bug report is a product document, not a diary.
- **Useful metrics.** Track decisions, not vanity numbers.

## License

MIT. See [LICENSE](LICENSE).

## Author

Rihan Yosral — QA Automation Engineer · <https://github.com/red-ruby-quay>
