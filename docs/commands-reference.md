# Commands Reference

All commands are slash commands available in Claude Code when working in the ChiefOfStaff project.

## Venture Management

### `/new-venture "idea description"`

Evaluate a business idea, design an agent team, and bootstrap a venture repo.

**Arguments:**
- `idea description` (required) — A description of the business idea in quotes

**What it does:**
1. Strategist + researcher evaluate the idea (market size, competition, viability)
2. Produces an idea brief with go/no-go recommendation
3. If approved: chief-of-staff designs a custom agent team
4. Creates a private GitHub repo scaffolded with agents, skills, docs
5. Updates `portfolio/registry.md`
6. Creates a Notion entry in the Ventures database

**Example:**
```
/new-venture "AI-powered invoice tool for freelancers that auto-generates invoices from project tracking tools"
```

---

### `/venture-status [slug]`

Check the status of one or all ventures.

**Arguments:**
- `slug` (optional) — The venture slug. If omitted, shows all ventures.

**What it does:**
- If slug provided: pulls the venture repo, reads state files, reports stage, health, metrics, blockers, next actions
- If no slug: reads `portfolio/registry.md` and displays the portfolio table

**Examples:**
```
/venture-status ai-invoice-tool
/venture-status
```

---

### `/advance-venture slug`

Move a venture to the next lifecycle stage.

**Arguments:**
- `slug` (required) — The venture slug

**What it does:**
1. Reads current venture state and validates exit criteria for current stage
2. Presents evidence and recommendation to founder
3. On approval: updates stage in venture repo and portfolio registry
4. May add new agents to the venture (e.g., sales-ops at Launch, finance at Growth)
5. Updates Notion dashboard

**Example:**
```
/advance-venture ai-invoice-tool
```

---

### `/pause-venture slug`

Pause all work on a venture. State is preserved.

**Arguments:**
- `slug` (required) — The venture slug

**What it does:**
1. Sets venture stage to PAUSED in portfolio registry
2. Disables venture's scheduled tasks
3. Venture repo remains intact — can be resumed later

**Example:**
```
/pause-venture ai-invoice-tool
```

---

### `/kill-venture slug`

Archive a venture and capture learnings.

**Arguments:**
- `slug` (required) — The venture slug

**What it does:**
1. Generates a post-mortem document in the venture repo
2. Extracts key learnings into `knowledge/lessons.md` (cross-venture)
3. Sets venture stage to KILLED in portfolio registry
4. Archives the GitHub repo
5. Updates Notion dashboard

**Example:**
```
/kill-venture ai-invoice-tool
```

## Ecosystem Intelligence

### `/scout [focus-area]`

Discover and catalog AI ecosystem tools, frameworks, and MCP servers.

**Arguments:**
- `focus-area` (optional) — A specific area to focus the search on. If omitted, runs a broad sweep.

**What it does:**
1. Searches discovery sources (GitHub trending, HN, Product Hunt, awesome-lists, AI communities)
2. Evaluates discoveries: scores across adoption, recency, docs, relevance, community (0-100)
3. Creates/updates entry files in `knowledge/ecosystem/entries/`
4. Re-verifies entries older than 30 days (marks stale/deprecated as needed)
5. Rebuilds the catalog index (`knowledge/ecosystem/_index.md`)
6. Generates recommendations for active ventures (`knowledge/ecosystem/_recommendations.md`)

**Examples:**
```
/scout                        # Broad sweep across all categories
/scout mcp-servers            # Focus on new MCP servers
/scout marketplace-tools      # Tools for marketplace ventures
/scout content-generation     # Content creation and publishing tools
/scout web-scraping           # Web scraping and data extraction
```

---

## Reporting

### `/daily-briefing`

Generate today's portfolio digest.

**What it does:**
1. Reads all active venture states
2. Generates a digest covering: progress, metrics, decisions needed, blockers
3. Saves to `digests/daily/YYYY-MM-DD.md`
4. Updates Notion Digests database

**Example:**
```
/daily-briefing
```

---

### `/weekly-review`

Generate this week's board review.

**What it does:**
1. Reads all venture states and this week's daily digests
2. Generates comprehensive review: week-over-week trends, strategic insights, resource allocation
3. Saves to `digests/weekly/YYYY-WNN.md`
4. Updates Notion Digests database

**Example:**
```
/weekly-review
```

## Operations

### `/run-cycle`

Manually trigger an autonomous work cycle across all ventures.

**What it does:**
1. Reads portfolio registry
2. For each active venture (sorted by priority):
   - Pulls latest from GitHub
   - Runs health check
   - Determines what work is needed based on current stage
   - Spawns `claude --task` against the venture repo
3. Updates portfolio registry with new state

**Example:**
```
/run-cycle
```
