# ForgeBot Discussion Agents

Agent prompts for **non-dev** roles used by ForgeBot's orchestration engine (OpenAI API).

These agents participate in the **discussion phase** before any code is written.
They are NOT Copilot custom agents — they are executed by ForgeBot via the OpenAI API.

## How it works

1. A GitHub issue is created with the `forgebot` label
2. ForgeBot reads `catalog.json` to discover available agents
3. ForgeBot starts the **Product Owner** agent (always first)
4. The PO orchestrates: cites other agents, reviews their output, makes decisions
5. When the PO says "ready", ForgeBot generates a brief and assigns Copilot to implement

## Adding a new agent

1. Create `roles/your-agent.md` with the prompt
2. Add an entry to `catalog.json`
3. The PO will automatically see the new agent in its available list

## Structure

```
catalog.json          ← Index of available agents
roles/
├── product-owner.md  ← Orchestrator (always runs first)
├── functional-analyst.md
├── ux-designer.md
└── ...               ← Add more here
```

## Dev agents

Agents that **write code** (senior-react-dev, backend-dev, etc.) live in
[`Johanson1988/.github/agents/`](https://github.com/Johanson1988/.github/tree/main/agents)
as Copilot custom agents. They are NOT in this repo.
