---
name: forge-memory-protocol
description: How ForgeBot agents read and write to the persistent memory system
metadata:
  author: forgebot
  version: "1.0.0"
---

# Forge Memory Protocol

## Overview

ForgeBot maintains three layers of persistent memory stored in GitHub repos.
Agents interact with memory through the `reflect` action.

## Memory Layers

### Layer 1: Episodic Memory (this session)
- The current conversation turns you can already see
- Automatically maintained — no action needed
- Lives in `discussions/forum-issue-{N}.md`

### Layer 2: Project Memory (cross-session, per repo)
- Architectural decisions, conventions, tech debt, completed features, lessons
- Stored in `forge-memory/{repo}/project.json`
- **You should update this** when something important is decided
- Injected into ALL agents at the start of each task

### Layer 3: Agent Memory (your personal memory, cross-project)
- Your strengths, experience, learned patterns, relationships
- Stored in `forge-agents/agents/{slug}/memory.json`
- Only you and the PO (summary) can read it
- Updated automatically after each task via auto-reflect

## When to Use `reflect`

Use `action: "reflect"` when:
- A significant architectural decision was made
- A new convention was established for the project
- You learned something that would help future tasks on this project
- An agent did something notably good or bad
- A mistake was made and you want to ensure it's not repeated

**The PO should reflect before declaring `ready` or `closed` on important tasks.**

## What to Include in Reflections

### Project Memory Updates
Record decisions that affect future work:
```json
{
  "type": "architectural_decision",
  "content": "Using CSS Modules for all new components in this project"
}
```
```json
{
  "type": "convention", 
  "content": "All API routes must have Zod validation before touching the database"
}
```
```json
{
  "type": "tech_debt",
  "content": "Auth middleware is duplicated in 3 routes — needs consolidation"
}
```
```json
{
  "type": "lesson_learned",
  "content": "Should spec the database schema before writing API routes, not after"
}
```

### Agent Feedback
Honest assessment of agent performance:
```json
{
  "agent": "functional-analyst",
  "feedback": "Amy's acceptance criteria were thorough but overly detailed for this scope — 40 criteria for a simple form is too much"
}
```

### Lessons Learned
Cross-cutting insights:
```json
"Always check existing components before creating new ones — found 3 duplicates this sprint"
```

## Memory Lifecycle

1. **Task starts** → Project memory and agent memory injected into prompts
2. **During task** → Agents work normally, memory is read-only
3. **Task ends (auto-reflect)** → PO reflects automatically, memory persisted
4. **Next task** → New memory available to all agents

## Context Budget

Memory is compressed if it exceeds the context budget (100K chars total).
The memory summarizer prioritizes:
1. Architectural decisions (never compressed)
2. Active conventions (never compressed)  
3. Recent lessons (last 10)
4. Older items (summarized)
