---
name: commit
description: Run tests and commit changes. Use after completing any task that modified code. Handles test verification, staging, commit message, and confirmation.
allowed-tools: Bash(git *), Bash(pytest *), Bash(python *), Read
---

# Commit — Test and Commit Changes

## Steps

1. Run `git status` and `git diff HEAD` — understand what changed
2. Run the test suite appropriate for this project
   - Python: `venv/bin/python3 -m pytest -x --tb=short`
   - If no test suite exists, flag it and skip
3. If tests fail — stop. Report the failure. Do not commit.
4. If tests pass — stage relevant files by name (never `git add -A`)
5. Propose a commit message focused on WHY not what:
   - Format: `type(scope): description`
   - Types: feat / fix / docs / test / refactor
6. Wait for explicit approval before running `git commit`
7. After commit, check if BACKLOG.md exists and scan for stale entries
   related to the files changed

## Hard rules
- Never use `git add -A` or `git add .`
- Never commit without showing the message first
- Never push unless explicitly asked
- Never amend a previous commit unless explicitly asked
