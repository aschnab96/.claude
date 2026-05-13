---
name: fix-pyright
description: Fix all Pyright type errors in the project — catalogue by group, explain each, fix one group at a time with approval
allowed-tools: Bash, Read, Edit, Write, LSP
---

# Fix Pyright Errors

## When to run
- User says "fix pyright errors" or "clean up type errors"
- Before a release or PR when a clean type check is required

## Steps

### 1. Get the current error count
Run pyright once and capture full output. Do NOT run it again until all
fixes are applied — pyright is slow and running it repeatedly pegs the CPU.

```bash
pyright 2>&1
```

If pyright hangs for more than 30 seconds, kill it and check:
- Is `venv/` excluded in `pyrightconfig.json`? If not, add it.
- Are there multiple pyright processes already running? Kill them first.

### 2. Catalogue errors by group
Read the full output and sort errors into groups by root cause — NOT by file.
Common groups:

| Group | Root cause | Fix type |
|-------|-----------|----------|
| Dead code directory | Missing imports in archived/unused files | Config exclusion |
| Module-level `= None` | Pyright infers type as `None` permanently | Type annotation |
| Wrong annotation | e.g. `params: dict = None` should be `dict \| None` | Fix the annotation |
| Possibly unbound variable | Variable assigned inside `try`, used in `finally` | Initialize before `try` |
| Union type missing method | e.g. `.sign()` not on all key types | `assert isinstance` narrowing |
| MagicMock attributes | `.return_value`, `.assert_called`, `.side_effect` on typed methods | `# type: ignore[attr-defined]` |
| Typeshed quirks | `signal.Handlers`, known stdlib typing gaps | `# type: ignore` |
| `Path` vs `str` | Passing `Path` object where `str` expected | `str(path)` at callsite |

### 3. Explain each group to the user
Before touching any file:
- State what the error is in plain language
- State whether it's a **real bug** or a **false positive**
- State the fix and why it's appropriate
- Rate your confidence

### 4. Fix one group at a time, lowest risk first
Order: config exclusions → annotation fixes → real bugs → false positive suppressions

For each group:
1. Propose the diff
2. Wait for explicit approval
3. Apply the fix
4. Confirm the diagnostics cleared (use LSP hover/diagnostics, not a new pyright run)

### 5. Run tests after all groups are done
```bash
venv/bin/python3.14 -m pytest -x --tb=short
```
If tests fail — stop and investigate before committing.

### 6. Run pyright once to confirm final count
One run only. If it hangs past 60 seconds, kill it — trust the VS Code
diagnostics panel instead. The editor extension and the CLI check the same
thing.

### 7. Commit
Use `/commit` skill.

## Fix patterns reference

### Config exclusion (dead code)
```json
{ "exclude": ["archive", "venv"] }
```

### Wrong default annotation
```python
# before
def foo(params: dict = None):
# after
def foo(params: dict | None = None):
```

### Possibly unbound in finally
```python
# before
try:
    conn = sqlite3.connect(path)
finally:
    conn.close()
# after
conn = None
try:
    conn = sqlite3.connect(path)
finally:
    if conn:
        conn.close()
```

### Type narrowing with assert isinstance
```python
assert isinstance(self.private_key, RSAPrivateKey)
sig = self.private_key.sign(...)
```

### MagicMock attributes in tests
```python
mock.method.return_value = {...}  # type: ignore[attr-defined]
mock.method.assert_not_called()   # type: ignore[attr-defined]
mock.method.side_effect = exc     # type: ignore[attr-defined]
```

### Module-level None variable
```python
# before
_db_conn = None
# after
_db_conn: sqlite3.Connection | None = None
```

## Hard rules
- NEVER run pyright more than once per session until all fixes are applied
- NEVER batch all fixes — one group at a time, one approval at a time
- NEVER use bare `# type: ignore` — always scope it: `[attr-defined]`, `[union-attr]`, `[index]`, `[arg-type]`
- NEVER suppress a real bug — distinguish false positives from genuine gaps
- NEVER skip the test run before committing
- Use LSP (hover, diagnostics) to verify fixes, not repeated pyright runs
