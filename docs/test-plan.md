# Test plan

A plan turns a strategy into a schedule with owners and deliverables. Keep it short enough that people read it.

## 1. Summary

| Field | Value |
| --- | --- |
| Release | |
| Owner | |
| Test window | |
| Environment | |
| Build or commit | |

## 2. Objectives

- Verify the release against the agreed scope.
- Produce evidence for the release decision.

## 3. Scope

### Covered

- ...

### Not covered

- ...

## 4. Schedule

| Phase | Start | End | Deliverable |
| --- | --- | --- | --- |
| Preparation | | | Seeded environment, test data |
| Functional | | | Passing critical journeys |
| Non-functional | | | Performance and security results |
| Regression | | | Automated suite green |
| Report | | | Test summary and release recommendation |

## 5. Resources

| Role | Name | Allocation |
| --- | --- | --- |
| Test lead | | |
| QA engineer | | |
| Developer on call | | |

## 6. Test items

| Item | Type | Priority | Owner |
| --- | --- | --- | --- |
| Sign-in and session | Functional | Critical | |
| Checkout | Functional | Critical | |
| `/api/v1/orders` | API | High | |
| Peak load | Performance | High | |
| DAST baseline | Security | High | |

## 7. Test data

- Synthetic accounts and orders are seeded by `scripts/seed.sh`.
- Data is reset before each run so results are comparable.
- No real personal data is used.

## 8. Environment

- Container images are tagged with the release version.
- External dependencies are stubbed where they are not part of the scope.

## 9. Risks and mitigations

| Risk | Mitigation |
| --- | --- |
| Staging instability | Reserve a buffer day and notify the team |
| Missing test data | Seed script runs in CI before tests |
| Flaky E2E | Retry once, then report and investigate |

## 10. Deliverables

- Test summary with pass/fail per item.
- Defect list with severity and owner.
- Performance and security reports attached.
- Release recommendation.

## 11. Communication

- Daily status update in the release channel.
- Blockers raised immediately, not at the end of the window.

## 12. Approval

| Name | Role | Decision | Date |
| --- | --- | --- | --- |
| | Test lead | | |
| | Product owner | | |
