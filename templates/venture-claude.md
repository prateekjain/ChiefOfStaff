# CLAUDE.md — {{VENTURE_NAME}}

## Venture Context

- **Name**: {{VENTURE_NAME}}
- **Slug**: {{VENTURE_SLUG}}
- **Type**: {{VENTURE_TYPE}} (e.g., SaaS, Content, Marketplace, API/Dev Tool)
- **Stage**: {{CURRENT_STAGE}}
- **Started**: {{START_DATE}}
- **One-Liner**: {{ONE_LINER}}

## Vision

{{VENTURE_VISION — What this venture does and why it matters}}

## Target Users

{{TARGET_USERS — Who are we building for, what problem do we solve for them}}

## Agent Team

| Agent | Role | Status |
|-------|------|--------|
{{AGENT_TABLE — populated by chief-of-staff during bootstrap}}

## Key File Relationships

```
agents/*.md        → do the work, read docs/ for context
docs/              → architecture, requirements, market research, business model
plans/current.md   → what we're working on right now
decisions/         → decision log with rationale
metrics/           → KPIs, revenue, tracking
learnings/         → what we've learned, pivots
src/               → product source code
marketing/         → marketing assets and copy
```

## Working Rules

1. **Read before writing** — Always read relevant docs before making changes.
2. **Update docs with changes** — When you change architecture, update `docs/architecture.md`. When you change strategy, update `docs/gtm-strategy.md`. Etc.
3. **Log decisions** — Every significant choice goes in `decisions/` with context, options considered, decision, and rationale.
4. **Track learnings** — What worked/didn't goes in `learnings/`.
5. **Update changelog** — Milestones, pivots, and significant changes go in `docs/changelog.md`.
6. **Commit and push** — Auto-commit all work with descriptive messages. Push after every commit.
7. **Follow guardrails** — Read the ChiefOfStaff guardrails. No spending, no external comms, no publishing without founder approval.
8. **Brainstorm before building** — For new features or pivots, refine requirements through structured exploration before writing code:
   - What problem are we solving? For whom?
   - What's the simplest solution that validates the hypothesis?
   - What are the risks and unknowns?
   - Document conclusions in `docs/requirements.md` before starting implementation.

## Deployment

- **Live URL**: {{LIVE_URL}} (set by ChiefOfStaff after deployment)
- **Vercel Project**: {{VERCEL_PROJECT}} (if deployed)
- **Supabase Project**: {{SUPABASE_PROJECT}} (if applicable)
- **Last Deployed**: {{LAST_DEPLOYED}}

## Current Focus

{{CURRENT_FOCUS — What the team should be working on right now. Updated each cycle.}}

## Continuity

Agents must update `continuity.md` at the end of every work session with:
- **What was done** — completed work this session
- **What's next** — the immediate next step for the next session
- **Blockers** — anything preventing progress
- **Open questions** — decisions needed from the founder

This ensures any agent (or future session) can pick up exactly where the last one left off.

## Success Metrics

| Metric | Current | Target | Notes |
|--------|---------|--------|-------|
{{METRICS_TABLE — populated and updated as venture progresses}}
