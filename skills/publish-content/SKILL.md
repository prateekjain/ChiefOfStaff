---
description: Publish approved content to social media, blog, or other channels via Chrome MCP
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

# Publish Content

Publish an approved piece of content via the appropriate channel. This skill reads from the Decisions DB and publishes via Chrome MCP.

## Step 1: Read the Approved Item

Fetch the Decisions DB entry to get:
- The content to publish (from Context field)
- The target channel (Twitter/X, LinkedIn, blog, Reddit, forum, etc.)
- The venture slug

## Step 2: Publish via Chrome MCP

### Twitter/X
1. Navigate to `https://twitter.com/compose/tweet` (or `https://x.com/compose/post`)
2. Use form_input to enter the tweet text
3. Use computer to click the Post button
4. Capture the tweet URL from the resulting page

### LinkedIn
1. Navigate to `https://www.linkedin.com/feed/`
2. Use computer to click "Start a post"
3. Use form_input to enter the post content
4. Use computer to click Post
5. Capture the post URL

### Reddit
1. Navigate to the target subreddit
2. Use computer to click "Create Post"
3. Use form_input to enter title and body
4. Use computer to click Post

### Blog (if venture has a blog platform)
1. Navigate to the blog admin
2. Create a new post with the content
3. Publish and capture the URL

### General approach for other platforms
1. Navigate to the platform
2. Find the compose/post area
3. Input the content
4. Submit and capture the result URL

## Step 3: Log the Publication

1. Save to venture's `marketing/published/{date}-{platform}-{slug}.md`:
   ```markdown
   # Published: {title}

   **Platform:** {channel}
   **Date:** {date}
   **URL:** {published-url}

   ## Content
   {the content that was published}
   ```

2. Append to venture's `docs/changelog.md`:
   ```
   ## {date}: [Launch] Published on {platform}
   {title} — {published-url}
   ```

3. Update the Decisions DB entry with the published URL in Context

## Step 4: Report

"Published to {platform}: {url}"
