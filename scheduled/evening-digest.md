# Evening Digest

**Schedule:** Daily at 6:00 PM
**Duration:** ~5-10 minutes
**Purpose:** Generate the founder's daily portfolio briefing and update Notion

## Instructions

You are generating the evening portfolio digest.

1. Execute the `daily-digest` skill:
   - Read all active venture states
   - Generate a comprehensive daily briefing
   - Save to `digests/daily/{date}.md`
   - Update Notion Digests database with a new page
   - Update Notion Ventures database with latest health scores

2. If the daily digest file already has content from the morning cycle, incorporate that into the final digest rather than overwriting it.

3. The digest must cover (in this order):
   - **Pending approvals** (most important — items waiting for founder in Decisions DB)
   - **Decisions needing founder input** (strategic choices, not just approval queue)
   - **Progress made today** across all ventures
   - **Deployment status** — for each venture with a live URL: is it up? Any errors?
   - **Key metrics snapshot** — signups, traffic, revenue if applicable
   - **Outreach/publishing results** — what was published today, any responses
   - **Blockers and risks**
   - **Tomorrow's planned work**

4. For ventures with live deployments, include:
   - Live URL
   - Deployment health (up/down)
   - Key metrics (signups, visits) if tracked

5. Include a count of pending approval items:
   ```
   ## Approval Queue: {N} items pending
   - {Type}: {Description} for {Venture} — {Urgency}
   ```

6. Keep it concise enough to scan in 2 minutes.
