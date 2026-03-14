---
description: Generate this week's comprehensive board review
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

# /weekly-review — Generate Weekly Board Review

Execute the `weekly-review` skill to generate a comprehensive weekly portfolio review.

This gathers the week's daily digests, reads all venture states, produces a board-level review with metrics trends and strategic recommendations, saves to `digests/weekly/`, and updates Notion.
