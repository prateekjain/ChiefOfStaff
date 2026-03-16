---
description: Generate a portfolio-wide daily briefing and update Notion
argument-hint: ""
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - mcp__claude_ai_Notion__notion-create-pages
  - mcp__claude_ai_Notion__notion-fetch
  - mcp__claude_ai_Notion__notion-search
  - mcp__claude_ai_Notion__notion-update-page
---

# Daily Digest — Portfolio Briefing

Generate the founder's daily briefing across all ventures.

## Step 1: Read Portfolio State

Read `portfolio/registry.md` to get all active ventures (exclude KILLED, PAUSED, MATURE).

## Step 2: Gather Venture States

For each active venture, read its state. Use `Bash` to pull latest if the repo is cloned locally:

```bash
cd $PROJECTS_DIR/{slug} && git pull --quiet 2>/dev/null
```

Then read:
- `CLAUDE.md` — for venture context and current focus
- `plans/current.md` — for active plan and task status
- `metrics/` — for latest KPIs (if any files exist)
- `decisions/` — for recent decisions (check dates)
- `docs/changelog.md` — for recent changes

If the venture repo isn't cloned locally, use:
```bash
gh repo clone {user}/{slug} $PROJECTS_DIR/{slug} -- --quiet 2>/dev/null
```

## Step 3: Generate Digest

Spawn the `reporter` agent to generate the digest:

```
Generate a daily portfolio digest for today ({date}).

Data for each venture:
{pass the state data gathered in Step 2}

Use this format:

# Daily Briefing — {date}

## Decisions Needed
- [Venture] What needs founder input and why

## Progress Today
| Venture | Stage | Activity | Result |
|---------|-------|----------|--------|

## Key Metrics
| Venture | MRR | Users | Health | Trend |
|---------|-----|-------|--------|-------|

## Blockers
- [Venture] What's blocked and what would unblock it

## Tomorrow's Plan
- [Venture] What agents will work on next

If there are no decisions needed, omit that section.
If a venture has no metrics yet (early stage), show "—" for metrics.
Keep it concise — the founder should be able to scan this in 2 minutes.
```

## Step 4: Save Digest

Write the digest to `digests/daily/{YYYY-MM-DD}.md`.

## Step 5: Update Notion

Search for the "Digests" database in Notion and create a new page:
- Title: "Daily Briefing — {date}"
- Type: Daily
- Content: The full digest in Notion markdown format

Also update the "Ventures" database entries with latest health scores and activity dates.

## Step 6: Display to User

If this was triggered manually (not by scheduled task), display the digest to the founder.
