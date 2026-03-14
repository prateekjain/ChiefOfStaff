---
description: Generate today's portfolio digest
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

# /daily-briefing — Generate Daily Portfolio Digest

Execute the `daily-digest` skill to generate today's portfolio briefing.

This reads all active venture states, generates a digest covering progress, metrics, decisions needed, and blockers, saves it to `digests/daily/`, and updates Notion.
