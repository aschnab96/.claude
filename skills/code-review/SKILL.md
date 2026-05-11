---
name: code-review
description: Review code, a diff, or a file for correctness, security risks, best practice violations, and learning opportunities. Run after writing new code or before committing anything non-trivial.
allowed-tools: Read, Bash(git diff *), Bash(git log *)
---

# Code Review

## Steps

### 1. Get the target
If not specified, run `git diff HEAD` to get the latest changes.
If a file is specified, read it directly.

### 2. Review for correctness
- Does the logic do what it claims?
- Are there edge cases not handled?
- Are there off-by-one errors, null cases, or type mismatches?

### 3. Review for security
- Are credentials or secrets hardcoded or logged?
- Is user input sanitized?
- Are file paths validated?
- Flag any risk even if not asked

### 4. Review for best practices
- Is there duplicated logic that should be a function?
- Are functions doing more than one thing?
- Is error handling present and specific?
- Are variable names clear?

### 5. Learning callouts
For each issue found, explain:
- What the problem is
- Why it matters
- What the correct pattern looks like

### 6. Verdict
End with one of:
- SHIP IT — no issues found
- MINOR — small issues, list them, safe to ship after fixing
- HOLD — significant issues that must be fixed first

## Hard rules
- Never skip the learning explanation — this is a learning project
- Never just say "looks good" without checking all four areas
- Flag security issues even if everything else is fine
