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

## MCP Server Mappings

When you connect MCP servers in Claude Code, each gets a UUID-based identifier.
Map them here so agents can reference them by friendly name.

- `mcp__notion__` → `mcp__YOUR-NOTION-MCP-UUID__`
- `mcp__hubspot__` → `mcp__YOUR-HUBSPOT-MCP-UUID__`
- `mcp__eraser__` → `mcp__YOUR-ERASER-MCP-UUID__`

## Paths

- `$PROJECTS_DIR` = `/path/to/your/projects` (where venture repos get cloned)
- `$CHIEFOFSTAFF_DIR` = `/path/to/your/projects/ChiefOfStaff` (this repo)
