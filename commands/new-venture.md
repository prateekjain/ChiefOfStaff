---
description: Evaluate a new business idea, design an agent team, and bootstrap a venture repo
argument-hint: "<idea description in quotes>"
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
  - mcp__notion__notion-create-pages
  - mcp__notion__notion-update-page
  - mcp__notion__notion-search
  - mcp__notion__notion-fetch
  - mcp__contextportal__contextportal_search
  - mcp__contextportal__contextportal_semantic_search
  - mcp__contextportal__contextportal_deep_search
---

# /new-venture — Evaluate and Bootstrap a New Venture

Execute the full new venture pipeline: evaluate → staff → bootstrap.

## Input
The idea description: `$ARGUMENTS`

If no argument provided, ask: "What's the business idea you'd like to evaluate?"

## Execution

### Phase 1: Evaluate
Execute the `venture-intake` skill with the idea description.
This spawns strategist + researcher agents to produce an idea brief with a go/no-go recommendation.

### Phase 2: Founder Decision
Present the idea brief and wait for founder approval before proceeding.

### Phase 3: Staff (on approval)
Execute the `venture-staffing` skill with the venture slug.
This designs a custom agent team based on the venture type.

### Phase 4: Bootstrap (on approval)
Execute the `venture-bootstrap` skill with the venture slug.
This creates a private GitHub repo, scaffolds it, and pushes.

### Phase 5: Summary
Report the final state: repo URL, agent team, stage, next steps.
