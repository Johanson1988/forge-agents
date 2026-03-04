---
name: forge-communication-protocol
description: How ForgeBot agents communicate with each other via forge-comms repo
metadata:
  author: forgebot
  version: "1.0.0"
---

# Forge Communication Protocol

## Overview

Agents communicate asynchronously via the `forge-comms` GitHub repository.
Messages are stored as JSONL files. All inter-agent communication goes through this system.

## When to Use Communication Actions

### `send_message`
Use when you want to proactively notify another agent:
- Share a decision that affects their work: `"type": "decision"`
- Report a blocker that requires another agent's input: `"type": "blocker"`
- Recognize great work: `"type": "kudos"`
- Ask a question that doesn't need to be in the main discussion: `"type": "question"`

Example payload:
```json
{
  "action": "send_message",
  "message": "Sending Lily a note about the spacing tokens",
  "sendMessage": {
    "to": "ux-designer",
    "type": "question",
    "content": "Hey Lily! For the new card component, should we use spacing-4 or spacing-6 between elements? Asking because Amy's spec says 'comfortable spacing' but I need the actual token. — Chandler",
    "priority": "normal"
  }
}
```

### `read_messages`
Use at the start of a new task or when you suspect there are relevant messages waiting:
- Check inbox before making a decision that could be outdated
- Read a project channel to get context about recent activity
- Read DMs with a specific agent to catch up on a conversation

Example payload:
```json
{
  "action": "read_messages",
  "message": "Checking my inbox for any pending context before deciding",
  "readMessages": {
    "source": "inbox",
    "limit": 10
  }
}
```

## Message Types Reference

| Type | When to use |
|---|---|
| `suggestion` | You have an idea that could improve the current work |
| `question` | You need information from another agent |
| `response` | Answering a previous message |
| `decision` | Announcing a decision that affects others |
| `blocker` | You are blocked and need another agent's input |
| `kudos` | Recognizing excellent work by another agent |
| `alert` | Something important that needs immediate attention |
| `standup` | Daily status update (automated by CRON) |

## Etiquette Rules

1. **Be concise** — messages are asynchronous, keep them to the point
2. **Sign your messages** — always end with "— [Your Character Name]"
3. **Reference issues** — include relevant issue numbers: `refs: ["#42"]`
4. **Mark responses** — if responding to a message, use `type: "response"`
5. **Don't spam** — one message per topic, not multiple follow-ups in quick succession
6. **Read before you write** — always read your inbox before sending new messages
7. **Escalate blockers** — if a blocker is unresolved for 2+ turns, report it to the PO

## Channel Guide

| Channel | Purpose |
|---|---|
| `inbox/{slug}` | Your personal notifications and messages |
| `dm/{a}--{b}` | Private conversation between two agents |
| `channels/general` | Team-wide announcements |
| `channels/standups` | Daily standup posts |
| `channels/project-{repo}` | Project-specific channel |

## Priority Levels

- `urgent` — needs attention in the current turn
- `normal` — standard priority, check when you wake up  
- `low` — informational, no action required
