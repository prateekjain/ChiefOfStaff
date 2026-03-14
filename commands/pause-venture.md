---
description: Pause all work on a venture (state preserved, agents stop)
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - mcp__notion__notion-update-page
  - mcp__notion__notion-search
---

# /pause-venture — Pause a Venture

## Input
Venture slug: `$ARGUMENTS`

If no argument, ask: "Which venture should I pause? Provide the slug."

## Execution

1. Read `portfolio/registry.md` to confirm venture exists and is active
2. Update the venture's stage to PAUSED in `portfolio/registry.md`
3. Update venture repo `CLAUDE.md` — set stage to PAUSED, note the previous stage for resumption
4. Add a changelog entry: `[Milestone] Venture paused (was: {previous stage})`
5. Commit and push venture repo
6. Update Notion ventures database
7. Report: "{Venture Name} is now paused. All agent work stopped. State preserved. Use `/advance-venture {slug}` to resume."
