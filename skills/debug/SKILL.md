---
name: debug
description: Systematically debug a failing test, error, or unexpected behavior. Run when something is broken and the cause is not immediately obvious.
allowed-tools: Read, Bash(python *), Bash(git *), Bash(cat *), Bash(grep *)
---

# Debug — Systematic Debugging Workflow

## Steps

### 1. Understand the failure
Before touching any code ask:
- What is the exact error message or unexpected behavior?
- What was the last change made before this broke?
- Is this reproducible every time or intermittent?

Do not guess. Do not start fixing. Understand first.

### 2. Reproduce it
Run the failing code or test directly and confirm the error.
If you cannot reproduce it, stop and ask the user for more context.

### 3. Isolate the cause
- Check git log for recent changes near the failure
- Narrow to the smallest possible failing case
- Identify which layer failed: data, logic, or integration?
- Latent vs deterministic: is this a judgment failure or a 
  computation failure?

### 4. Fix one thing
- Propose one specific fix
- Explain what caused the bug so the user learns the pattern
- Show the diff before applying

### 5. Verify
- Re-run the failing test or reproduce case
- Run the full test suite to confirm no regressions

### 6. Skillify if recurring
Ask: could this class of bug happen again?
If yes — run `/skillify` to encode the fix as a permanent guard.

## Hard rules
- Never fix multiple things at once
- Never skip the explanation of what caused the bug
- Never commit a fix without running the full test suite
- If the root cause is unclear after step 3, ask — don't guess
