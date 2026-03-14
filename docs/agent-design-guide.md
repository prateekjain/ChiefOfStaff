# Agent Design Guide

## How Agents Are Defined

Every agent is a markdown file with YAML frontmatter. This format is used consistently across ChiefOfStaff and all venture repos.

### Format

```yaml
---
name: agent-name
description: >
  Use this agent when [specific trigger conditions].
  [1-2 example scenarios].

model: inherit
color: color-name
tools:
  - Read
  - Write
  - Glob
  - Grep
  - WebSearch
  - mcp__tool_name__action
---

[Role definition in natural language]

**Core Identity:**
- [Key characteristic 1]
- [Key characteristic 2]

**Expertise Areas:**
- [Domain 1]
- [Domain 2]

**Principles:**
1. [Guiding principle]
2. [Another principle]

**When Working on This Venture:**
- [Venture-specific instruction]
- [Another instruction]

**Before Starting Work:**
- Read CLAUDE.md for venture context
- Check docs/ for current state
- Review plans/current.md for active priorities
```

### Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Kebab-case identifier (e.g., `sales-ops`) |
| `description` | Yes | When to use this agent — drives the orchestrator's routing decisions |
| `model` | Yes | Usually `inherit` (uses parent model) |
| `color` | No | UI color hint |
| `tools` | Yes | List of tools the agent can access |

## How the Chief-of-Staff Designs Venture Teams

When a new venture is approved, the chief-of-staff designs a custom agent team:

### 1. Analyze the Venture Type

The strategist categorizes the venture:
- **SaaS** — Software product with recurring revenue
- **Content/Media** — Content-driven business (blog, newsletter, course)
- **Marketplace** — Two-sided platform connecting buyers and sellers
- **API/Dev Tool** — Developer-facing product
- **E-commerce** — Physical or digital product sales
- **Service** — Service-based business (consulting, agency)

### 2. Select Agent Templates

Based on the venture type, select from `templates/agents/`:

| Template | Best for |
|----------|----------|
| `builder.md` | SaaS, API/Dev Tool, Marketplace |
| `marketer.md` | All ventures (after Validation) |
| `researcher.md` | All ventures (especially early stage) |
| `sales-ops.md` | SaaS, Service, B2B ventures |
| `finance.md` | All ventures (after Growth stage) |
| `writer.md` | Content/Media, any content-heavy venture |

### 2.5. Consult Ecosystem Catalog

Before finalizing the team, check `knowledge/ecosystem/_index.md` for tools that could enhance agents:

- Filter for tools with Score >= 60 that match the venture type
- **Agent Enhancement**: Tools that improve an existing agent's capabilities (e.g., a web scraping MCP server for the researcher)
- **Skill Component**: Tools that can be incorporated into venture skills/workflows
- **Future-Stage Addition**: Not needed now, but note for later stages
- Include relevant ecosystem tools in the team design output

### 3. Customize for the Venture

Templates are starting points. The chief-of-staff customizes:

- **Role definition** — Adjusted to the specific venture context
- **Venture-specific instructions** — E.g., "This is a B2B SaaS for accountants. Understand accounting workflows."
- **Tool access** — Add or remove tools based on venture needs
- **Principles** — Aligned with the venture's strategy and positioning

### 4. Create Additional Agents

For specialized ventures, the chief-of-staff may create entirely new agents:

- **support-agent** — For ventures with customer support needs
- **analytics-agent** — For data-heavy ventures
- **seo-specialist** — For content/SEO-driven ventures
- **devrel** — For developer-focused products
- **trust-safety** — For marketplaces
- **operations** — For e-commerce/logistics ventures

## Agent Template Library

Templates in `templates/agents/` provide the starting point:

### builder.md
Technical execution — architecture, coding, prototyping, deployment. Used for any venture that involves building software.

### marketer.md
Marketing strategy and execution — positioning, content, growth experiments, landing pages, distribution. Used for most ventures after Validation.

### researcher.md
Market intelligence — web research, competitive analysis, trend monitoring. Used in early stages and for ongoing market awareness.

### sales-ops.md
Revenue operations — CRM management, pipeline tracking, outreach strategy, deal management. Used for B2B and sales-driven ventures.

### finance.md
Financial governance — revenue tracking, unit economics, budget management, spending approval. Typically added at Growth stage.

### writer.md
Content creation — blog posts, documentation, email sequences, social media copy. Used for content-driven ventures.

## Agent Evolution

Venture agent teams evolve as the venture progresses through stages:

| Stage | Typical Team Changes |
|-------|---------------------|
| VALIDATION | Initial team (researcher + 1-2 others) |
| MVP | Builder added (if not already present) |
| LAUNCH | Marketer and/or sales-ops added |
| GROWTH | Finance agent added, growth-specific agents |
| OPTIMIZATION | Operations/automation agents may be added |

The chief-of-staff handles this via the `venture-evolve` skill (Phase B).

## Documentation Rules for Agents

Every agent must follow these documentation rules:

1. **Update relevant docs when making changes** — E.g., builder updates `docs/architecture.md`, marketer updates `docs/gtm-strategy.md`
2. **Log decisions** — Significant choices go in `decisions/` with rationale
3. **Track learnings** — What worked/didn't goes in `learnings/`
4. **Update changelog** — Milestones and pivots go in `docs/changelog.md`
