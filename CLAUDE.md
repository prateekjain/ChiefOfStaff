# CLAUDE.md — ChiefOfStaff Business Operating System

## Project Context

ChiefOfStaff is a two-level autonomous multi-agent system for running businesses end-to-end.

**Level 1 (this repo)**: The "holding company" — 4 portfolio-level agents that evaluate ideas, design venture teams, create repos, and monitor the portfolio.
**Level 2 (venture repos)**: Each venture is a separate private GitHub repo with its own custom agent team, skills, commands, and scheduled tasks.

There is no compiled code in this repo — all changes are markdown and YAML edits. Agents, skills, commands, and scheduled tasks are all markdown files with YAML frontmatter.

## Key File Relationships

```
agents/*.md          → skills/*/SKILL.md      (agents are invoked by skills)
skills/*/SKILL.md    → commands/*.md           (skills are triggered by commands)
commands/*.md        → scheduled/*.md          (commands can be run by scheduled tasks)
portfolio/registry.md ← all venture state      (lightweight index of all ventures)
templates/*          → venture repos           (templates are scaffolded into new repos)
docs/*               → describes this system   (must stay in sync with actual behavior)
```

## Agent Definitions

Agents are markdown files in `agents/` with YAML frontmatter:
```yaml
---
name: agent-name
description: When to use this agent
model: inherit
color: color-name
tools: [list, of, tools]
---
```
Followed by role definition, principles, and behavioral rules.

## Venture Repo Conventions

When scaffolding a new venture repo via `skills/venture-bootstrap/SKILL.md`:
- Always create a `CLAUDE.md` with venture-specific context, goals, and team
- Always create a `README.md` with venture overview and current status
- Always create `docs/` with architecture, requirements, market-research, business-model, changelog
- Always create custom agents tailored to the venture type
- Set up `.gitignore`, initial commit, push to GitHub as private repo
- Venture agents must update relevant docs when they make changes

## Documentation Rules

- `docs/` in this repo describes the ChiefOfStaff system itself
- Every change to agents, skills, commands, or scheduled tasks must be reflected in relevant docs
- `docs/commands-reference.md` must list all commands with current arguments and examples
- `docs/architecture.md` must reflect the actual system structure

## Workflow

1. **Plan First**: For changes touching 3+ files, write plan before starting.
2. **Verify**: Check that all cross-references resolve, all YAML is valid.
3. **Document**: Update docs in the same change that modifies behavior.
4. **Lessons**: After any correction, update `knowledge/lessons.md`.

## Portfolio State

- `portfolio/registry.md` — lightweight index of all ventures (slug, repo URL, stage, health)
- Venture details live in their own repos, not here
- `portfolio/guardrails.md` — ethical and spending rules that apply to ALL ventures

## Scheduled Tasks

Scheduled tasks in `scheduled/` define the 24/7 autonomous operation:
- Morning cycle (8 AM) — advance all ventures
- Evening digest (6 PM) — generate portfolio report → Notion
- Health check (every 6 hrs) — monitor venture health
- Weekly review (Friday 5 PM) — comprehensive portfolio review

## Tools Available

- **Notion** — primary reporting dashboard (ventures database, digests, decisions)
- **GitHub** (`gh` CLI) — create/manage venture repos
- **Claude CLI** (`claude --task`) — spawn Claude instances for venture work
- **WebSearch/WebFetch** — market research, competitive analysis
- **ContextPortal** — institutional memory and context retrieval
- **HubSpot CRM** — contact/deal management for ventures in Launch/Growth
- **Google Calendar** — scheduling
- **Eraser** — diagrams and visual documentation

## Notion Database IDs

These IDs are needed by agents when creating/updating Notion entries:

- **ChiefOfStaff page**: `YOUR_NOTION_PAGE_ID`
- **Ventures database**: `YOUR_VENTURES_DB_ID` (data source: `YOUR_VENTURES_DATASOURCE_ID`)
- **Digests database**: `YOUR_DIGESTS_DB_ID` (data source: `YOUR_DIGESTS_DATASOURCE_ID`)
- **Decisions database**: `YOUR_DECISIONS_DB_ID` (data source: `YOUR_DECISIONS_DATASOURCE_ID`)

<!-- SETUP: Replace the placeholder IDs above with your own Notion database IDs.
     You also need to configure MCP server IDs in your Claude settings:
     - mcp__notion__ → Your Notion MCP server UUID
     - mcp__hubspot__ → Your HubSpot MCP server UUID
     - mcp__eraser__ → Your Eraser MCP server UUID
     Set $PROJECTS_DIR and $CHIEFOFSTAFF_DIR environment variables to match your local paths. -->
