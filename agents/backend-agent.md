Implementation Workflow:

Role:
- `roles/developer.md`

Skills:
- `skills/backend/dotnet.md`
- `skills/backend/api-design.md`
- `skills/backend/api-versioning.md` when API compatibility is affected
- `skills/backend/error-handling.md`
- `skills/backend/observability.md` when logging, health, telemetry, or diagnostics are involved
- `skills/backend/testing.md`
- `skills/database/sql-server.md` when persistence is involved
- `skills/database/migrations.md` when schema change is involved
- `skills/engineering/coding-standards.md`
- `skills/engineering/technical-debt.md`
- `skills/security/auth.md` when authentication or authorization is involved
- `skills/security/jwt.md` when JWT is involved
- `skills/security/devsecops.md`
- `skills/security/secrets.md` when configuration or credentials are touched

Skill loading is additive and must not replace this agent contract.

Step 0:
Read `memory/learning/*.md`, especially `backend-learnings.md`, and relevant `skills/**/*.md` before coding.

Step 1:
Read requirement.md

Step 2:
Read architecture.md

Step 2.5:
Read `issues/*.md` when present.

Identify the issue file(s) assigned to this implementation run. Scope backend work to the vertical slice described in the assigned issue file — do not implement the full feature in one pass unless no issue files exist.

If no issue files are present, fall back to full feature scope from requirement.md.

Step 3:
Read backend-plan.md if available

Step 3.05:
Read `defects.md`, `qa-report.md`, `review.md`, or PR review findings when work is returning from QA, review, or PR review.

If this is a defect loop, fix only the assigned backend issue, add or update relevant tests, rerun targeted validation, and return to the originating validation role for re-test or re-review.

Step 3.06:
Read `jira.md` when Jira work exists.

Identify the executable Jira child item or parent Feature that owns the backend work.

When executable child Jira work exists, select the specific child item for the scenario being implemented. Do not use the parent Feature as the only lifecycle item.

If lifecycle sync is enabled, request Jira sync for that selected executable item:

- development start -> `In Progress`
- implementation complete -> review or release-ready state
- defect fix ready -> review or re-test state

If the owning child item cannot be identified in `REAL_ENGINEERING_MODE`, stop handoff with `BLOCKED_CHILD_MAPPING`.

Step 3.1:
Confirm the selected implementation placement mode.

If `REAL_ENGINEERING_MODE` is selected:

1. Run `scripts/ensure-feature-worktree.ps1` to create or reuse the feature branch and worktree before touching any files.
2. Run `scripts/assert-real-engineering-worktree.ps1` to confirm the worktree is valid. Stop with `BLOCKED_WORKTREE` if either script fails.
3. Read and validate:

```text
projects/<project-name>/context/project-structure.md
```

Stop safely before implementation if backend, service, repository, database, or test roots needed for the change are missing, still placeholders, or do not exist.

Step 4:
Create implementation incrementally

Order:

1. folder structure
2. entities
3. DTOs
4. validators
5. services
6. API controllers
7. unit tests

Step 5:
Run build validation

Step 6:
Fix errors automatically. Re-run build after fixes. Do not proceed to output until build passes or failure is explicitly documented with reason.

Step 5.1:
Update `testing-confidence.md` using `templates/testing-confidence-template.md` and `governance/testing-confidence-policy.md`.

Record backend build, unit, integration, API, security, and regression results that apply to the feature. If a required test is not run, record `NOT_RUN` with a reason instead of omitting it.

Output:

- backend source files
- domain or application models when needed
- DTOs or request/response contracts when needed
- validators
- services or handlers
- API endpoints or controllers when needed
- unit tests
- build validation result
- testing-confidence.md
- implementation summary

Implementation Placement:

`VALIDATION_MODE`:

- keep current behavior
- write generated backend implementation under `projects/<project-name>/outputs/<feature-name>/implementation/`
- keep backend summaries in the feature output folder

`REAL_ENGINEERING_MODE`:

- write backend code only under configured backend, service, repository, or database roots from `project-structure.md`
- write backend tests only under the configured test root from `project-structure.md`
- keep artifacts such as plans, review notes, score, and summary under `projects/<project-name>/outputs/<feature-name>/`
- do not write implementation code to the feature output folder

Output Rules:

- list created or modified files
- state the build command used
- state whether build validation passed or failed
- update `testing-confidence.md` with test commands, pass/fail/not-run results, blockers, gaps, and confidence score
- in the Role Validation Matrix, update only Developer-owned rows that apply to backend work: Build / Type Check, Code Implementation, Unit Tests, Integration Tests, API Tests, Security Checks through review notes when applicable, and Regression Tests
- state any known limitations or follow-up work
- do not mark backend work complete without tests or an explicit reason tests are not applicable
- record the owning Jira executable work item when Jira exists
- do not report only the parent Feature when a child executable Jira item owns the work
- when implementing multiple scenarios, update each scenario's executable child Jira item as work starts and completes
- when returning from QA, review, or PR feedback, reference the originating Jira key and evidence source, fix only the assigned items, and add a concise developer response to the affected executable item
- developer Jira comments must include files changed, commands run, tests added or updated, validation result, known gaps, evidence uploaded, and next owner
- when Jira comments are needed, prepare `[DEVELOPER_AGENT]` comment text using the standard format from `governance/jira-evidence-policy.md` and request Jira integration sync
- identify developer evidence only when it materially proves a fix, validation result, or discrepancy
- in `REAL_ENGINEERING_MODE`, required developer proof must be queued for Jira evidence sync before marking developer handoff complete; if required sync fails in the Jira integration, report `BLOCKED_EVIDENCE_SYNC` unless explicitly waived
- after confirmed Jira upload by the Jira integration, request local screenshot/proof cleanup according to `governance/jira-evidence-policy.md`

Rules:
- update `agent-status.json` from `governance/command-center-status-policy.md` when developer backend work starts, completes, blocks, or is routed back from QA/review
- if dependency readiness is `Blocked by Dependency` or `Foundation Required`, stop with `BLOCKED_DEPENDENCY`
- if dependency readiness is `Can Start With Risk`, read `dependency-waiver.md`, follow the mitigation exactly, and record waiver-aware validation evidence
- do not generate placeholder code
- code must compile
- follow the selected project's architecture and engineering standards
- follow the selected project's real folder structure from project-structure.md in `REAL_ENGINEERING_MODE`
- apply relevant reusable learnings from `memory/learning/*`
- if a previous backend mistake exists, avoid repeating it
- do not hardcode a backend framework, language, or architecture style
- explain major decisions
