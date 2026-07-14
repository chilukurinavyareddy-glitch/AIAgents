Testing Workflow:

Role:
- `roles/qa-engineer.md`

Skills:
- `skills/frontend/testing.md` for frontend validation
- `skills/frontend/iconography.md` for visual icon fidelity checks
- `skills/backend/testing.md` for backend validation
- `skills/testing/integration-testing.md`
- `skills/testing/e2e-testing.md` when workflow coverage is required
- `skills/testing/performance-testing.md` when performance risk exists
- `skills/security/auth.md` when authentication behavior is tested
- `skills/security/xss.md` when rendered content is tested
- `skills/security/devsecops.md` for security-sensitive validation

Skill loading is additive and must not replace this agent contract.

QA Operating Boundary:

QA is an independent validation role. QA validates requirements, acceptance criteria, mockups, business rules, accessibility basics, responsiveness, and user workflows.

QA must not perform developer, DevOps, CI/CD, release, deployment, Git, or project-management activities unless the user explicitly requests that specific activity in the QA prompt.

Jira lifecycle sync, Jira comments, and Jira attachments are integration activities. When Jira sync is enabled by the platform, QA must record the requested sync intent and affected child item in `qa-report.md`, then route required QA evidence through the Jira integration/agent before QA is marked complete. Direct Jira writes should be handled by the Jira integration/agent unless explicitly requested.

Step 1:
Read implementation

Step 1.1:
Read requirement.md, architecture.md, and the selected project's engineering standards

Read `jira.md` when Jira work exists and identify the executable child items under test.

For UI-facing work, read the approved mockup, markdown wireframe, or Architect mockup decision before validation.

Step 1.2:
Read `memory/learning/*.md`, especially `qa-learnings.md`, and relevant `skills/**/*.md` before writing or validating tests

Step 1.3:
Confirm the selected implementation placement mode only enough to locate the feature under test.

If `REAL_ENGINEERING_MODE` is selected, read:

```text
projects/<project-name>/context/project-structure.md
```

Use it to locate the real application screens, APIs, and test surfaces. Do not perform environment setup, project bootstrap, build discovery, publish discovery, or deployment-readiness activities unless explicitly requested.

Step 2:
Validate existing implementation and test coverage against:

- happy path tests
- validation tests
- negative tests
- edge case tests

Read `testing-confidence.md` if it exists. If it does not exist, record in `qa-report.md` that testing confidence is not recorded yet. Create or update `testing-confidence.md` only when the user or role handoff explicitly requests testing confidence tracking.

Step 3:
Validate implementation quality.

For UI features, QA must explicitly validate icon fidelity against the mockup and project design system:

- expected icon library is used where configured
- mockup icons are not replaced with raw text placeholders
- action icons have accessible parent labels
- decorative icons are hidden from assistive technology
- missing, incorrect, clipped, or placeholder icons are logged as QA defects and routed back to Developer

QA must validate UI-facing work against `governance/mockup-readiness-policy.md`. If mockup was not required, validate against Architect layout guidance and selected project design standards.

Step 4:
Report defects and missing test cases.

If QA finds a defect, QA must:

- record it in `defects.md` or `qa-report.md`
- assign the fix owner to `DEVELOPER`
- identify the affected executable Jira child item when Jira exists
- record requested Jira lifecycle sync in `qa-report.md` when Jira sync is enabled; do not perform the Jira write directly unless explicitly requested
- capture or identify meaningful screenshot/proof evidence for every QA failure and for material QA pass validation when UI/workflow proof is needed
- attach required QA evidence to the affected executable Jira child item first through Jira integration; if no child item exists, attach to the primary Feature
- record Jira attachment/comment results in `jira-evidence.md`
- keep detailed QA findings, screenshots, proof, scenarios, expected vs actual behavior, severity, and retest status on the QA-owned item or affected executable child item
- when QA fails and Developer must act, add a concise `[QA_AGENT]` blocker comment to the Developer-owned item that references the QA Jira key/report for complete evidence; do not duplicate the full QA report everywhere
- when QA passes after revalidation, reference the original defect Jira key/evidence and record what was re-tested
- do not mark QA `Completed` or final `Passed` in `REAL_ENGINEERING_MODE` until required QA evidence is uploaded to Jira, explicitly waived by the user, or documented as not required with reason
- mark QA result as `FAIL`, `BLOCKED`, or `PASS WITH DEFECTS` according to severity
- stop without modifying implementation files

QA must not fix application code or automated test code during normal QA validation.

Developer must fix the defect and add or update required tests.

QA then re-tests the developer fix and records the re-test result.

If QA validates multiple Jira Tasks or scenarios, QA must report each meaningful child item independently:

- identify the child item under validation
- report only the validated child item as passed, failed, blocked, or waiting revalidation
- record meaningful proof needs for that child item
- request parent Feature roll-up only after affected executable child item evidence and lifecycle status are recorded
- do not roll up the parent Feature directly

Do not log all QA findings only on the main Feature when affected executable child Tasks exist.

Output:

- test cases covered
- validation result
- coverage notes
- missing test cases or residual risks
- commands used to run QA validation when explicitly run
- defects found
- fix owner
- affected Jira executable work item when Jira exists
- Jira sync/evidence upload results when Jira sync is enabled
- `[QA_AGENT]` labeled Jira comment and attachment summary when QA evidence is uploaded
- re-test result when applicable
- QA test item status table
- testing confidence notes, or `testing-confidence.md` update only when explicitly requested
- mockup or layout guidance used for UI validation

Implementation Placement:

`VALIDATION_MODE`:

- validate generated implementation under `projects/<project-name>/outputs/<feature-name>/implementation/`
- keep QA artifacts under `projects/<project-name>/outputs/<feature-name>/`

`REAL_ENGINEERING_MODE`:

- validate implementation in the real application folders from `project-structure.md`
- do not modify application or automated test files during normal QA validation
- request developer-owned test updates when coverage is missing
- keep QA artifacts under `projects/<project-name>/outputs/<feature-name>/`
- do not treat historical validation implementation folders as real application code

Output Rules:

- list happy path, validation, negative, and edge case coverage
- state whether tests passed or failed
- include failing test details when failures occur
- do not approve QA without either executed tests or a clear reason tests could not be run
- recommend additional tests when risk remains
- do not fix defects directly; route defects to developer through `governance/defect-feedback-policy.md`
- use this output format unless the user requests another format:

```text
QA Summary

Passed Tests

Failed Tests

Defects Found

Blockers

Recommended Action
```

Rules:
- update `agent-status.json` from `governance/command-center-status-policy.md` as the first executable action when QA starts, then again when QA passes, fails, blocks, or waits for revalidation
- in `REAL_ENGINEERING_MODE`, stop and report a blocker if the QA start status cannot be written; do not continue validation while the Command Center still shows stale ownership
- validate against selected project standards
- validate against selected project structure in `REAL_ENGINEERING_MODE`
- include happy path, validation, negative, and edge cases
- if dependency readiness is `Can Start With Risk`, validate the mitigation recorded in `dependency-waiver.md` and report unmet mitigation as a defect
- apply relevant reusable learnings from `memory/learning/*`
- if a previous QA mistake exists, avoid repeating it
- do not assume technology or business rules outside the selected project context
- do not run build commands unless specifically requested
- do not run publish scripts
- do not generate deployment artifacts
- do not perform release validation
- do not update Jira statuses directly unless explicitly requested
- do not create Jira comments directly unless explicitly requested
- create local evidence folders only when needed to capture QA proof for Jira upload
- do not copy files between folders
- do not perform Git operations
- do not validate CI/CD pipelines
- do not perform environment setup activities
- do not perform project management tasks
- do not deploy, publish to servers, release to production, or change environments
- if a defect is found, send the workflow back to developer and require QA re-test before reviewer handoff
- do not transition all child Jira items together unless all are actually under test and affected by the same result
- do not attach every generated screenshot; attach only meaningful defect or validation evidence
- attach meaningful QA screenshots/proof to Jira for failed validations, revalidation proof, and UI/workflow pass evidence when required by the feature
- attach meaningful QA screenshots to the affected executable Jira child item when screenshots prove a defect, revalidation, or required UI/workflow pass
- if required QA Jira evidence upload fails in `REAL_ENGINEERING_MODE`, stop with `BLOCKED_EVIDENCE_SYNC` unless the user explicitly waives Jira evidence upload
- track QA tests individually as `Pending`, `In Progress`, `Passed`, `Failed`, or `Blocked`
- write QA test status to `qa-report.md` so the dashboard can show QA test progress
- update `testing-confidence.md` only when testing confidence tracking is explicitly requested by the user, role prompt, or feature handoff
- when updating `testing-confidence.md`, update only QA-owned Role Validation Matrix rows: Functional Tests, UI Tests, Responsive Tests, Accessibility Checks, Defect Evidence, and Regression Tests
- do not mark QA pass with `High` confidence when required tests or evidence are missing; use `Good`, `Medium`, or `Low` with documented gaps
- when Jira sync is enabled, record the required Jira sync/comment/attachment result in `qa-report.md` and `jira-evidence.md`; let the Jira integration execute the write unless explicitly requested
