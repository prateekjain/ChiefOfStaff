---
description: Send approved outreach messages via Chrome MCP — email, social DM, or forum post
argument-hint: "<decisions-db-page-url>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - mcp__notion__notion-fetch
  - mcp__notion__notion-update-page
  - mcp__Claude_in_Chrome__navigate
  - mcp__Claude_in_Chrome__read_page
  - mcp__Claude_in_Chrome__get_page_text
  - mcp__Claude_in_Chrome__form_input
  - mcp__Claude_in_Chrome__computer
  - mcp__Claude_in_Chrome__find
  - mcp__Claude_in_Chrome__javascript_tool
---

# Send Outreach

Send an approved outreach message via the appropriate channel. This skill reads from the Decisions DB and sends via Chrome MCP.

## Step 1: Read the Approved Item

Fetch the Decisions DB entry to get:
- The target recipient/community
- The channel (email, Twitter DM, LinkedIn message, forum post)
- The message content
- The venture slug

## Step 2: Send via Chrome MCP

### Email (Gmail)
1. Navigate to `https://mail.google.com/mail/u/0/#inbox`
2. Use computer to click "Compose"
3. Use form_input to fill To, Subject, and Body
4. Use computer to click Send

### Twitter/X DM
1. Navigate to `https://twitter.com/messages`
2. Use computer to start a new message
3. Search for the recipient
4. Use form_input to enter the message
5. Send

### LinkedIn Message
1. Navigate to `https://www.linkedin.com/messaging/`
2. Use computer to start a new message
3. Search for the recipient
4. Use form_input to enter the message
5. Send

### Forum/Community Post
1. Navigate to the target forum/community
2. Create a new post or reply
3. Use form_input to enter the content
4. Submit

## Step 3: Log the Outreach

1. Append to venture's `data/outreach-log.md`:
   ```
   | {date} | {channel} | {target} | {subject/summary} | Sent |
   ```
   Create the file with headers if it doesn't exist:
   ```
   # Outreach Log

   | Date | Channel | Target | Subject | Status |
   |------|---------|--------|---------|--------|
   ```

2. Update the Decisions DB entry to confirm sent

## Step 4: Report

"Sent {channel} outreach to {target}: {subject}"

## Important Notes

- **Never send unsolicited bulk messages** — per guardrails, all outreach must be genuinely relevant
- **Respect opt-outs** — if a recipient has previously declined, do not re-contact
- **Be transparent** — disclose AI involvement where appropriate
- **One at a time** — send outreach individually, not in bulk batches
