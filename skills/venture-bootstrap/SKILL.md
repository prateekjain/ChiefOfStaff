---
description: Create a private GitHub repo for a venture, scaffold it with custom agents, skills, docs, and push
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - mcp__claude_ai_Notion__notion-create-pages
  - mcp__claude_ai_Notion__notion-update-page
  - mcp__claude_ai_Notion__notion-search
---

# Venture Bootstrap — Create and Scaffold a Venture Repo

Create a private GitHub repo for a venture and scaffold it with everything it needs to operate.

## Input

Venture slug: `$ARGUMENTS`

## Step 1: Read Context

1. Read `portfolio/ideas/{slug}.md` for the idea brief
2. Read `portfolio/ideas/{slug}-team.md` for the team design
3. Read `portfolio/guardrails.md` for operating rules
4. Determine the GitHub username: `gh api user --jq .login`

## Step 2: Create GitHub Repo

```bash
gh repo create {slug} --private --description "{one-liner from idea brief}"
```

Clone it locally:
```bash
cd $PROJECTS_DIR
gh repo clone {slug}
cd {slug}
```

## Step 3: Create Directory Structure

```bash
mkdir -p agents skills commands src docs marketing data plans/archive decisions metrics learnings scheduled qa/reports
```

## Step 4: Scaffold CLAUDE.md

Read `templates/venture-claude.md` and customize with venture-specific content:
- Replace all `{{PLACEHOLDERS}}` with actual values from the idea brief
- Set venture name, slug, type, stage (VALIDATION), one-liner, vision, target users
- Fill in the agent team table
- Set current focus based on stage (VALIDATION → "Validate demand and refine positioning")
- Set initial success metrics

Write to `{slug}/CLAUDE.md`.

## Step 5: Scaffold README.md

Read `templates/venture-readme.md` and customize:
- Replace all `{{PLACEHOLDERS}}` with actual values
- Include current status, team, metrics
- Link to all docs

Write to `{slug}/README.md`.

## Step 6: Scaffold Documentation

For each doc template in `templates/docs/`:
- Read the template
- Customize with venture-specific content where possible (from the idea brief and team design)
- Leave `{{PLACEHOLDERS}}` for sections that need more research

Create these files:
- `docs/architecture.md` — Populate what we know (type-appropriate stack recommendations)
- `docs/requirements.md` — Populate from idea brief (problem, target users, initial user stories)
- `docs/market-research.md` — Populate from researcher's data in the idea brief
- `docs/business-model.md` — Populate from strategist's model recommendation
- `docs/changelog.md` — Initial entry: "Venture bootstrapped"

Also create:
- `docs/user-personas.md` — From idea brief's customer segments
- `docs/gtm-strategy.md` — Initial placeholder with venture type-appropriate structure

## Step 7: Scaffold Agents

For each agent in the team design:
1. Read the appropriate template from `templates/agents/{agent}.md`
2. Apply the customizations specified in the team design
3. Add venture-specific context, principles, and instructions
4. Write to `{slug}/agents/{agent}.md`

## Step 7b: Apply Ecosystem Enhancements

If the team design (`portfolio/ideas/{slug}-team.md`) includes an "Ecosystem Tools" table:

1. For each tool classified as **Agent Enhancement**:
   - Add integration notes as comments in the relevant agent's file
   - If the tool is an MCP server, add it to the agent's `tools:` list
   - Reference the tool in the agent's instructions where applicable

2. For each tool classified as **Skill Component**:
   - Note the tool in the relevant skill's instructions
   - Add integration guidance to `docs/architecture.md`

3. For each tool classified as **Future-Stage Addition**:
   - Document in `plans/current.md` under a "Future Enhancements" section
   - Note which stage to revisit

4. Reference all ecosystem tools in `docs/architecture.md` under a "Ecosystem Integrations" section.

## Step 8: Create Initial Skills

Based on the team design's skill list, create venture-specific skills:

At minimum, create:
- `skills/status-report/SKILL.md` — Generate a status report for ChiefOfStaff health checks

## Step 9: Brand Setup (if stage >= VALIDATION)

Run the brand-setup skill to research domains, validate the venture name, and generate a brand kit:

```
/brand-setup {slug}
```

This will:
1. Validate the venture name (trademark conflicts, SEO, pronunciation)
2. Research domain availability (.com, .ai, .io, .co + variations)
3. Check social handle availability (Twitter/X, LinkedIn, GitHub)
4. Generate a complete brand kit at `docs/brand-kit.md` (identity, voice & tone, visual identity, domain recommendations)

Skip this step if the venture is at IDEA stage (brand research happens during VALIDATION).

## Step 10: Create Continuity File

Read `templates/continuity.md` and customize:
- Replace `{{VENTURE_NAME}}` with the venture name
- Set Last Updated to today's date, by "chief-of-staff"
- Set "What Was Done" to "Venture bootstrapped with agent team and docs"
- Set "What's Next" to the first task from the plan (typically: deep market research)

Write to `{slug}/continuity.md`.

## Step 11: Create Initial Plan

Write `plans/current.md`:

```markdown
# Current Plan — {Venture Name}

**Stage:** VALIDATION
**Sprint:** Initial Setup
**Updated:** {today}

## Objectives
1. Validate demand for {venture concept}
2. Identify and deeply understand target customer segment
3. Sharpen competitive positioning
4. Design first validation experiment

## Tasks
- [ ] Deep market research (researcher)
- [ ] Customer persona development (researcher)
- [ ] Competitive positioning document (researcher + marketer)
- [ ] Validation experiment design (marketer)
- [ ] Landing page or signup test plan (marketer)

## Success Criteria
- Market research completed with TAM/SAM/SOM
- At least 2 customer personas defined
- Clear differentiation from top 3 competitors
- One validation experiment designed and ready to execute
```

## Step 12: Create .gitignore

```
.DS_Store
node_modules/
.env
.env.*
*.log
dist/
build/
.claude/
```

## Step 13: Deploy (if stage allows)

If the venture is at VALIDATION or later stage and has deployable code (e.g., a landing page):

1. Check `portfolio/guardrails.md` Stage → Capabilities Matrix to confirm deployment is allowed
2. Run the `deploy` skill to deploy to Vercel free tier
3. Record the deployment URL in the venture's CLAUDE.md Deployment section
4. Update the Notion Ventures DB entry with the live URL

If the venture needs a database, set up Supabase via the `deploy` skill.

Skip this step if:
- The venture is at IDEA stage (no deployment)
- There's no deployable code yet (just docs/plans)

## Step 14: Initial Commit and Push

```bash
cd $PROJECTS_DIR/{slug}
git add -A
git commit -m "Bootstrap venture: {venture name}

Scaffolded by ChiefOfStaff with custom agent team.
Stage: VALIDATION
Type: {venture type}
Team: {agent list}"
git push -u origin main
```

## Step 15: Update Portfolio Registry

Append the new venture to `portfolio/registry.md`:

```
| {slug} | {Venture Name} | github.com/{user}/{slug} | VALIDATION | -- | $0 | {today} | Begin validation |
```

## Step 16: Update Notion

Search for the "Ventures" database in Notion and create a new entry:
- Name: {Venture Name}
- Stage: VALIDATION
- Health: --
- MRR: $0
- Repo URL: https://github.com/{user}/{slug}
- Last Activity: {today}
- Next Action: Begin validation research

## Step 17: Summary

Report to the founder:

```
Venture "{Venture Name}" bootstrapped successfully.

- GitHub repo: https://github.com/{user}/{slug} (private)
- Stage: VALIDATION
- Agent team: {list of agents}
- Docs: architecture, requirements, market-research, business-model, changelog
- Next: Run /run-cycle or wait for morning cycle to begin validation work

The agents are ready. Run `/venture-status {slug}` to check progress at any time.
```
