# Claude Code Guidance

This repository stores installable skills that can be shared across Codex and Claude Code via `npx skills`.

## Repository shape

- `README.md`: user-facing install instructions.
- `AGENT.md`: generic agent entrypoint that redirects agents to this file.
- `skills/<skill-name>/SKILL.md`: the actual skill definition.
- `skills/<skill-name>/references/`: optional task-specific workflow references loaded by the skill.

## Editing rules

- Keep each skill in its own directory under `skills/`.
- The skill file must be named `SKILL.md`.
- Start each `SKILL.md` with front matter containing at least:
    - `name`
    - `description`
- Write instructions for concrete triggers and workflows, not generic advice.
- Prefer stable shell commands and explicit paths in examples.
- Preserve compatibility with both Codex and Claude Code consumers.
- Keep README install examples aligned with the actual skill names in `skills/`.
- Keep repository documentation in English unless the existing target file is already localized.

## When adding a new skill

1. Create `skills/<skill-name>/SKILL.md`.
2. Add clear front matter and a concise title.
3. Document when to use the skill, required inputs, and the exact workflow.
4. Update `README.md` if the new skill should be mentioned in install examples or layout docs.

## Current skills

- `motrixsim`: use for MotrixSim Python programming, simulation scripts, MJCF XML model authoring, debugging, and review. It requires version-correct `motrixsim-docs-md` docs before making API or MJCF decisions.