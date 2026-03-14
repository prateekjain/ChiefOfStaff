---
description: Archive a venture and capture learnings
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - mcp__notion__notion-update-page
  - mcp__notion__notion-search
---

# /kill-venture — Archive a Venture

## Input
Venture slug: `$ARGUMENTS`

If no argument, ask: "Which venture should I archive? Provide the slug."

## Step 1: Confirm

Read venture state and display:
```
You're about to kill {Venture Name} (stage: {current stage}).
This will:
- Archive the GitHub repo
- Set stage to KILLED in the portfolio
- Extract learnings to the cross-venture knowledge base

Are you sure? This cannot be undone.
```

Wait for founder confirmation.

## Step 2: Generate Post-Mortem

Pull latest from venture repo and read all state files. Generate a post-mortem:

```markdown
# Post-Mortem: {Venture Name}

**Killed:** {date}
**Stage at death:** {stage}
**Duration:** {days since start}

## What was the idea?
{One-paragraph summary}

## What worked?
- {Things that went well}

## What didn't work?
- {Things that failed or underperformed}

## Key learnings
1. {Learning 1}
2. {Learning 2}
3. {Learning 3}

## Would we try this again?
{Under what conditions, if any, would this idea be worth revisiting?}

## Final metrics
| Metric | Final Value |
|--------|------------|
```

Write to venture repo `learnings/post-mortem.md`.

## Step 3: Extract Cross-Venture Learnings

Append key learnings to ChiefOfStaff `knowledge/lessons.md` with proper format:
```
## {date}: [{Category}] {Short title from venture}

**What happened**: {context}
**Why it happened**: {root cause}
**Lesson**: {takeaway to apply to future ventures}
**Applies to**: {venture types or stages}
```

## Step 4: Archive

1. Commit and push post-mortem to venture repo
2. Archive the GitHub repo: `gh repo archive {user}/{slug} --yes`
3. Update `portfolio/registry.md` — set stage to KILLED
4. Update Notion ventures database

## Step 5: Report

```
{Venture Name} has been killed and archived.

Key learnings captured:
{List the learnings extracted}

The GitHub repo is archived at https://github.com/{user}/{slug} (read-only).
```
