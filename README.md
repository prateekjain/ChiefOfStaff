# ChiefOfStaff

**An autonomous multi-agent system that runs businesses end-to-end.**

One command to go from idea to running venture — with AI agents that evaluate markets, design custom teams, write code, ship products, and report back daily. All from markdown files.

```
/new-venture "AI-powered invoice tool for freelancers"
```

```
Strategist + Researcher evaluate viability
    → Market sizing, competitive analysis, go/no-go recommendation
    → Anti-sycophancy protocol: ideas get challenged, not cheerled

Chief-of-Staff designs a custom agent team
    → SaaS venture? → builder + marketer + sales-ops
    → Content business? → writer + seo-specialist + distribution

Private GitHub repo bootstrapped with agents, docs, skills
    → Agents work autonomously — research, build, market, iterate
    → RARV cycle: Reason → Act → Reflect → Verify

You get daily digests and weekly reviews on Notion
```

---

## Why ChiefOfStaff?

Most AI agent frameworks give you tools to build one agent. ChiefOfStaff is the **operating system above the agents** — it designs agent teams, manages their lifecycle, and runs them 24/7 across multiple ventures simultaneously.

| Feature | What it does |
|---------|-------------|
| **Two-level architecture** | Holding company agents manage portfolio; venture agents do the work |
| **Custom team design** | Each venture gets agents tailored to its type (SaaS, content, marketplace, API, e-commerce) |
| **Autonomous 24/7 operation** | Scheduled tasks run morning cycles, evening digests, health checks, weekly reviews |
| **Anti-sycophancy** | Strategist agent actively challenges ideas — blind review, forced pros/cons balance |
| **RARV work cycle** | Reason → Act → Reflect → Verify. Nothing ships without verification passing |
| **Stage-gated capabilities** | Ventures unlock tools (deploy, outreach, CRM) as they advance through stages |
| **Founder guardrails** | $0 spending, no external comms, no publishing without explicit approval |
| **Zero compiled code** | Everything is markdown + YAML. Agents, skills, commands, schedules — all plain text |

## Quick Start

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and authenticated
- [GitHub CLI](https://cli.github.com/) (`gh`) installed and authenticated
- (Optional) Notion integration via MCP for dashboards

### Setup

1. **Clone the repo**
   ```bash
   git clone https://github.com/prateekjain/ChiefOfStaff.git
   cd ChiefOfStaff
   ```

2. **Create your local config** — Copy the template and fill in your IDs:
   ```bash
   mkdir -p .claude
   cp docs/config.local.example.md .claude/config.local.md
   # Edit .claude/config.local.md with your Notion database IDs,
   # MCP server UUIDs, and local paths
   ```
   This file is gitignored — your personal config stays private. See [Setup Guide](docs/getting-started.md) for details.

3. **Launch your first venture**
   ```bash
   claude
   # Then type:
   /new-venture "your idea here"
   ```

### Commands

| Command | Description |
|---------|-------------|
| `/new-venture "idea"` | Evaluate a business idea and bootstrap a venture |
| `/venture-status [slug]` | Check status of one or all ventures |
| `/advance-venture slug` | Move a venture to its next lifecycle stage |
| `/pause-venture slug` | Pause work on a venture |
| `/kill-venture slug` | Archive a venture and capture learnings |
| `/scout [focus]` | Discover and catalog AI ecosystem tools |
| `/run-cycle` | Trigger an autonomous work cycle across all ventures |
| `/daily-briefing` | Generate today's portfolio digest |
| `/weekly-review` | Generate this week's board review |

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                    ChiefOfStaff Repo                         │
│                   (The Holding Company)                      │
│                                                              │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ ┌──────┐ │
│  │ Chief of │ │Strategist│ │Researcher│ │Reporter│ │Scout │ │
│  │ Staff    │ │          │ │          │ │        │ │      │ │
│  └────┬─────┘ └──────────┘ └──────────┘ └────────┘ └──────┘ │
│       │                                                      │
│       │ spawns claude --task                                 │
│       │                                                      │
├───────┼──────────────────────────────────────────────────────┤
│       ▼                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────┐         │
│  │ Venture A   │  │ Venture B   │  │ Venture C    │         │
│  │ (SaaS)      │  │ (Content)   │  │ (Marketplace)│         │
│  │             │  │             │  │              │         │
│  │ builder     │  │ writer      │  │ buyer-agent  │         │
│  │ marketer    │  │ seo-spec    │  │ seller-agent │         │
│  │ sales-ops   │  │ distro      │  │ trust-safety │         │
│  │             │  │             │  │ growth       │         │
│  │ Own repo    │  │ Own repo    │  │ Own repo     │         │
│  │ Own agents  │  │ Own agents  │  │ Own agents   │         │
│  └─────────────┘  └─────────────┘  └──────────────┘         │
└──────────────────────────────────────────────────────────────┘
```

### Repo Structure

```
ChiefOfStaff/
├── agents/              # 5 portfolio-level agents
│   ├── chief-of-staff.md    # Orchestrator — designs teams, runs cycles
│   ├── strategist.md        # Business evaluation, go/no-go decisions
│   ├── researcher.md        # Market research, competitive analysis
│   ├── reporter.md          # Daily digests, Notion dashboards
│   └── scout.md             # AI ecosystem tool discovery
├── skills/              # Reusable multi-step workflows
│   ├── venture-bootstrap/   # Scaffold a new venture repo
│   ├── deploy/              # Deploy to Vercel/Supabase
│   ├── daily-digest/        # Generate portfolio reports
│   └── ...
├── commands/            # Slash commands (user-facing)
├── templates/           # Venture repo scaffolding
│   ├── agents/              # Builder, marketer, QA, etc.
│   ├── docs/                # Architecture, requirements, etc.
│   ├── venture-claude.md    # CLAUDE.md template for ventures
│   └── continuity.md        # Cross-session state tracking
├── portfolio/           # Venture registry and guardrails
├── knowledge/           # Lessons, ecosystem catalog
├── scheduled/           # 24/7 autonomous task definitions
└── docs/                # System documentation
```

## Agents

### Portfolio Level (this repo)

| Agent | Role | Key Capability |
|-------|------|----------------|
| **Chief of Staff** | Orchestrator | Designs venture teams, runs RARV work cycles, manages tool access |
| **Strategist** | Business strategy | Go/no-go recommendations with anti-sycophancy protocol |
| **Researcher** | Market intelligence | TAM/SAM/SOM sizing, competitor analysis, trend identification |
| **Reporter** | Portfolio reporting | Daily digests, Notion dashboards, weekly board reviews |
| **Scout** | Ecosystem intelligence | Discovers and evaluates AI tools, scores on 5 dimensions |

### Venture Level (auto-designed per venture)

| Venture Type | Agent Team |
|-------------|------------|
| SaaS | builder, marketer, sales-ops, qa |
| Content/Media | writer, seo-specialist, distribution |
| Marketplace | buyer-agent, seller-agent, trust-safety, growth |
| API/Dev Tool | builder, devrel, docs-writer |
| E-commerce | product-curator, marketer, operations |

## Venture Lifecycle

```
IDEA → VALIDATION → MVP → LAUNCH → GROWTH → OPTIMIZATION → MATURE
                                                              ↘ KILLED
```

Each stage gates what tools ventures can access:

| Stage | Research | Build | Deploy | Publish | Outreach | CRM |
|-------|----------|-------|--------|---------|----------|-----|
| IDEA | Yes | - | - | - | - | - |
| VALIDATION | Yes | Yes | Landing page | Via approval | - | - |
| MVP | Yes | Yes | Full app | Via approval | - | - |
| LAUNCH | Yes | Yes | Yes | Via approval | Via approval | Yes |
| GROWTH+ | Yes | Yes | Yes | Via approval | Via approval | Yes |

## Development Methodology

Inspired by [Superpowers](https://claude.com/plugins/superpowers) and [Loki Mode](https://github.com/asklokesh/loki-mode):

- **RARV Cycle** — All work follows Reason → Act → Reflect → Verify. Verification is a gate, not a suggestion.
- **Anti-Sycophancy** — The strategist actively challenges ideas with blind review and forced balance of pros/cons.
- **TDD for Critical Paths** — Venture builders use red-green-refactor for business logic and APIs.
- **Systematic Debugging** — 4-phase methodology (reproduce → investigate → fix → verify) prevents going in circles.
- **Continuity Tracking** — Every venture maintains `continuity.md` so agents can pick up exactly where the last session left off.
- **Blocking Quality Gates** — Code isn't done until all quality checks pass. No exceptions.

## Guardrails

Built-in safety rails that apply to ALL agents across ALL ventures:

- All claims must be factual and verifiable — no fabricated testimonials or stats
- No dark patterns, spam, or deceptive practices
- Any expense > $0 requires founder approval
- No external messages (email, social, forums) without approval
- Stage transitions require founder approval
- All venture repos are private by default
- Deployments use free tiers only unless explicitly approved

See [portfolio/guardrails.md](portfolio/guardrails.md) for the full framework.

## Integrations

| Service | Purpose | Required? |
|---------|---------|-----------|
| **Claude Code** | Agent runtime | Yes |
| **GitHub** | Venture repos, version control | Yes |
| **Notion** | Dashboard, digests, approval queue | Recommended |
| **HubSpot** | CRM for Launch/Growth ventures | Optional |
| **Vercel** | Deployment (free tier) | Optional |
| **Supabase** | Database/auth (free tier) | Optional |

## Documentation

- [Architecture](docs/architecture.md) — System design, data flow, two-level agent model
- [Getting Started](docs/getting-started.md) — Setup and first venture walkthrough
- [Commands Reference](docs/commands-reference.md) — All commands with examples
- [Venture Lifecycle](docs/venture-lifecycle.md) — Stages and transition rules
- [Agent Design Guide](docs/agent-design-guide.md) — How agents are defined and staffed
- [Scheduled Tasks](docs/scheduled-tasks.md) — Autonomous 24/7 operation
- [Guardrails & Ethics](docs/guardrails-and-ethics.md) — Ethical framework and rules

## Contributing

Contributions welcome! Some areas where help is appreciated:

- **New venture type templates** — e-commerce, API/dev tools, mobile apps
- **Agent improvements** — better prompts, new capabilities
- **Integration guides** — connecting new tools and services
- **Documentation** — tutorials, walkthroughs, examples

## License

MIT — see [LICENSE](LICENSE) for details.

---

Built with [Claude Code](https://claude.ai/claude-code). The entire system — every agent, skill, command, and schedule — is just markdown files.
