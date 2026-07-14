# Skills

## Purpose

`skills/` contains reusable capability packs used by agents.

Skills keep platform knowledge modular and easy to review.

Examples:

- Angular guidance
- .NET guidance
- API design
- testing
- security
- PR review
- merge readiness
- scalability and resiliency
- accessibility and UX review
- observability and error handling
- rollback and dependency management

## Relationship To Agents

Agents remain the execution contract.

Skills are additive guidance loaded by selected agents.

```text
Role -> Skill -> Agent -> Workflow -> Worker
```

## How To Extend

Add a skill when the guidance is reusable across features or projects.

Keep each skill focused:

- one capability
- clear guidance
- expected outputs
- no project-specific assumptions

## Skill Areas

| Folder | Purpose |
| --- | --- |
| `frontend/` | Angular, forms, accessibility, UX, frontend tests. |
| `backend/` | .NET, API design/versioning, error handling, observability, backend tests. |
| `database/` | SQL Server and migrations. |
| `security/` | Auth, JWT, XSS, DevSecOps, secrets. |
| `testing/` | Integration, E2E, and performance testing. |
| `architecture/` | Scalability and resiliency. |
| `review/` | Code, PR, architecture, security, and performance review. |
| `release/` | Branching, PRs, merge readiness, rollback, toggles, dependency management. |
| `requirement-engineering/` | Story decomposition, Jira creation, risk scoring. |
| `engineering/` | Coding standards and technical debt. |
