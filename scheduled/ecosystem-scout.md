# Ecosystem Scout

**Schedule:** Wednesday at 12:00 PM
**Duration:** ~10-15 minutes
**Purpose:** Weekly broad sweep of the AI ecosystem to discover and catalog new tools

## Instructions

You are running the weekly ecosystem scout sweep.

1. Execute the `ecosystem-scout` skill with no arguments (broad sweep).

2. This will:
   - Search across GitHub trending, HN, Product Hunt, awesome-lists, and AI communities
   - Evaluate and score all discoveries
   - Re-verify entries older than 30 days
   - Rebuild the ecosystem catalog index
   - Generate recommendations for active ventures
   - Write updated `_recommendations.md`

3. After the scout completes:
   - If any discoveries score >= 80: flag them as high-priority in today's digest notes
   - If any existing entries were deprecated: note which ventures may be affected
   - Log a brief summary to `digests/daily/{date}.md` (append if exists, create if not)

4. High-relevance findings will be surfaced in the evening digest automatically (the reporter reads `_recommendations.md`).
