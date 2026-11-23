# Security testing checklist

This checklist covers a baseline security review. It is not a substitute for a full penetration test. Only test systems you own or have written authorization to test.

## Scope and authorization

- [ ] Written permission exists and names the target, window, and allowed techniques.
- [ ] Test accounts have the minimum privileges needed.
- [ ] You know the escalation contact and the stop condition.
- [ ] Production testing is explicitly allowed or excluded.

## Authentication

- [ ] Passwords are hashed with a modern algorithm (bcrypt, scrypt, argon2).
- [ ] Login is rate-limited and lockout is configurable.
- [ ] Session tokens are random, long, and invalidated on logout.
- [ ] Cookies set `HttpOnly`, `Secure`, and `SameSite`.
- [ ] Session IDs rotate after login.
- [ ] Password reset tokens are single-use and expire.

## Authorization

- [ ] Access control is enforced on the server, not the client.
- [ ] Object references are checked against the caller (no IDOR).
- [ ] Admin endpoints reject non-admin users.
- [ ] Role changes and privilege escalation paths are tested.

## Input handling

- [ ] SQL queries use parameterized statements.
- [ ] Output is encoded for the correct context (HTML, attribute, JS, URL).
- [ ] File uploads validate type, size, and destination.
- [ ] SSRF protections block internal metadata endpoints.
- [ ] Command execution paths avoid shell injection.

## Transport and headers

- [ ] TLS is enforced and HSTS is set.
- [ ] Content-Security-Policy is present and restrictive.
- [ ] `X-Content-Type-Options: nosniff` is set.
- [ ] Clickjacking is blocked with `frame-ancestors` or `X-Frame-Options`.
- [ ] CORS allows only trusted origins.

## Data protection

- [ ] Secrets are not in source control, images, or client bundles.
- [ ] Sensitive data is encrypted at rest.
- [ ] Logs do not contain tokens, passwords, or personal data.
- [ ] Backups are encrypted and access-controlled.

## Error handling and configuration

- [ ] Stack traces and debug output are off in production.
- [ ] Default accounts and sample data are removed.
- [ ] Dependencies are scanned for known vulnerabilities.
- [ ] Unused services and ports are closed.

## Automated baseline

Run a DAST baseline against a staging deployment:

```bash
zap-baseline.py -t https://staging.example.com -r report.html -J report.json -I
```

Review every alert. Classify each as a true positive, a false positive with evidence, or a risk accepted with an owner. A passing scan is not proof of security.

## Reporting

For each finding, record:

- Title and severity.
- Affected endpoint or component.
- Reproduction steps and evidence.
- Impact in business terms.
- Remediation advice.

Report responsibly. Do not publish findings or exploit details before the owner has fixed them and agreed on disclosure.
