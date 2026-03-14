---
description: Discover, evaluate, and catalog AI ecosystem tools, then cross-reference against active ventures
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

# Ecosystem Scout — Discover and Catalog AI Tools

Discover new AI tools, evaluate them, update the ecosystem catalog, and generate recommendations for active ventures.

## Input

Focus area (optional): `$ARGUMENTS`

- If provided: focused sweep on that area (e.g., "mcp-servers", "marketplace-tools", "content-generation")
- If empty: broad sweep across all discovery sources

## Step 1: Read Current State

1. Read `knowledge/ecosystem/_index.md` for the current catalog
2. Read `knowledge/ecosystem/_categories.md` for taxonomy and scoring guide
3. Read `knowledge/ecosystem/_recommendations.md` for previous recommendations
4. Read `portfolio/registry.md` for active ventures and their stages
5. Read `knowledge/lessons.md` for relevant learnings

Note: Remember the current catalog entries so you can detect what's new vs. already cataloged.

## Step 2: Discovery Sweep

Spawn the `scout` agent to search for tools.

**If focus area provided (`$ARGUMENTS`):**
- Search specifically for tools related to `$ARGUMENTS`
- Use targeted queries: "{focus-area} AI tools", "{focus-area} open source", "{focus-area} MCP server"

**If broad sweep (no arguments):**
- Search GitHub trending for AI/ML repos (last week)
- Search for new MCP servers and integrations
- Search for new AI agent frameworks and tools
- Search for tools relevant to active venture types
- Check awesome-lists for recently added entries (awesome-mcp, awesome-ai-agents, etc.)

**For each discovery, collect:**
- Name, URL, description
- GitHub stars (if applicable), last commit date
- License
- Category and tags (per `_categories.md`)

**Target: 5-15 discoveries per sweep** (quality over quantity).

## Step 3: Evaluate Discoveries

For each discovered tool that isn't already in the catalog (or has changed significantly):

1. **Fetch the tool's homepage/README** to understand capabilities
2. **Score across 5 dimensions** (see `_categories.md` for scoring guide):
   - Adoption (0-20)
   - Recency (0-20)
   - Documentation (0-20)
   - Relevance (0-20)
   - Community (0-20)
3. **Classify** by category and tags
4. **Assess venture relevance** — which venture types and stages would benefit?
5. **Write entry file** to `knowledge/ecosystem/entries/{slug}.md`

Skip tools that score below 30 total — not worth cataloging.

## Step 4: Re-verify Existing Entries

Check entries in the catalog that were last verified more than 30 days ago:

1. Read the entry file
2. Quick web check — is the project still active? Any major changes?
3. Update score if the situation has changed
4. Mark status:
   - `active` — still maintained and relevant
   - `stale` — no updates in 6+ months, reduced score
   - `deprecated` — project archived or abandoned, set score to 0
   - `archived` — we've decided not to track this anymore

## Step 5: Rebuild Index

Rewrite `knowledge/ecosystem/_index.md` with all current entries:

- Include all entries with status `active` or `stale`
- Sort by score (highest first)
- Exclude `deprecated` and `archived` entries from the main table (list them in a separate section)

## Step 6: Generate Scout Report

Output a report summarizing:

### New Discoveries
| Tool | Category | Score | Why It Matters |
|------|----------|-------|----------------|

### Updated Entries
| Tool | Change | New Score |
|------|--------|-----------|

### Deprecated/Stale
| Tool | Reason |
|------|--------|

### Top Recommendations for Active Ventures
For each active venture, list the top 3 most relevant tools with integration suggestions.

## Step 7: Write Recommendations

Rewrite `knowledge/ecosystem/_recommendations.md` with current recommendations:

For each active venture in the portfolio:
1. Filter catalog for entries matching the venture's type and stage
2. Only include entries with Score >= 60
3. Classify each recommendation:
   - **Agent Enhancement** — improves an existing venture agent
   - **Skill Component** — can be incorporated into a workflow
   - **Future-Stage Addition** — valuable at a later stage
   - **Reference Only** — worth knowing about, no immediate action
4. Include integration notes for each

Update the "Last Updated" and "Active Ventures Considered" fields.
