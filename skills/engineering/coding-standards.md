# Skill: Coding Standards

Use when implementing or reviewing code across any stack.

## Guidance

- Follow the selected project's conventions.
- Keep names clear and consistent.
- Prefer small, focused units.
- Avoid unrelated refactors.
- Keep comments useful and sparse.
- Do not introduce new architectural patterns without a reason.
- Preserve semantic boundaries in normalized reporting data. Do not copy one evidence category into another for convenience; for example, `Gaps` must not be surfaced as `Missing Validation`.
- When changing parsing, normalization, or dashboard summary logic, add or run a focused regression check for the source artifact, normalized API shape, and UI-facing data contract.

## Outputs

- Coding convention notes.
- Review findings.
- Refactor risk notes.
