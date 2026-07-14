# Skill: Secure Secrets Handling

Use when code, configuration, tests, CI, or docs touch tokens, keys, passwords, connection strings, or credentials.

## Guidance

- Never commit secrets.
- Keep local secrets in ignored local configuration.
- Prefer environment variables or approved secret stores.
- Do not print secrets in logs, reports, dashboard state, PR comments, or screenshots.
- Use placeholder names in docs and examples.
- Rotate credentials if accidental exposure is suspected.

## Outputs

- Secrets handling notes.
- Configuration safety checks.
- Review findings when secrets are exposed.

