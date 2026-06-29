# MotrixSim Docs Layout

Use this reference when locating or validating `motrixsim-docs-md`.

## Expected Repository

`motrixsim-docs-md` is a versioned documentation repository intended for code agents. It should be treated as generated reference material.

Recommended local storage for versioned docs:

```text
~/.motrixsim/docs-md/
├── 0.5.0-beta.1/
│   ├── api_md/
│   └── mjcf_md/
└── 0.5.0-beta.2/
    ├── api_md/
    └── mjcf_md/
```

Each version directory is a complete `motrixsim-docs-md` tree. Do not mix files from different version directories in one task.

If no repo-local or versioned local docs are found, the agent may download the docs from:

```text
https://github.com/Motphys/motrixsim-agent-docs.git
```

Clone or update it under `~/.motrixsim/motrixsim-agent-docs`, check out the tag that matches the target MotrixSim version, then copy or link the checkout root into `~/.motrixsim/docs-md/<version>`.

Expected per-version layout:

```text
<docs-version>/
├── api_md/
│   ├── index.md
│   └── ...
└── mjcf_md/
    ├── index.md
    ├── body.md
    ├── default.md
    └── ...
```

## Resolution Order

1. If the current repo contains `motrixsim-python/motrixsim-docs-md`, use that.
2. If the current repo contains `motrixsim-docs-md`, use that.
3. Determine the target MotrixSim version from the user request; if none was named, infer it from the current project.
4. Check only `~/.motrixsim/docs-md/<version>` for versioned local docs.
5. If that versioned local directory is missing, download or update `https://github.com/Motphys/motrixsim-agent-docs.git` at the matching tag.
6. If docs are still unavailable, report the exact blocker.

Useful commands:

```bash
find . -path '*/motrixsim-docs-md/api_md/index.md' -o -path '*/motrixsim-docs-md/mjcf_md/index.md'
ls -la ~/.motrixsim/docs-md/<version>
find ~/.motrixsim/docs-md/<version> -maxdepth 2 -path '*/api_md/index.md' -o -path '*/mjcf_md/index.md'
git clone https://github.com/Motphys/motrixsim-agent-docs.git ~/.motrixsim/motrixsim-agent-docs
git -C ~/.motrixsim/motrixsim-agent-docs fetch --tags --force
git -C ~/.motrixsim/motrixsim-agent-docs checkout <tag>
```

## How to Read

- Read index files first.
- Use registries to find exact files and headings.
- Prefer heading-level reads over whole-file reads when tools support it.
- Do not load the entire docs tree into context.

## Version Discipline

When the user targets a specific MotrixSim release, confirm the docs version if possible. If the docs version differs from the installed runtime, say so and avoid making unsupported claims.

Infer the current project's MotrixSim version in this order:

1. `<current-repo>/motrixsim-python/motrixsim-meta/pyproject.toml`, `[project] name = "motrixsim"` and `version`.
2. `<current-repo>/motrixsim-python/pyproject.toml`, `[project] version`.
3. `<current-repo>/motrixsim-python/motrixsim-core/pyproject.toml`, `[project] version`.
4. `<current-repo>/Cargo.toml`, workspace dependency `motrixsim = { ..., version = "..." }`.
5. `<current-repo>/motrixsim-python/motrixsim-core/Cargo.toml`, package `version`.

For the GitHub checkout tag, try `v<version>` first, then the exact version string if the `v`-prefixed tag does not exist.

If neither tag exists, list available tags and select the closest version that does not exceed the target version. Inform the user which docs version is being used and that it differs from the project version, then continue working. Do not block on a missing exact-match tag when a close alternative is available.

```bash
git -C ~/.motrixsim/motrixsim-agent-docs tag --list --sort=-version:refname
```

If no available tag is a reasonable match (e.g. all tags are for a much newer major version), report the situation and ask how to proceed. Do not fall back to the default branch unless the user explicitly permits it.

If a task does not specify a version and no repo-local docs are available, infer it from the current project before checking `~/.motrixsim`. If the requested or inferred version is not installed under `~/.motrixsim/docs-md/<version>`, check out the matching GitHub tag following the rules above.
