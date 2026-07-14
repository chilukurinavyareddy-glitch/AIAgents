# Skill: JWT Security

Use when implementing or reviewing JWT flows.

## Guidance

- Validate issuer, audience, expiry, and signing key.
- Keep signing secrets out of source control.
- Avoid overly long token lifetimes unless project policy requires them.
- Do not put sensitive personal data in token payloads.
- Add tests for invalid, expired, and missing tokens where practical.

## Outputs

- JWT configuration notes.
- Token validation tests.
- Security review notes.

