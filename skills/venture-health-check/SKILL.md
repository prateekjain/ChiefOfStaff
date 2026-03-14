---
description: Check the health of one or all ventures and score them across dimensions
argument-hint: "[venture-slug]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
---

# Venture Health Check

Score venture health across multiple dimensions. Used by scheduled health checks and on-demand.

## Input

Optional venture slug: `$ARGUMENTS`
- If provided: check only that venture
- If empty: check all active ventures

## Step 1: Get Ventures

If slug provided, use it. Otherwise read `portfolio/registry.md` and get all ventures where stage is NOT KILLED, PAUSED, or MATURE.

## Step 2: For Each Venture

### 2a: Pull Latest
```bash
cd $PROJECTS_DIR/{slug} && git pull --quiet 2>/dev/null
```

If not cloned:
```bash
gh repo clone {user}/{slug} $PROJECTS_DIR/{slug} -- --quiet 2>/dev/null
```

### 2b: Read State Files

Read these files (skip if they don't exist):
- `CLAUDE.md` — venture context and focus
- `plans/current.md` — active plan, how many tasks completed vs pending
- `docs/changelog.md` — last entry date (recency of progress)
- `metrics/` — any metric files
- `decisions/` — recent decisions
- `learnings/` — any learnings captured

### 2c: Check Git Activity
```bash
cd $PROJECTS_DIR/{slug} && git log --oneline -10 --format="%h %ad %s" --date=short
```
This shows recent commit activity — a proxy for work being done.

### 2d: Score Health

Score 0-100 across these dimensions:

**Progress Velocity (0-25)**
- 25: Multiple commits this week, tasks being completed, changelog updated recently
- 15: Some activity this week but slow
- 5: No activity in the past week
- 0: No activity in 2+ weeks

**Plan Clarity (0-25)**
- 25: `plans/current.md` exists, has clear objectives and tasks, tasks are being checked off
- 15: Plan exists but is stale or vague
- 5: No clear plan
- 0: No `plans/current.md` at all

**Documentation Health (0-25)**
- 25: Key docs exist and are populated (not just templates), changelog is up to date
- 15: Docs exist but some are still templates/placeholders
- 5: Minimal documentation
- 0: No docs beyond initial scaffold

**Stage Appropriateness (0-25)**
- 25: Venture is doing work appropriate to its stage and making progress toward exit criteria
- 15: Work is appropriate but slow
- 5: Work seems misaligned with stage (e.g., building features during validation)
- 0: No evidence of stage-appropriate work

**Overall Score** = sum of all dimensions

**Health Levels:**
- 80-100: Healthy — operating well
- 60-79: Attention — some areas need improvement
- 40-59: Warning — significant issues, flag for founder
- 0-39: Critical — needs immediate founder attention

## Step 3: Update Registry

Update `portfolio/registry.md` with new health scores and last check date.

## Step 4: Flag Issues

If any venture scores below 50:
- Write a brief health alert explaining what's wrong
- Include in the output for the founder

## Step 5: Output

Display a health summary:

```
## Venture Health Check — {date}

| Venture | Stage | Health | Velocity | Plan | Docs | Stage Fit |
|---------|-------|--------|----------|------|------|-----------|
| {slug} | {stage} | {total}/100 | {v}/25 | {p}/25 | {d}/25 | {s}/25 |

{If any alerts:}
### Alerts
- **{slug}** ({score}/100): {brief description of issue}
```
