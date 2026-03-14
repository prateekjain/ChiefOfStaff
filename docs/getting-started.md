# Getting Started

## Prerequisites

1. **Claude CLI** — Install and authenticate: [docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-cli)
2. **GitHub CLI** — Install and authenticate: [cli.github.com](https://cli.github.com/)
   ```bash
   gh auth status  # Verify you're authenticated
   ```
3. **Notion MCP** — Configure Notion integration in your Claude Code MCP settings
4. **ContextPortal** (optional) — For institutional memory and context retrieval

## Setup

1. Clone this repo:
   ```bash
   git clone git@github.com:YOUR_USER/ChiefOfStaff.git
   cd ChiefOfStaff
   ```

2. Open in Claude Code:
   ```bash
   claude
   ```

3. The system is ready. All agents, skills, and commands are markdown files — no build step needed.

## Your First Venture

### Step 1: Submit an Idea

```
/new-venture "AI-powered invoice tool for freelancers"
```

This triggers a three-phase process:

1. **Evaluation** — The strategist and researcher agents evaluate your idea:
   - Market size and growth
   - Competitive landscape
   - Differentiation potential
   - Go/no-go recommendation

2. **Team Design** — If the idea passes evaluation, the chief-of-staff designs a custom agent team:
   - Analyzes what type of venture this is (SaaS, content, marketplace, etc.)
   - Selects appropriate agents from the template library
   - Customizes agents with venture-specific context

3. **Bootstrap** — A private GitHub repo is created and scaffolded:
   - Custom agents, skills, and commands
   - Documentation templates (architecture, requirements, market research, etc.)
   - CLAUDE.md with venture context
   - Initial commit pushed

### Step 2: Check Status

```
/venture-status ai-invoice-tool
```

This pulls the latest from the venture repo and reports current state, stage, health score, and next actions.

Or check all ventures:

```
/venture-status
```

### Step 3: Let It Run

The system works autonomously via scheduled tasks:
- **8 AM**: Morning work cycle — agents advance work on each venture
- **6 PM**: Daily digest — you get a summary on Notion
- **Every 6 hours**: Health checks — problems get flagged

### Step 4: Advance Stages

When a venture's exit criteria are met, advance it to the next stage:

```
/advance-venture ai-invoice-tool
```

This may add new agents (e.g., adding a sales-ops agent when moving to Launch).

### Step 5: Review

```
/daily-briefing     # Today's portfolio digest
/weekly-review      # This week's board review
```

## Managing Your Portfolio

### Pause or Kill Ventures

```
/pause-venture slug      # Pause work (agents stop, state preserved)
/kill-venture slug       # Archive venture, capture learnings
```

### Manual Work Cycle

Trigger an autonomous work cycle on demand:

```
/run-cycle
```

## What Happens in Each Stage

| Stage | What Agents Do |
|-------|---------------|
| **IDEA** | Strategist evaluates, researcher scans market |
| **VALIDATION** | Research demand signals, design experiments, test landing pages |
| **MVP** | Builder architects and codes, marketer prepares launch |
| **LAUNCH** | Go-to-market execution, initial outreach, first users |
| **GROWTH** | Growth experiments, funnel optimization, scaling |
| **OPTIMIZATION** | Unit economics, cost reduction, automation |
| **MATURE** | Maintenance, monitoring, incremental improvements |

## Next Steps

- Read [Architecture](architecture.md) for the full system design
- Read [Commands Reference](commands-reference.md) for all available commands
- Read [Venture Lifecycle](venture-lifecycle.md) for detailed stage descriptions
- Read [Guardrails & Ethics](guardrails-and-ethics.md) for operating rules
