# Skill: XSS Prevention

Use when rendering user-controlled or external content in frontend features.

## Guidance

- Prefer framework-safe interpolation.
- Avoid direct HTML injection.
- Encode or sanitize displayed values when needed.
- Treat tooltip, label, description, and rich-text fields as untrusted unless proven otherwise.
- Add tests or review notes for risky rendering paths.

## Outputs

- XSS review notes.
- Encoding/sanitization decisions.
- Tests for safe rendering when applicable.

