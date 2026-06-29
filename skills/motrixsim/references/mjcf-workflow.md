# MotrixSim MJCF Workflow

Use this reference for MJCF XML authoring, editing, debugging, and Python loading tasks that depend on MJCF structure.

## Lookup Protocol

1. Locate `motrixsim-docs-md`.
2. Read `mjcf_md/index.md`.
3. Use `Path Registry` to resolve the exact canonical path.
4. Read the file and heading for that path.
5. Use the documented attributes, required/default fields, and child relationships.

Useful commands:

```bash
sed -n '1,180p' <docs-path>/mjcf_md/index.md
rg -n '^## body/joint$|^## equality/joint$|Defaults Target' <docs-path>/mjcf_md
```

## Canonical Path Rules

- Use full paths, not bare tags.
- `body/joint`, `equality/joint`, and `tendon/fixed/joint` are different elements.
- `body/geom`, `asset/mesh`, and `default/geom` have different roles.
- `default/<tag>` is a defaults context. Read `Defaults Target` to find the actual element semantics.

## Authoring Pattern

When creating or editing MJCF:

1. Start from the XML structure requested by the user.
2. Resolve every nontrivial tag through `mjcf_md/index.md`.
3. For each tag, check:
   - allowed parent
   - child paths
   - required attributes
   - defaults behavior
   - Motphys-only `[MPEX]` markers
4. Keep XML minimal until it parses.
5. Add complexity only after a parse/load check passes.

## Validation

Prefer a real MotrixSim parse/load path. If the task is inside a repository, use its established commands. Otherwise run the smallest Python loader script available from the current API docs.

If validation cannot run:

- state whether the blocker is missing MotrixSim install, missing docs, missing assets, or an unsupported command;
- still report the exact docs paths used for the XML decisions.

## Common Pitfalls

- Bare `joint` is ambiguous. Resolve the path first.
- Defaults entries are not independent element definitions.
- Asset elements and body-attached elements can share tag names but have different paths.
- Do not copy MuJoCo-only attributes unless they appear in MotrixSim's `mjcf_md` docs.
