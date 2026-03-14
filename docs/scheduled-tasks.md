# Scheduled Tasks

ChiefOfStaff runs 24/7 via scheduled tasks registered through Claude Code's task infrastructure.

## Portfolio-Level Tasks (this repo)

### Morning Cycle
- **Schedule:** Daily at 8:00 AM
- **Duration:** ~15-30 min depending on portfolio size
- **What it does:**
  1. Reads `portfolio/registry.md` for all active ventures
  2. For each venture (sorted by priority):
     - `git pull` latest from venture repo
     - Read venture state (stage, backlog, blockers)
     - Determine what work is needed based on stage and backlog
     - Spawn `claude --task` against the venture repo with specific instructions
  3. Updates `portfolio/registry.md` with new state
  4. Logs activity to `digests/daily/` (appends if already exists)

**Priority order:**
1. Ventures with founder-requested work
2. Blocked ventures needing unblocking
3. Ventures closest to revenue (Launch/Growth)
4. Validation-stage ventures
5. Idea-stage ventures

### Evening Digest
- **Schedule:** Daily at 6:00 PM
- **Duration:** ~5-10 min
- **What it does:**
  1. Reads all venture states and today's activity log
  2. Generates portfolio digest covering:
     - Progress made today
     - Key metrics across ventures
     - Decisions needing founder input
     - Blockers and risks
     - Tomorrow's planned work
  3. Saves to `digests/daily/YYYY-MM-DD.md`
  4. Updates Notion Digests database

### Health Check
- **Schedule:** Every 6 hours
- **Duration:** ~5 min
- **What it does:**
  1. For each active venture: pull latest, read state
  2. Score health across dimensions:
     - **Progress velocity** — Is work moving forward?
     - **Market signals** — Any competitive changes?
     - **Financial health** — Revenue trends, costs
     - **Blockers** — Any unresolved blockers?
  3. Overall score: 0-100
  4. Flag any venture below threshold (< 50) for founder attention
  5. Update health scores in `portfolio/registry.md`

### Ecosystem Scout
- **Schedule:** Wednesday at 12:00 PM
- **Duration:** ~10-15 min
- **What it does:**
  1. Broad sweep across discovery sources (GitHub trending, HN, Product Hunt, awesome-lists)
  2. Evaluate and score all discoveries (0-100 across 5 dimensions)
  3. Re-verify entries older than 30 days (mark stale/deprecated)
  4. Rebuild `knowledge/ecosystem/_index.md` catalog
  5. Generate venture-specific recommendations in `_recommendations.md`
  6. Flag high-scoring discoveries (>= 80) for the evening digest
  7. Log summary to daily digest

**Why Wednesday noon:** Avoids contention with morning cycle (8AM) and evening digest (6PM). Catches weekend and early-week releases. `/scout` handles urgent or focused needs between sweeps.

### Weekly Review
- **Schedule:** Friday at 5:00 PM
- **Duration:** ~10-15 min
- **What it does:**
  1. Reads all venture states and this week's daily digests
  2. Generates comprehensive review:
     - Portfolio overview with week-over-week changes
     - Per-venture deep dive (metrics, achievements, concerns)
     - Strategic recommendations
     - Resource allocation assessment
     - Decisions made this week and their outcomes
  3. Saves to `digests/weekly/YYYY-WNN.md`
  4. Updates Notion Digests database

## Venture-Level Tasks (per venture repo)

Each venture can have its own scheduled tasks, set up during bootstrap and modified as the venture evolves.

### Common Venture Tasks

| Task | When | Purpose |
|------|------|---------|
| Research pulse | Daily | Monitor competitors, market news, relevant trends |
| Metric tracking | Daily | Pull and log key metrics (if data sources available) |
| Content publishing | As scheduled | Publish prepared content (posts, emails) |
| Customer monitoring | Daily | Check CRM for new leads, deal updates |
| Code health | Weekly | Review code quality, dependencies, security |

### How Venture Tasks Are Created

1. During bootstrap, the `venture-bootstrap` skill creates initial scheduled tasks based on the venture type and stage
2. As the venture progresses, the chief-of-staff may add new tasks or modify existing ones via `venture-evolve`
3. Tasks are defined as markdown files in the venture's `scheduled/` directory

## Task Registration

Tasks are registered using Claude Code's scheduled task infrastructure:

```bash
# Register a task (done by setup script or manually)
claude task create --schedule "0 8 * * *" --project /path/to/ChiefOfStaff --prompt "Execute morning-cycle.md"
```

The `scheduled/*.md` files contain the full task instructions that Claude reads and executes when the task runs.

## Monitoring Task Health

- Check task execution history: `claude task list`
- If a task fails, it logs the error and continues with the next task
- Failed tasks are flagged in the evening digest
- The health check will detect if a venture hasn't been updated recently (stale state)
