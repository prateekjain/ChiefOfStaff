---
description: Trigger an autonomous work cycle across all active ventures
argument-hint: "[venture-slug]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - WebSearch
  - WebFetch
  - mcp__notion__notion-update-page
  - mcp__notion__notion-search
  - mcp__contextportal__contextportal_search
  - mcp__contextportal__contextportal_semantic_search
  - mcp__contextportal__contextportal_deep_search
---

# /run-cycle — Autonomous Work Cycle

Manually trigger an autonomous work cycle. The chief-of-staff reads the portfolio, prioritizes ventures, and spawns work for each.

## Input
Optional venture slug: `$ARGUMENTS`
- If provided: run cycle for only that venture
- If empty: run cycle for all active ventures

## Execution

Spawn the `chief-of-staff` agent with this prompt:

```
Run an autonomous work cycle.

1. Read portfolio/registry.md to get all active ventures (or just {slug} if specified).
2. Sort by priority:
   - Blocked ventures first
   - Ventures closest to revenue (Launch/Growth)
   - Validation-stage ventures
   - Idea-stage ventures
3. For each venture:
   a. Pull latest from the venture repo
   b. Read CLAUDE.md, plans/current.md, docs/changelog.md
   c. Determine what work is needed based on current stage and plan
   d. Spawn claude --task against the venture repo with specific instructions:
      - What agents should work on
      - What the expected outputs are
      - Remind about guardrails and doc maintenance
   e. After the task completes, update portfolio/registry.md with latest state
4. After all ventures processed, provide a summary of what was done.

When spawning claude --task for a venture:
- Set the working directory to the venture repo
- Provide clear, specific instructions about what to work on
- Reference the venture's plans/current.md for priorities
- Remind agents to commit and push their work
- Remind agents to update docs alongside their work

Example:
claude --task "You are working on the {venture-name} venture. Read CLAUDE.md for context.
Your current plan is in plans/current.md. Work on the highest-priority uncompleted task.
After completing work, commit with a descriptive message and push. Update relevant docs."
--cwd $PROJECTS_DIR/{slug}
```

## After Cycle

Display a cycle summary:

```
## Work Cycle Complete — {date} {time}

| Venture | Stage | Work Done | Commits | Status |
|---------|-------|-----------|---------|--------|

{Any issues or blockers encountered}
{Any decisions that need founder input}
```
