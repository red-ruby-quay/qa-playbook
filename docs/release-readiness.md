# Release readiness checklist

Use this before shipping. Every unchecked item needs an owner and a decision, not silence.

## Build and version

- [ ] The release version and commit are recorded.
- [ ] The artifact was built from the tagged commit by CI.
- [ ] The same artifact is deployed to staging and production.

## Quality evidence

- [ ] Critical journeys pass on staging.
- [ ] Automated regression suite is green.
- [ ] No open critical or high defects.
- [ ] Known issues are documented with impact and owner.

## Performance

- [ ] Load test at expected peak meets the SLOs.
- [ ] No regression versus the previous release baseline.
- [ ] Capacity headroom is documented.

## Security

- [ ] DAST baseline reviewed; no unaccepted high findings.
- [ ] Dependency and image scans are clean or risk-accepted.
- [ ] Secrets are not in the artifact.
- [ ] Access control changes were reviewed.

## Data and migrations

- [ ] Database migrations were tested on a production-sized copy.
- [ ] Migrations are backward compatible with the running version.
- [ ] A rollback path exists and was tested.
- [ ] Backups are current.

## Operations

- [ ] Health checks and alerts cover the new features.
- [ ] Dashboards show the new endpoints.
- [ ] Runbooks are updated.
- [ ] On-call knows what changed.

## Documentation

- [ ] User-facing changes are documented.
- [ ] API changes are documented and versioned.
- [ ] Release notes are written.

## Communication

- [ ] Stakeholders know the release window.
- [ ] Support has the known-issues list.
- [ ] A rollback decision owner is named.

## Decision

| Outcome | Meaning |
| --- | --- |
| Go | All criteria met or residual risk accepted |
| Conditional go | Ship with a documented, time-bound mitigation |
| No-go | A blocking risk remains |

| Name | Role | Decision | Date |
| --- | --- | --- | --- |
| | Test lead | | |
| | Product owner | | |
| | Engineering lead | | |
