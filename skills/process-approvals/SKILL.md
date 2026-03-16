---
description: Process approved items from the Notion Decisions DB — deploy, publish, or send as appropriate
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - mcp__claude_ai_Notion__notion-fetch
  - mcp__claude_ai_Notion__notion-update-page
  - mcp__claude_ai_Notion__notion-search
  - mcp__Claude_in_Chrome__navigate
  - mcp__Claude_in_Chrome__read_page
  - mcp__Claude_in_Chrome__get_page_text
  - mcp__Claude_in_Chrome__form_input
  - mcp__Claude_in_Chrome__computer
  - mcp__Claude_in_Chrome__find
  - mcp__Claude_in_Chrome__javascript_tool
---

# Process Approvals

Check the Notion Decisions DB for approved items and execute them. This skill is run by ChiefOfStaff at the start of every work cycle.

## Step 1: Fetch Approved Items

Search the Decisions database (ID: `YOUR_DECISIONS_DB_ID`) for items where Status = "Approved".

## Step 2: Process Each Approved Item

For each approved item, execute based on Type:

### Deployment
1. Read the Context field for deployment details
2. Run the `deploy` skill for the specified venture
3. Update the Decisions DB entry: add "Executed on {date}" to Context
4. Update Status to indicate completion (add a note — keep Status as Approved so founder sees it was done)

### Content
1. Read the Context field for the full content draft and target channel
2. Use Chrome MCP to navigate to the target platform (Twitter/X, LinkedIn, blog, etc.)
3. Post the content
4. Save a copy to the venture's `marketing/published/{date}-{title}.md`
5. Log in the venture's `docs/changelog.md`
6. Update the Decisions DB entry with the published URL

### Outreach
1. Read the Context field for target, channel, and message
2. Use Chrome MCP to navigate to the platform (email, social DM, forum)
3. Send the message
4. Log in the venture's `data/outreach-log.md`:
   ```
   | {date} | {channel} | {target} | {subject/summary} | Sent |
   ```
5. Update the Decisions DB entry to confirm sent

### Spending
1. Read the Context field for what to purchase/subscribe to
2. Execute the purchase (may require Chrome MCP for web-based purchases)
3. Log the cost in the venture's `metrics/costs.md`
4. Update the Decisions DB entry with confirmation

### Stage Change
1. Read the Context field for the target stage
2. Update the venture's CLAUDE.md with the new stage
3. Update `portfolio/registry.md`
4. Update the Notion Ventures DB entry
5. If new stage unlocks capabilities, update the venture's agent team if needed
6. Log the transition in the venture's `docs/changelog.md` and `decisions/`

## Step 3: Summary

Report what was processed:
```
Processed {N} approved items:
- {Type}: {Description} for {Venture} — {result}
- ...
```

If no approved items found, report: "No pending approvals to process."
