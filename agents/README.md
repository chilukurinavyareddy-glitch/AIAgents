# Agents

## Purpose

`agents/` contains the active execution contracts for the AI Engineering Platform.

Agents describe what each AI role does, what it must read, what it can output, and which guardrails it must follow.

## Responsibilities

- Keep orchestration behavior explicit.
- Define input and output contracts.
- Reference relevant roles and skills.
- Preserve backward compatibility for workflows and workers.
- Support discovery-first execution for enhancement and legacy rewrite modes.

## Dependencies

Agents commonly load:

- `memory/platform-context.md`
- `memory/learning/*.md`
- `guardrails/*.md`
- `governance/*.md`
- `roles/*.md`
- relevant `skills/**/*.md`
- `projects/<project-name>/context/`
- `projects/<project-name>/context/project-config.yml` when engineering modes are selected
- `config/engineering-modes/*.yml`

## How To Extend

Add a new agent only when a responsibility is distinct enough to require its own contract.

Before adding a new agent:

- check whether an existing agent plus a new skill is enough
- define exact inputs and outputs
- update `agents/master-orchestrator.md`
- update relevant workflows
- add validation coverage

Discovery plugins live under:

```text
agents/discovery/
```

Use discovery plugins when `ENHANCEMENT_MODE` or `LEGACY_REWRITE_MODE` requires framework, architecture, routing, API, database, or dependency detection before implementation.

## Project-Specific Agent Extensions

Project-specific agents may extend a generic role agent when a project has strict domain, runtime, database, or delivery gates that should be checked consistently.

Current project-specific extensions:

- `pdf-processing-architecture-agent.md` extends `architect-agent.md` for `projects/PDF-Processing`.

Selection rule:

- For `PROJECT: PDF-Processing` architecture work, select `pdf-processing-architecture-agent.md` as the Architect stage agent.

These extensions are additive. They do not replace the generic role contract; the project-specific agent must still follow the generic role agent it extends.
