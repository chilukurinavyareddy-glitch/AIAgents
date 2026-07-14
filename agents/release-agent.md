Release Workflow:

Role:
- `roles/release-engineer.md`

Skills:
- `skills/engineering/coding-standards.md`
- `skills/devops/release.md` when available
- `skills/security/devsecops.md`

Skill loading is additive and must not replace this agent contract.

Step 0:
Read `memory/learning/*.md` and `governance/command-center-status-policy.md` before starting.

Step 1:
Read `requirement.md`, `architecture.md`, `qa-report.md`, `review.md`, and PR review findings to confirm all pre-release gates have passed.

Step 2:
Read `jira.md` when Jira work exists.

Identify the executable Jira child items or parent Feature that owns the release work.

If lifecycle sync is enabled, request Jira sync for each item:

- release started -> `In Release` or equivalent
- release complete -> `Done` or equivalent

Step 3:
Confirm the following pre-release checklist before proceeding:

- All QA sign-offs are present in `qa-report.md`
- All PR reviews are approved
- Build is green
- No open blocking defects
- Database migrations are applied or scheduled
- Configuration changes are deployed or scheduled
- Security checks are complete

If any checklist item is missing or failed, stop with `BLOCKED_PRE_RELEASE` and list the blocking items.

Step 4:
Prepare the release notes using the following structure:

```
# Release Notes: <Feature or Version>

## Summary
Brief description of what is being released.

## Changes Included
- List of features, fixes, and migrations.

## Deployment Steps
Ordered list of steps to deploy this release.

## Rollback Plan
Steps to roll back the release if a critical issue is found post-deployment.

## Post-Deployment Verification
Steps to verify the release is working correctly after deployment.

## Known Limitations
Any known issues accepted as risks in this release.
```

Step 5:
Coordinate deployment actions in the correct order:

1. Apply database migrations if any.
2. Deploy backend services.
3. Deploy frontend if applicable.
4. Run smoke tests.
5. Confirm post-deployment verification steps are complete.

Step 6:
Update Jira lifecycle state to release-complete for all owned executable items.

Output:

- release-notes.md
- deployment confirmation
- post-deployment verification result
- Jira sync status

Output Rules:

- state whether the release is complete, partially complete, or blocked
- list all steps executed and their results
- list any rollback actions taken if applicable
- record the owning Jira executable work items
- do not mark release complete without post-deployment verification
- if Jira sync fails and is required, report `BLOCKED_EVIDENCE_SYNC` unless explicitly waived

Rules:
- update `agent-status.json` from `governance/command-center-status-policy.md` when release starts, completes, or is blocked
- do not deploy without confirmed QA and review sign-off
- do not hardcode environment-specific values — read from project configuration
- apply relevant reusable learnings from `memory/learning/*`
- if a previous release mistake exists, avoid repeating it
- explain major deployment decisions
