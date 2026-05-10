---
name: skillify
description: Convert a working solution or recent failure into a permanent skill. Run when something worked and will repeat, or when a bug is fixed and must never recur.
allowed-tools: Bash(git log:*), Read
---

# Skillify — Make It Permanent

## When to run
- You just fixed a bug
- You just built something that will repeat
- User says "remember this" or "make this permanent"

## Steps

### 1. Name and describe the skill
- Short kebab-case name
- One-line description that triggers naturally
  (ask: "what would I say to invoke this?")
- Description must be specific enough not to overlap with other skills

### 2. Determine scope
Ask: is this habit universal or project-specific?
- Universal (any project) → create in `~/.claude/skills/<name>/`
- Project-specific (paths, APIs, domain logic) → create in 
  `.claude/skills/<name>/` inside the project

### 3. Create the skill file
SKILL.md with:
- Frontmatter: name, description, allowed-tools
- Clear steps
- Hard rules and what NOT to do
- Any deterministic scripts referenced

### 4. Identify deterministic work
Is any step doing computation or lookup a script could handle?
If yes — write the script. The skill calls it; Claude interprets output.

### 5. Update the project's MODULE_MAP.md if project-level
Add to the skills group with name and description.

### 6. Verify it's reachable
Is the description specific enough to invoke naturally?
Does it overlap with any existing skill description?

### 7. Commit
`feat(skills): add /<name> skill — <one line why>`

## What a complete skill looks like
- SKILL.md with frontmatter ✓
- Deterministic scripts if needed ✓
- MODULE_MAP.md updated if project-level ✓
- No description overlap with existing skills ✓
