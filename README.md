# Motphys Agent Skills

This repository is organized for `npx skills` so the same skills can be installed into both Codex and Claude Code.

## Available skills

### `motrixsim`

Use when writing, debugging, or reviewing MotrixSim Python programs, simulation scripts, or MJCF XML models.

The skill requires agents to use version-correct `motrixsim-docs-md` documentation as the source of truth before choosing Python APIs, MJCF paths, XML attributes, defaults behavior, or validation commands.

## Usage

List available skills from this repository:

```bash
npx skills add git@github.com:Motphys/agent-skills.git --list
```

Install a specific skill:

```bash
npx skills add git@github.com:Motphys/agent-skills.git --skill motrixsim
```

Install into both Codex and Claude Code explicitly:

```bash
npx skills add git@github.com:Motphys/agent-skills.git --skill motrixsim -a codex -a claude-code
```

The `npx skills` client reads the skill metadata first, then loads the full skill instructions when the current task matches the skill description.

## Repository layout

```text
skills/
  motrixsim/
    SKILL.md
    references/
      docs-layout.md
      mjcf-workflow.md
      python-workflow.md
```

Each skill lives in its own directory under `skills/`. A skill directory may also contain helper files such as:

```text
<skill-name>/
  SKILL.md
  scripts/       # optional helper scripts
  references/    # optional supplementary docs
  assets/        # optional static assets
```
