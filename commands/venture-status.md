---
description: Check the status of one or all ventures in the portfolio
argument-hint: "[venture-slug]"
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Bash
  - Agent
---

# /venture-status — Check Venture Status

## Input
Optional venture slug: `$ARGUMENTS`

## If No Slug Provided — Portfolio Overview

Read `portfolio/registry.md` and display the portfolio table:

```
## Portfolio Overview

| Venture | Stage | Health | MRR | Last Check | Next Action |
|---------|-------|--------|-----|------------|-------------|
```

Then ask: "Want details on a specific venture? Provide the slug."

## If Slug Provided — Venture Deep Dive

1. Pull latest from the venture repo:
   ```bash
   cd $PROJECTS_DIR/{slug} && git pull --quiet 2>/dev/null
   ```
   If not cloned, clone it first.

2. Read venture state files:
   - `CLAUDE.md` — context, stage, focus
   - `plans/current.md` — active plan and tasks
   - `docs/changelog.md` — recent changes
   - `metrics/` — KPIs (if any)
   - `decisions/` — recent decisions
   - Recent git log: `git log --oneline -5 --format="%ad %s" --date=short`

3. Display a comprehensive status:

```
## {Venture Name}

**Stage:** {stage} | **Health:** {score}/100 | **Type:** {type}

### Current Focus
{From CLAUDE.md current focus}

### Active Plan
{From plans/current.md — objectives and task completion status}

### Recent Activity
{Last 5 commits}

### Key Metrics
| Metric | Current | Target |
|--------|---------|--------|

### Recent Decisions
{From decisions/ — last 2-3}

### Recent Changes
{From changelog — last 2-3 entries}

### Agent Team
{From CLAUDE.md agent table}

**Repo:** https://github.com/{user}/{slug}
```
