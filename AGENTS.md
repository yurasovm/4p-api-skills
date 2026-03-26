# 4Partners API Skills for AI Agents

This repository provides AI agent skills for the 4Partners Site API.

## Skills Overview

The skills in this repository allow AI agents to interact with the 4Partners API using natural language. Each skill is defined in the `skills/` directory.

## How to Use

Read the relevant `SKILL.md` file from the `skills/` directory to understand how to interact with each API module. Start with:

- `skills/article-browser/SKILL.md` — browse site variations and list articles
- `skills/bug-task-creator/SKILL.md` - 

## Authentication

All requests require the `X-Auth-Token` header:

```
X-Auth-Token: your-access-token-here
```

Get your token via `POST /auth/sign-in` or from your 4Partners admin panel.

## Safety

- Never log or expose the full auth token
- `article-browser` is strictly read-only — no write or delete operations
