# Health Check

**Schedule:** Every 6 hours
**Duration:** ~5 minutes
**Purpose:** Quick health scan of all active ventures, flag problems

## Instructions

You are running a portfolio health check.

1. Execute the `venture-health-check` skill with no arguments (checks all ventures).

2. This will:
   - Pull latest from each active venture repo
   - Score health across 4 dimensions (velocity, plan clarity, docs, stage fit)
   - Update health scores in `portfolio/registry.md`
   - Flag any venture scoring below 50

3. If any venture is flagged:
   - Note the issue in the daily digest file (`digests/daily/{date}.md`)
   - The evening digest will pick this up and alert the founder

4. This is a quick check — don't do any work on ventures, just assess their health.
