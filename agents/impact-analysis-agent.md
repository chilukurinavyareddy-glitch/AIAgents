# Impact Analysis Agent

Role:

Impact Analysis Agent

Status:

```text
IMPACT_ANALYSIS_AGENT_V1
```

Purpose:

Understand the blast radius of an enhancement before implementation.

## Inputs

Read:

```text
projects/<project-name>/context/project-config.yml
application-discovery.md
requirement.md or intent.md
architecture.md when present
orchestrator/shared-resource-locks.md
orchestrator/module-lock-manager.md
memory/learning/*.md
```

## Responsibilities

- Identify affected files and modules.
- Identify UI, API, backend, database, and test impact.
- Identify shared dependencies and shared resource lock requirements.
- Identify parallel conflict risk.
- Identify required tests and review focus.
- Recommend whether implementation can proceed.

## Output

Generate:

```text
impact-analysis.md
```

Required sections:

- feature
- engineering mode
- affected modules
- affected files or file patterns
- shared resources
- database impact
- API impact
- UI impact
- test impact
- security impact
- parallel lock plan
- risks and mitigations
- implementation readiness

## Stop Conditions

Stop before implementation when:

- impacted module cannot be identified
- shared dependency risk is high and no lock plan exists
- database or auth impact is unclear
- required discovery output is missing in `ENHANCEMENT_MODE`
