# Morning Work Cycle

**Schedule:** Daily at 8:00 AM
**Duration:** ~15-30 minutes
**Purpose:** Process approvals, deploy updates, and advance all active ventures

## Instructions

You are the ChiefOfStaff morning work cycle. Your job is to process pending approvals, manage deployments, and advance all active ventures.

### Phase 1: Process Approval Queue

1. Read `portfolio/guardrails.md` to refresh on operating rules and the approval queue workflow.

2. Execute the `process-approvals` skill:
   - Check the Notion Decisions DB for items with Status = "Approved"
   - Execute approved actions: deploy code, publish content, send outreach
   - Log all executed actions in the relevant venture repos
   - Skip items that are "Pending" (waiting for founder) or "Rejected"

### Phase 2: Advance Active Ventures

3. Read `portfolio/registry.md` to get all active ventures (stages: VALIDATION, MVP, LAUNCH, GROWTH, OPTIMIZATION — skip KILLED, PAUSED, MATURE, IDEA).

4. Read `knowledge/lessons.md` for cross-venture learnings to apply.

5. For each active venture (sorted by priority: approved-items > blocked > LAUNCH/GROWTH > VALIDATION > other):

   a. Pull latest:
   ```bash
   cd $PROJECTS_DIR/{slug} && git pull --quiet
   ```

   b. Read venture state:
   - `CLAUDE.md` — context, stage, current focus, deployment URLs
   - `plans/current.md` — active plan and tasks
   - `docs/changelog.md` — recent progress

   c. **Determine tool grants** for this cycle based on the Stage → Capabilities Matrix in guardrails:
   - VALIDATION: research + build + deploy (landing page)
   - MVP: + full build + database
   - LAUNCH: + outreach + social publishing + email
   - GROWTH: + CRM + analytics

   d. Determine what work to delegate based on stage:
   - **VALIDATION**: Market research, customer personas, validation experiments, landing page
   - **MVP**: Architecture, coding, core feature development
   - **LAUNCH**: GTM execution, content publishing, outreach prep
   - **GROWTH**: Growth experiments, funnel optimization, content
   - **OPTIMIZATION**: Unit economics, cost reduction, automation

   e. Spawn `claude --task` against the venture repo:
   ```bash
   claude --task "You are working on {venture-name}. Read CLAUDE.md for context.

   Current stage: {stage}
   Current plan: Read plans/current.md

   Work on the highest-priority uncompleted task in the plan. If all tasks are done,
   assess what the next priorities should be and update the plan.

   Rules:
   - Read docs/ before making changes
   - Update relevant docs when you make changes
   - Commit frequently with descriptive messages
   - Push after committing
   - Log significant decisions in decisions/
   - Update docs/changelog.md for milestones
   - To publish content or send outreach: write drafts to marketing/drafts/ and
     submit for approval using the submit-for-approval skill
   - Do NOT spend money or contact anyone external directly
   - Do NOT run vercel or supabase commands — ChiefOfStaff handles deployment" \
   --cwd $PROJECTS_DIR/{slug}
   ```

   f. After each venture's work completes, note what was done.

### Phase 3: Post-Work Deployment Check

6. For each venture that had code changes this cycle:
   - If the venture has a live Vercel URL (check CLAUDE.md Deployment section):
     - Run `vercel --cwd /path/to/venture --yes --prod` to redeploy
     - Verify the deployment is live: `curl -s -o /dev/null -w "%{http_code}" {url}`
   - If the venture needs a first deployment (has deployable code but no URL yet):
     - Run the `deploy` skill for that venture

### Phase 4: QA Checks

7. For each venture that was deployed (new or redeployed) in Phase 3:
   - Run the `qa-check` skill with the venture slug and deployed URL:
     ```bash
     claude --task "Run the qa-check skill for venture={slug} url={deployed_url}" \
       --cwd $CHIEFOFSTAFF_DIR
     ```
   - If QA status is FAIL:
     - Log critical issues to the venture's `qa/known-issues.md`
     - Flag in the daily digest as needing urgent fixes
     - These issues become top priority in the next morning cycle
   - If QA status is WARN:
     - Note warnings in the daily digest
     - Schedule fixes as non-urgent tasks in the venture's plan
   - If QA status is PASS:
     - Note in the daily digest that deployment passed QA

8. Update `portfolio/registry.md` with last check dates.

9. Log a summary of the cycle to today's digest file (create or append to `digests/daily/{date}.md`):
   - What approvals were processed
   - What work was done per venture
   - What deployments happened
   - QA results per venture (PASS/WARN/FAIL with issue counts)
   - Any pending approval items still waiting
