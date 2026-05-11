---
name: enrich
description: Research any person, company, topic, or concept and return a structured one-page brief. Use when you need to understand something before making a decision or starting a conversation.
allowed-tools: WebSearch(*), Read
---

# Enrich — Structured Research Brief

## Steps

### 1. Clarify the target
- What is being researched? (person / company / topic / concept)
- What is the purpose? (decision, conversation prep, learning)
- Are there specific questions to answer?

### 2. Search broadly first
Run 3-5 searches covering:
- Overview and background
- Recent developments (last 12 months)
- Controversies, risks, or open questions
- Relevance to the user's specific context

### 3. Cross-reference
Check at least 2 independent sources before treating anything 
as fact. Flag anything only found in one source.

### 4. Produce the brief
Structure the output as:

**[Name/Topic]**

WHAT IT IS
One paragraph. No jargon. What this actually is.

CURRENT STATE
What is true right now. Key facts, numbers, status.

RELEVANT TO YOU
How this connects to the user's specific context, goals, 
or current projects. Not generic — specific.

KEY RISKS OR OPEN QUESTIONS
What is uncertain, contested, or worth watching.

SOURCES
List the 2-3 most authoritative sources used.

### 5. Flag gaps
If something important couldn't be confirmed, say so explicitly.
Don't fill gaps with inference without flagging it.

## Hard rules
- Never present a single source as fact
- Never skip the "Relevant To You" section — generic research 
  is not useful
- Always include publication dates for time-sensitive claims
- If the topic is financial or medical, add a disclaimer that 
  this is research not advice
