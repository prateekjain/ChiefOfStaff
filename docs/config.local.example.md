# Local Configuration
# Copy this file to .claude/config.local.md and fill in your values.
# .claude/ is gitignored — your personal config stays private.

## Notion Database IDs

Set up a Notion integration and create the required databases, then paste the IDs here.
Agents read this file to know where to create/update entries.

- **ChiefOfStaff page**: `YOUR_NOTION_PAGE_ID`
- **Ventures database**: `YOUR_VENTURES_DB_ID` (data source: `YOUR_VENTURES_DATASOURCE_ID`)
- **Digests database**: `YOUR_DIGESTS_DB_ID` (data source: `YOUR_DIGESTS_DATASOURCE_ID`)
- **Decisions database**: `YOUR_DECISIONS_DB_ID` (data source: `YOUR_DECISIONS_DATASOURCE_ID`)

## MCP Servers

Agents reference MCP tools using the standard Claude.ai naming convention:
- `mcp__claude_ai_Notion__` — connect Notion via Claude.ai MCP integrations
- `mcp__claude_ai_HubSpot__` — connect HubSpot via Claude.ai MCP integrations
- `mcp__claude_ai_Miro__` — connect Miro via Claude.ai MCP integrations

No manual UUID mapping needed — just connect the services in Claude.ai and the tools become available automatically.

## Paths

- `$PROJECTS_DIR` = `/path/to/your/projects` (where venture repos get cloned)
- `$CHIEFOFSTAFF_DIR` = `/path/to/your/projects/ChiefOfStaff` (this repo)
