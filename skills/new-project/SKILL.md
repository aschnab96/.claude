---
name: new-project
description: Scaffold a new project from scratch with the correct structure, config files, and Claude setup. Run at the start of any new project before writing any code.
allowed-tools: Bash(mkdir *), Bash(git *), Bash(touch *), Bash(python *), Bash(echo *), Read
---

# New Project — Scaffold From Scratch

## Steps

### 1. Clarify before creating
Ask the user:
- What is the project name?
- What type? (web app / script / bot / library)
- What language/stack? (Python / JS / other)
- Will it run on a server or locally?

Do not create anything until these are answered.

### 2. Create directory structure
```bash
mkdir -p <project-name>/.claude/skills
mkdir -p <project-name>/.claude/hooks
mkdir -p <project-name>/.claude/rules
mkdir -p <project-name>/docs
mkdir -p <project-name>/tests
mkdir -p <project-name>/scripts
```

### 3. Initialize git
```bash
cd <project-name>
git init
```

**Checkpoint:** After running git init, confirm success with the user
before continuing. Run:
```bash
git status
```
Show the output to the user and wait for confirmation. The initial commit
happens at Step 10 only — after all files are created. Do not commit anything
before Step 10.

### 4. Create .gitignore
Include at minimum:
- `.env`
- `venv/`
- `__pycache__/`
- `*.pyc`
- `*.db`
- `*.log`
- Any key or credential files

For any data import or upload folders, use selective ignore to track folder structure but not contents:
```
folder/*
!folder/.gitkeep
```
Never add a folder path directly to .gitignore if you want to track its structure in git.

### 5. Create Python venv if Python project
```bash
python3 -m venv venv
```

### 6. Create docs/
Create these files with starter content:
- `CLAUDE.md` — project overview, file structure pointer, 
  session start instructions, sensitive files list
- `docs/MODULE_MAP.md` — empty groups A-I ready to fill
- `docs/BACKLOG.md` — empty, ready for tasks
- `docs/SCHEMA.md` — empty if DB project, skip if not

### 7. Copy global hooks
Copy protect-sensitive-files.sh from ~/.claude/hooks if it exists.
Adapt for this project's sensitive files.

### 8. Create settings.json
Basic `.claude/settings.json` with hook configuration for 
PreToolUse file protection.

### 9. Create skillify skill
Copy `~/.claude/skills/skillify/SKILL.md` into 
`.claude/skills/skillify/SKILL.md` and update any 
project-specific paths.

### 10. Initial commit
Stage everything and commit:
`feat: scaffold <project-name> project structure`

## Hard rules
- Never create a project without a .gitignore
- Never skip CLAUDE.md — it's the model's entry point
- Never put credentials in any tracked file
- Always confirm the structure with the user before the initial commit
