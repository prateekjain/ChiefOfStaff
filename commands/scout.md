---
description: Discover and catalog AI ecosystem tools, frameworks, and MCP servers
argument-hint: "[focus-area]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Agent
  - WebSearch
  - WebFetch
  - mcp__contextportal__contextportal_search
  - mcp__contextportal__contextportal_semantic_search
  - mcp__contextportal__contextportal_deep_search
---

# /scout — Ecosystem Intelligence

Scan the AI ecosystem for tools, frameworks, and integrations. Evaluate and catalog discoveries, then generate recommendations for active ventures.

## Input
Focus area (optional): `$ARGUMENTS`

If no argument provided, run a broad sweep. If a focus area is given, concentrate the search there.

## Execution

Execute the `ecosystem-scout` skill with the provided arguments.

## Examples

```
/scout                        # Broad sweep across all categories
/scout mcp-servers            # Focus on new MCP servers
/scout marketplace-tools      # Tools for marketplace ventures
/scout content-generation     # Content creation and publishing tools
/scout web-scraping           # Web scraping and data extraction
```
