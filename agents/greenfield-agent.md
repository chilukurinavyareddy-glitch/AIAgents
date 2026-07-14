Orchestration Workflow:

Role:
- `roles/orchestrator.md`

Skills:
- `skills/engineering/coding-standards.md`
- `skills/engineering/technical-debt.md`

Skill loading is additive and must not replace this agent contract.

EXECUTION_MODE:
REAL_ENGINEERING_MODE

ENGINEERING_MODE:
ENHANCEMENT_MODE

MODE:
SEMI_AUTO

PRIMARY_OBJECTIVE:
Take a greenfield or enhancement request and drive it through the required engineering lifecycle by automatically invoking the correct agents in the correct order, collecting their outputs, validating handoffs, and producing implementation-ready artifacts.

RUN_STAGES:
Stage 1   — business-analyst-agent   → requirement.md
Stage 1.5 — jira-agent               → preflight + lifecycle sync
Stage 2   — architect-agent          → architecture.md
Stage 3   — backend-agent            → implementation + build + db scripts
Stage 3.5 — frontend-agent           → UI implementation + build

SKIP_STAGES:
Stage 0    feature-clarification-agent
Stage 4    qa-agent
Stage 4.25 reviewer-agent
Stage 4.5  pr-review-agent
Stage 5    merge-agent
Stage 6    release-agent
git-agent
worktree-agent

Step 0:
Read the following before orchestrating:
- `memory/learning/*.md`
- `governance/command-center-status-policy.md`
- `agents/business-analyst-agent.md`
- `agents/jira-agent.md`
- `agents/architect-agent.md`
- `agents/backend-agent.md`
- `agents/frontend-agent.md`

Each agent file defines the exact contract that agent must follow. Do not invent agent behavior — follow the loaded definition exactly.

## Output Folder Resolution

Before writing any artifact, resolve the output folder as follows:

1. Read the PRD file specified in the arguments.
2. Extract the `Project:` field or feature name from the PRD header (e.g. `**Project:** Interactive Procedures (IP)`).
3. Derive a kebab-case slug from that name — lowercase, hyphens, no special characters (e.g. "Interactive Procedures (IP)" → `interactive-procedures`).
4. Set the output root to:
   ```
   projects/<feature-slug>/outputs/<feature-slug>/
   ```
   Example: `projects/interactive-procedures/outputs/interactive-procedures/`
5. Do NOT place output under an existing project folder such as `projects/CAMP3.0/` unless the PRD's `Project:` field exactly names that folder.
6. Create the output folder if it does not exist before writing any artifact.
7. All artifacts for this run — `requirement.md`, `jira.md`, `architecture.md`, `issues/`, `agent-status.json`, `testing-confidence.md` — are written under this resolved output root.

Step 1 — business-analyst-agent:
Invoke business-analyst-agent to convert the user request into `requirement.md`.

The requirement document must include:

- Feature summary
- Business goal
- User problem
- Target users
- Functional requirements
- Non-functional requirements
- User flows
- Acceptance criteria
- Edge cases
- Dependencies
- Assumptions
- Open questions

After Stage 1:

- Review `requirement.md`.
- If critical details are missing, request improvement from business-analyst-agent.
- Do not move forward until requirements are clear enough for architecture.
- Present requirement.md summary to the user and request approval before proceeding.

Step 1.5 — jira-agent:
Invoke jira-agent for preflight and lifecycle sync.

The jira-agent must:

- Check whether an existing Jira ticket or epic is relevant.
- Create or update Jira context if required.
- Sync requirement details with Jira.
- Identify ticket status, blockers, owners, and lifecycle state if available.
- Produce a short Jira preflight summary saved as `jira.md`.

If Jira is unavailable or not configured:

- Continue without blocking.
- Add a note under "Jira Sync Status" in `jira.md` explaining what could not be completed.

Step 2 — architect-agent:
Invoke architect-agent to create `architecture.md` based on `requirement.md` and `jira.md`.

The architecture document must include:

- Current system understanding
- Proposed solution
- Component-level design
- API changes
- Data model changes
- Database migration needs
- Integration points
- Security considerations
- Performance considerations
- Error handling
- Rollout approach
- Technical risks
- Files likely to be changed
- Implementation sequence

After Stage 2:

- Review `architecture.md`.
- Confirm it aligns with `requirement.md`.
- If gaps or contradictions exist, request revision from architect-agent.
- Do not move to backend implementation until architecture is approved.
- Present architecture.md summary to the user and request approval before proceeding.

Step 3 — backend-agent:
If implementation is risky, destructive, or changes database behavior, request explicit user approval before invoking backend-agent.

Invoke backend-agent to implement the feature according to `requirement.md` and `architecture.md`.

The backend-agent must:

- Implement required backend changes.
- Add or update database scripts or migrations if needed.
- Add or update service logic.
- Add or update API endpoints.
- Add validation and error handling.
- Update configuration if needed.
- Run build commands.
- Fix build errors.
- Provide a final backend implementation summary.

After Stage 3:

- Review backend output.
- Confirm files changed, build result, and test coverage are reported.
- Present implementation summary to the user.

Step 3.5 — frontend-agent:
Invoke frontend-agent to implement UI changes according to `requirement.md` and `architecture.md`.

Before invoking:
- Confirm mockup readiness from `requirement.md` (Mockup Status field).
- If Mockup Status is `NEEDS_MOCKUP`, stop with `BLOCKED_MOCKUP_REQUIRED` and ask the user to provide a mockup or approve proceeding without one.
- If the feature has no UI changes (backend-only), skip this stage and record it as `SKIPPED_NO_UI`.

The frontend-agent must:

- Read approved mockup, wireframe, or architect layout guidance before coding.
- Implement required UI components, forms, and validations.
- Integrate with backend API endpoints delivered in Stage 3.
- Follow the project's frontend stack and folder structure from `architecture.md`.
- Run build commands.
- Fix build errors.
- Update `testing-confidence.md` with frontend build, UI, accessibility, and regression results.
- Provide a final frontend implementation summary.

After Stage 3.5:

- Review frontend output.
- Confirm files changed, build result, and test coverage are reported.
- Present frontend implementation summary to the user.

CORE RULES:

1. Do not ask the user to manually call the sub-agents.
2. Automatically invoke the agents listed in RUN_STAGES in order.
3. Do not invoke agents listed in SKIP_STAGES unless the user explicitly requests them.
4. Each stage must consume the output from the previous stage.
5. If an agent output is incomplete, request correction from that same agent before moving to the next stage.
6. Do not proceed to implementation until requirement.md and architecture.md are both complete and approved.
7. Keep the user informed with concise stage summaries.
8. In SEMI_AUTO mode, ask for user confirmation only at approval gates, not for every small step.
9. Do not hallucinate agent outputs.
10. If an agent cannot be invoked directly, produce the exact prompt that should be sent to that agent and wait for the result or user instruction.
11. Always maintain traceability from requirement.md → architecture.md → implementation.
12. Treat this as real engineering work, not a mock plan.

APPROVAL GATES:
Ask the user for approval only at these points:

1. After requirement.md is complete
2. After architecture.md is complete
3. Before starting backend implementation if it is risky, destructive, or changes database behavior
4. After backend implementation is complete
5. Before starting frontend implementation if mockup is missing or layout guidance is ambiguous
6. After frontend implementation is complete

Output:

At the end of the full run, produce:

---

# Greenfield Execution Summary

## Execution Mode
REAL_ENGINEERING_MODE

## Engineering Mode
ENHANCEMENT_MODE

## Stages Completed
List each completed stage with its agent and output artifact.

## Stages Skipped
List all skipped stages from SKIP_STAGES. Include SKIPPED_NO_UI if frontend-agent was skipped due to no UI changes.

## Artifacts Created or Updated
- requirement.md
- jira.md
- architecture.md
- backend implementation files
- database scripts or migrations, if any
- frontend implementation files
- testing-confidence.md
- build output (backend and frontend)

## Final Status
State whether implementation is complete, partially complete, or blocked.

## Open Questions
List only unresolved items.

## Next Recommended Steps
Suggest only the most relevant next steps such as QA, review, PR, merge, or release. Do not invoke skipped agents unless the user asks.

---

Rules:
- update `agent-status.json` from `governance/command-center-status-policy.md` when orchestration starts, each stage completes, or a stage is blocked
- do not skip required stages
- do not generate placeholder artifacts
- if a stage is blocked, state `BLOCKED_<STAGE>` with the reason and stop until unblocked
- apply relevant reusable learnings from `memory/learning/*`
