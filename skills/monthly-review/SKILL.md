---
name: monthly-review
description: Run a structured monthly review of any project or system. Analyzes what worked, what almost worked, and proposes concrete improvements. Run at the end of each month or after enough data has accumulated.
allowed-tools: Read, Bash(git log *), Bash(python *), Bash(cat *)
---

# Monthly Review — Learning Loop

## Steps

### 1. Gather the data
Collect the month's outcomes:
- What was built or shipped?
- What failed or was skipped?
- What produced unexpected results?

### 2. Categorize outcomes
Sort into three buckets:
- WORKED — produced the intended result consistently
- ALMOST — close but something was off; these are the most valuable
- FAILED — didn't work, clear reason why

Do not skip the ALMOST bucket. That's where the learning lives.

### 3. Diarize the ALMOST cases
For each ALMOST outcome:
- What was the intended result?
- What actually happened?
- What was the gap?
- Was it a data problem, logic problem, or judgment problem?

### 4. Extract patterns
Look across all ALMOST and FAILED cases:
- Is there a recurring failure mode?
- Is there a step that consistently causes friction?
- Is there something being done manually that should be automated?

### 5. Propose concrete changes
For each pattern found, propose one of:
- A new skill file to encode the fix
- A change to an existing skill
- A deterministic script to replace latent judgment
- A rule to add to CLAUDE.md

Be specific. "Improve accuracy" is not a proposal.
"Add a validation step after X that checks Y" is.

### 6. Skillify any recurring fix
If a proposed change would prevent a recurring problem,
run `/skillify` to make it permanent infrastructure.

### 7. Write the summary
Produce a brief with:
- Month and project
- Top 3 wins
- Top 3 ALMOST cases and what they revealed
- Proposed changes (specific, actionable)
- One metric that would tell you if next month is better

## Hard rules
- Never skip the ALMOST bucket — wins and failures alone teach nothing
- Never propose vague improvements — every proposal must be specific
- Never run this without at least 2 weeks of data
- Always end with one measurable success metric for next month
