# MotrixSim Python Workflow

Use this reference for Python scripts, examples, API lookup, and debugging.

## Lookup Protocol

1. Locate `motrixsim-docs-md`.
2. Read `api_md/index.md`.
3. Search the API index for the class, function, module, or concept requested by the user.
4. Read the linked file or heading block for the exact symbol.
5. Use documented signatures and names in code.

Useful commands:

```bash
rg -n "Model|scene_from_file|load|step|viewer|render" <docs-path>/api_md
sed -n '1,200p' <docs-path>/api_md/index.md
```

Adjust the search terms to the user's task. Do not assume the examples above are correct for the current version.

## Implementation Pattern

When writing a MotrixSim Python program:

1. Decide whether the model source is MJCF, an existing asset, or programmatic construction.
2. Resolve the loading API from `api_md`.
3. Resolve any runtime/model/data access APIs from `api_md`.
4. Keep the first script minimal and runnable.
5. Add comments only where they clarify MotrixSim-specific API usage.

## Validation

Prefer the narrowest check:

```bash
python script.py
uv run python script.py
uv run pytest <test-file>
```

Use the command style already used by the target repository. If no environment is available, report the missing dependency or runtime.

## Error Handling

When a script fails:

1. Read the exact exception and stack frame.
2. Re-check the relevant API docs for the symbol and argument type.
3. If the failure is caused by MJCF input, switch to the MJCF workflow and inspect the canonical XML path.
4. Make the smallest correction and re-run.

## Avoid

- Do not invent aliases for API names.
- Do not use private or low-level APIs unless the docs or user explicitly require them.
- Do not write broad tutorial text when the user asked for working code.
