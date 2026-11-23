# API testing checklist

Use this when a service exposes an HTTP API that other systems depend on.

## Contract

- [ ] Every endpoint is documented with method, path, parameters, and sample responses.
- [ ] Request and response schemas are versioned.
- [ ] Breaking changes go through a new version, not a silent change.
- [ ] Error responses follow one consistent shape.

## Functional checks

- [ ] Happy path returns the expected body and status.
- [ ] Required fields are validated with clear messages.
- [ ] Unknown fields are rejected or ignored according to policy.
- [ ] Pagination returns stable, non-overlapping pages.
- [ ] Filtering and sorting behave as documented.
- [ ] Idempotency keys make retries safe for create operations.

## Status codes

| Code | Use |
| --- | --- |
| 200 | Success with a body |
| 201 | Resource created, with `Location` |
| 204 | Success without a body |
| 400 | Malformed request |
| 401 | Missing or invalid credentials |
| 403 | Authenticated but not allowed |
| 404 | Resource not found |
| 409 | Conflict with current state |
| 422 | Valid syntax, failed business rules |
| 429 | Rate limited, with `Retry-After` |
| 5xx | Server fault, never used for validation |

## Authentication and authorization

- [ ] Unauthenticated requests are rejected with 401.
- [ ] Expired or tampered tokens are rejected.
- [ ] Users cannot read or modify another user's resources.
- [ ] Scopes and roles are enforced per endpoint.

## Negative and edge cases

- [ ] Missing body, empty body, and malformed JSON.
- [ ] Wrong content type.
- [ ] Boundary values: zero, negative, maximum length, unicode.
- [ ] Very large payloads are rejected with a clear error.
- [ ] Concurrent updates produce a deterministic result or a conflict.

## Reliability

- [ ] Timeouts are documented and enforced.
- [ ] Retries are safe and bounded.
- [ ] Rate limits return 429 with a retry hint.
- [ ] Errors include a correlation ID.

## Performance

- [ ] p95 latency meets the SLO for each endpoint.
- [ ] Large result sets are paginated.
- [ ] Expensive queries are indexed and measured.

## Example with curl

```bash
curl -sS -X POST https://api.example.com/v1/login \
  -H 'content-type: application/json' \
  -d '{"username":"demo","password":"demo"}' | jq

curl -sS https://api.example.com/v1/items?limit=5 \
  -H "authorization: Bearer $TOKEN" | jq '.data | length'
```

## Example with k6

```javascript
import http from 'k6/http';
import { check } from 'k6';

export default function () {
  const res = http.get(`${__ENV.API_BASE_URL}/items?limit=5`);
  check(res, {
    'status is 200': (r) => r.status === 200,
    'returns at most 5 items': (r) => r.json('data').length <= 5,
  });
}
```

## Automation notes

- Assert on the contract, not on incidental fields.
- Store the schema next to the tests and validate responses against it.
- Keep a small smoke suite that runs on every deploy and a fuller suite that runs nightly.
