# 4Partners API Skills

> A 4Partners Site API Skills Library for AI coding assistants — skill modules for browsing and managing your e-commerce CMS.

Once installed, you can interact with the AI using natural language to explore articles, manage content, and work with site variations — no manual API coding required.

**Supported AI Assistants**: Cursor, Claude Code, and other AI coding assistants that support the skills mechanism.

---

## Quick Start

### Method 1: AI Conversation Install (Recommended)

Simply tell your AI:

> Set up the skills https://github.com/yurasovm/4p-api-skills

### Method 2: NPX Command Install

```bash
npx skills add yurasovm/4p-api-skills
```

---

## Authentication

All API requests require an `X-Auth-Token` header with your Bearer token.

```http
X-Auth-Token: your-access-token-here
```

Get your token via `POST /auth/sign-in` or from your 4Partners admin panel.

---

## Available Skills

### Article

| Skill               | Purpose                                                               | Auth Required | Mode      |
| ------------------- | --------------------------------------------------------------------- | ------------- | --------- |
| **article-browser** | Browse available site variations and retrieve paginated article lists | Yes           | Read-only |

---

## Skill Structure

```
skills/<skill-name>/
├── SKILL.md                    # Agent behavior instructions
├── agents/                     # Optional — agent interface config
│   └── openai.yaml
└── references/                 # Optional — detailed reference docs
    └── article-listing.md
```

Shared reference documents used across all skills:

```
skills/references/
├── authentication.md           # Token-based auth implementation
└── base-urls.md                # API base URLs and rate limits
```

---

## API Base URL

```
https://api.4partners.io/v1
```

Full OpenAPI spec: https://api.4partners.io/v1/doc/index.json

---

## Usage Examples

### article-browser

> "Show available article site variations"

> "List articles for the default variation"

> "Show active articles for the 'en' variation, sorted by publish date"

> "What article locales are configured on this site?"
