# Architecture

## Overview

ChiefOfStaff is a two-level autonomous multi-agent system for running businesses.

```
┌──────────────────────────────────────────────────────────┐
│                   ChiefOfStaff Repo                       │
│                  (The Holding Company)                     │
│                                                           │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ ┌──────┐│
│  │ Chief of │ │Strategist│ │Researcher│ │Reporter│ │Scout ││
│  │ Staff    │ │          │ │          │ │        │ │      ││
│  └────┬─────┘ └──────────┘ └──────────┘ └────────┘ └──────┘│
│        │                                                  │
│        │ spawns claude --task                             │
│        │                                                  │
├────────┼──────────────────────────────────────────────────┤
│        ▼                                                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐      │
│  │ Venture A   │  │ Venture B   │  │ Venture C   │      │
│  │ (SaaS)      │  │ (Content)   │  │ (Marketplace)│     │
│  │             │  │             │  │              │      │
│  │ builder     │  │ writer      │  │ buyer-agent  │      │
│  │ marketer    │  │ seo-spec    │  │ seller-agent │      │
│  │ sales-ops   │  │ distro      │  │ trust-safety │      │
│  │             │  │             │  │ growth       │      │
│  │ Own repo    │  │ Own repo    │  │ Own repo     │      │
│  │ Own agents  │  │ Own agents  │  │ Own agents   │      │
│  │ Own tasks   │  │ Own tasks   │  │ Own tasks    │      │
│  └─────────────┘  └─────────────┘  └──────────────┘      │
└──────────────────────────────────────────────────────────┘
```

## Level 1: ChiefOfStaff (This Repo)

The holding company has 5 portfolio-level agents:

### Chief of Staff (Orchestrator)
- Reads `portfolio/registry.md` to understand current state
- Evaluates new business ideas (delegates to strategist + researcher)
- Designs custom agent teams for each venture based on venture type
- Creates GitHub repos and scaffolds them with agents, skills, docs
- Spawns `claude --task` instances pointed at venture repos for execution
- Monitors portfolio via scheduled health checks

### Strategist
- Evaluates business viability: market size, competition, timing, differentiation
- Recommends go/no-go on new ideas
- Designs venture team composition based on venture type
- Provides strategic direction during stage transitions

### Researcher
- Deep web research: market sizing, competitor analysis, trend identification
- Customer persona development
- Validates assumptions with data
- Monitors market changes for active ventures

### Reporter
- Generates daily portfolio digests
- Updates Notion dashboard
- Produces weekly board reviews
- Creates health reports when issues are flagged

### Scout
- Discovers and evaluates AI ecosystem tools, frameworks, and MCP servers
- Maintains `knowledge/ecosystem/` catalog with scored entries
- Cross-references discoveries against active ventures
- Generates tool recommendations for venture staffing and stage transitions

## Level 2: Venture Repos

Each venture is a separate private GitHub repo. The repo structure is scaffolded by the `venture-bootstrap` skill using templates from `templates/`.

### Custom Agent Teams

The chief-of-staff designs each venture's agent team based on the venture type. Common patterns:

| Venture Type | Typical Agents |
|-------------|----------------|
| SaaS | builder, marketer, sales-ops, analytics |
| Content/Media | writer, seo-specialist, distribution, analytics |
| Marketplace | buyer-agent, seller-agent, trust-safety, growth |
| API/Dev Tool | builder, devrel, docs-writer, analytics |
| E-commerce | product-curator, marketer, operations, support |

Agent templates in `templates/agents/` provide a starting point. The chief-of-staff customizes them based on the specific venture's needs — modifying the role definition, adding venture-specific context, and adjusting tool access.

### Venture Autonomy

Once bootstrapped, ventures operate autonomously:
- Venture agents do the actual work (research, build, market)
- Changes are auto-committed and pushed to GitHub
- Venture-specific scheduled tasks drive continuous progress
- ChiefOfStaff monitors via health checks (reads venture state from repo)

## Data Flow

```
Founder                                  Notion Dashboard
   │                                          ▲
   │ /new-venture, /advance-venture          │ digests, decisions
   ▼                                          │
ChiefOfStaff ──── reads/writes ────► portfolio/registry.md
   │
   │ gh repo create + claude --task
   ▼
Venture Repos ──── auto-commit ────► GitHub (private)
   │
   │ agents read/write
   ▼
Venture State (docs/, metrics/, decisions/, learnings/)
```

## State Management

### ChiefOfStaff State
- `portfolio/registry.md` — lightweight table of all ventures (slug, repo, stage, health)
- `portfolio/guardrails.md` — rules that apply across all ventures
- `digests/` — archive of daily/weekly reports
- `knowledge/lessons.md` — cross-venture learnings

### Venture State (in each venture's repo)
- `docs/` — architecture, requirements, market research, business model, changelog
- `metrics/` — KPIs, revenue, users, conversion tracking
- `decisions/` — decision log with rationale
- `learnings/` — what worked, what didn't, pivots
- `plans/current.md` — current sprint/phase plan

### Notion State
- Ventures database — visual dashboard of all ventures
- Digests — daily/weekly reports as Notion pages
- Decisions — pending founder approvals

## Autonomous Operation

Four scheduled tasks drive 24/7 operation:

1. **Morning Cycle** (8 AM daily)
   - Read portfolio registry
   - For each active venture: pull latest, assess state, determine needed work
   - Spawn `claude --task` against venture repos to advance work

2. **Evening Digest** (6 PM daily)
   - Read all venture states
   - Generate portfolio digest
   - Update Notion dashboard

3. **Health Check** (every 6 hours)
   - Quick scan of all venture repos
   - Score health across dimensions (progress velocity, market signals, blockers)
   - Flag any venture below threshold

4. **Weekly Review** (Friday 5 PM)
   - Comprehensive cross-venture analysis
   - Week-over-week metric trends
   - Strategic recommendations

## Ecosystem Intelligence

The Scout agent maintains a continuously updated catalog of AI tools, frameworks, and integrations:

```
Ecosystem (GitHub, HN, ProductHunt, awesome-lists, etc.)
       │  WebSearch + WebFetch (weekly + on-demand)
       ▼
Scout Agent → knowledge/ecosystem/entries/*.md
       │       _index.md (lightweight catalog)
       ▼       _recommendations.md (for active ventures)
Venture Staffing → Team designs include ecosystem tools
       │
Venture Bootstrap → Agents configured with recommended tools
```

### Data Flow
- **Weekly sweep** (Wednesday noon): Scout scans discovery sources, evaluates tools, updates catalog
- **On-demand** (`/scout [focus]`): Targeted search for specific tool categories
- **Staffing integration**: venture-staffing skill consults catalog when designing teams
- **Strategist integration**: Strategist references catalog when recommending team composition
- **Chief-of-Staff integration**: Consults recommendations during stage transitions and when ventures are stuck

### Catalog Structure
- `knowledge/ecosystem/_index.md` — Lightweight table of all cataloged tools (sorted by score)
- `knowledge/ecosystem/_categories.md` — Taxonomy and scoring rubric
- `knowledge/ecosystem/_recommendations.md` — Current recommendations per active venture (regenerated each sweep)
- `knowledge/ecosystem/entries/{slug}.md` — Detailed entry per tool (capabilities, score breakdown, integration notes)

## Development Methodology

ChiefOfStaff embeds disciplined practices drawn from [Superpowers](https://claude.com/plugins/superpowers) and [Loki Mode](https://github.com/asklokesh/loki-mode):

### RARV Cycle (Reason → Act → Reflect → Verify)

All agents follow an iterative work loop:

```
Reason: Assess current state, identify the next task
    ↓
Act: Execute the work, commit changes
    ↓
Reflect: Update continuity.md, capture learnings
    ↓
Verify: Run quality gates — if fail, loop back to Act
```

The chief-of-staff applies RARV at the portfolio level (each work cycle). The builder agent applies it at the code level (each feature/fix).

### Anti-Sycophancy Protocol

The strategist agent evaluates ideas with deliberate bias correction:
- Blind review mindset — evaluate as if a stranger pitched the idea
- Forced balance — for every pro, actively search for a con
- Red flag detection — "however, with the right execution..." on a weak idea is a warning, not a save

### Continuity Tracking

Every venture repo includes `continuity.md`, updated at the end of every work session:
- What was done, what's next, blockers, open questions
- Ensures any agent (or future session) can resume without context loss

### Blocking Quality Gates

The builder agent's pre-ship checklist is blocking — work is not marked complete until all checks pass. Failed verification loops back to the Act phase with the error as input, preventing incomplete work from shipping.

### TDD for Critical Paths

Venture builders use red-green-refactor for core business logic and API endpoints. UI/styling work uses visual QA instead.

### Systematic Debugging

When bugs arise, agents follow a 4-phase protocol: Reproduce → Investigate → Fix → Verify. After 3 failed attempts, they must step back and review the architecture rather than continuing to iterate on symptoms.

## Technology Stack

- **Agent Framework**: Claude Agent SDK (markdown agents with YAML frontmatter)
- **Execution**: Claude CLI (`claude --task` for venture work)
- **Version Control**: GitHub (private repos, auto-commit/push)
- **Dashboard**: Notion (ventures database, digests, decisions)
- **Research**: WebSearch, WebFetch, ContextPortal
- **CRM**: HubSpot (for ventures in Launch/Growth stage)
- **Diagrams**: Eraser.io
