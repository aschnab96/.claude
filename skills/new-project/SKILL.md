---
name: new-project
description: Scaffold a new project from scratch with the correct structure, config files, and Claude setup. Run at the start of any new project before writing any code.
allowed-tools: Bash(mkdir *), Bash(git *), Bash(touch *), Bash(python *), Read
---

# New Project — Scaffold From Scratch

## Steps

### 1. Clarify before creating
Ask the user:
- What is the project name?
- What type? (web app / script / bot / library)
- What language/stack? (Python / JS / other)
- Will it run on a server or locally?
- Does it have a database?

Do not create anything until these are answered.

### 2. Create folders + .gitignore
```bash
mkdir -p <project-name>/.claude/skills
mkdir -p <project-name>/.claude/rules
mkdir -p <project-name>/docs
mkdir -p <project-name>/tests
mkdir -p <project-name>/scripts
git -C <project-name> init
```

Create `.gitignore` with at minimum:
- `.env`
- `__pycache__/`
- `*.pyc`
- `*.db`
- `*.log`
- Any key or credential files

For any data import or upload folders where you want to track folder structure
but not contents, use selective ignore with `.gitkeep`:
```
folder/*
!folder/.gitkeep
```
Never add a folder path directly to .gitignore if you want to track its
structure in git.

If Python project, create a virtual environment:
```bash
python3 -m venv <project-name>/venv
```
And add `venv/` to `.gitignore`.

### 3. Create CLAUDE.md
Place at the project root. Include:
- Project overview (one paragraph)
- Sensitive files list (never read, display, or commit)
- Session start instructions
- References section pointing to docs/

### 4. Create docs/SCHEMA.md
**Only if the project has a database** (wired to the "does it have a DB?"
answer from Step 1). Leave as a starter stub with table/column placeholders.
Skip entirely for non-database projects.

### 5. Create .claude/rules/
Add a project-specific rules file (e.g. `<project-name>.md`) covering:
- File and folder conventions
- Any tools or commands that must/must not be used
- Any security-sensitive paths

### 6. Copy skillify into .claude/skills/
```bash
cp ~/.claude/skills/skillify/SKILL.md <project-name>/.claude/skills/skillify/SKILL.md
```

### 7. Create docs/MODULE_MAP.md
Stub with labelled groups (A through I or however many make sense) ready to
fill in as the codebase grows.

### 8. Initial commit
Confirm the full structure with the user, then:
```bash
git -C <project-name> add .
git -C <project-name> commit -m "feat: scaffold <project-name> project structure"
```

### 9. Create GitHub remote and push
Check that the GitHub CLI is available:
```bash
gh --version
```
If not found, tell the user to install it and skip the rest of this step.

Ask the user: should the repo be public or private? Recommend private for
anything containing personal data, credentials, or sensitive configuration.

Create the remote and push in one command:
```bash
gh repo create <project-name> --private --source=. --remote=origin --push
# or --public if the user chose public
```

Confirm success:
```bash
git log --oneline
git remote -v
```
Show both outputs to the user.

## Hard rules
- Never create a project without a .gitignore
- Never skip CLAUDE.md — it's the model's entry point
- Never put credentials in any tracked file
- Never commit before Step 8 — all files must exist first
- Always confirm the structure with the user before the initial commit
- Never end scaffold with an unconnected local repo — always push to GitHub before closing
