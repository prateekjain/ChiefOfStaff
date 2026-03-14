---
description: Submit an action to the Notion Decisions DB for founder approval
argument-hint: "<type> <venture-slug> <description>"
allowed-tools:
  - Read
  - Write
  - mcp__notion__notion-create-pages
  - mcp__notion__notion-fetch
---

# Submit for Approval

Submit an action to the Notion Decisions DB approval queue for founder review.

## Input

- **Type**: One of: Deployment, Content, Outreach, Spending, Stage Change
- **Venture slug**: Which venture this is for
- **Description**: What action is being requested

## Step 1: Prepare the Submission

Read the context needed for the founder to make a decision:
- For **Content**: Include the full draft text in the Context field
- For **Outreach**: Include the target, channel, and full message draft
- For **Deployment**: Include what's being deployed and where
- For **Spending**: Include the amount, what it's for, and ROI justification
- For **Stage Change**: Include evidence that exit criteria are met

## Step 2: Create Decisions DB Entry

Create a page in the Decisions database (data source: `YOUR_DECISIONS_DATASOURCE_ID`):

```
Decision: {Short title of what needs approval}
Type: {Deployment / Content / Outreach / Spending / Stage Change}
Status: Pending
Venture: {venture slug}
Submitted By: {agent name}
Urgency: {Low / Medium / High}
Date: {today}
Context: {Full details — the draft content, the action description, the evidence}
```

## Step 3: Log the Submission

Write a note to the venture's `decisions/` directory:
```
decisions/{date}-{slug}.md:
# Pending Approval: {title}
Submitted to Decisions DB on {date}.
Type: {type}
Waiting for founder review.
```

## Step 4: Confirm

Report: "Submitted for approval: {title}. Check the Decisions DB in Notion to approve or reject."

The item will be executed by ChiefOfStaff during the next work cycle after the founder marks it "Approved".
