---
description: Generate a comprehensive weekly board review across all ventures
argument-hint: ""
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - mcp__notion__notion-create-pages
  - mcp__notion__notion-fetch
  - mcp__notion__notion-search
  - mcp__notion__notion-update-page
---

# Weekly Review — Board-Level Portfolio Review

Generate a comprehensive weekly review of the entire portfolio.

## Step 1: Gather This Week's Data

### Daily Digests
Read all daily digests from this week in `digests/daily/`:
```
digests/daily/{monday-date}.md through digests/daily/{friday-date}.md
```

### Portfolio Registry
Read `portfolio/registry.md` for current state.

### Per-Venture State
For each active venture, pull latest and read:
- `CLAUDE.md`, `plans/current.md`, `docs/changelog.md`
- `metrics/` (all files)
- `decisions/` (this week's decisions)
- `learnings/` (this week's learnings)

### Previous Weekly Review
Read the most recent file in `digests/weekly/` for week-over-week comparison.

## Step 2: Generate Review

Spawn the `reporter` agent to generate the weekly review:

```
Generate a comprehensive weekly board review for the week ending {friday-date}.

Use this structure:

# Weekly Review — Week of {monday-date}

## Portfolio at a Glance

| Venture | Stage | Health | MRR | WoW MRR | Users | WoW Users |
|---------|-------|--------|-----|---------|-------|-----------|

**Total portfolio MRR:** ${total}
**Active ventures:** {count}
**Average health:** {avg}/100

## Per-Venture Review

### {Venture Name} ({stage})
**Health:** {score}/100 ({change from last week})

**This week's achievements:**
- {achievement 1}
- {achievement 2}

**Key metrics:**
| Metric | This Week | Last Week | Change |
|--------|-----------|-----------|--------|

**Decisions made:**
- {decision with rationale}

**Concerns:**
- {any issues or risks}

**Next week's focus:**
- {planned work}

{Repeat for each venture}

## Cross-Venture Insights

### Patterns
- {Patterns observed across ventures}

### Lessons Learned
- {New lessons from this week}

### Resource Allocation
- {Are we spending time on the right ventures?}

## Strategic Recommendations

{2-3 strategic recommendations for the founder based on this week's data}

## Pending Founder Decisions

| Venture | Decision Needed | Urgency | Context |
|---------|----------------|---------|---------|

## Looking Ahead

{What's coming next week across the portfolio}
```

## Step 3: Save Review

Write to `digests/weekly/{YYYY}-W{WW}.md`.

## Step 4: Update Knowledge

If any new cross-venture lessons were identified, append them to `knowledge/lessons.md`.

## Step 5: Update Notion

Create a new page in the "Digests" database:
- Title: "Weekly Review — Week of {monday-date}"
- Type: Weekly
- Content: Full review in Notion markdown

## Step 6: Display

If triggered manually, display the review to the founder.
