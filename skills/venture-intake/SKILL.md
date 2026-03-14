---
description: Evaluate a new business idea and produce a structured idea brief with go/no-go recommendation
argument-hint: "<idea description>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Agent
  - Bash
  - WebSearch
  - WebFetch
  - mcp__contextportal__contextportal_search
  - mcp__contextportal__contextportal_semantic_search
  - mcp__contextportal__contextportal_deep_search
---

# Venture Intake — Evaluate a New Business Idea

You are evaluating a new business idea for the ChiefOfStaff portfolio.

## Input

The idea description provided as argument: `$ARGUMENTS`

## Step 1: Generate Venture Slug

Create a URL-friendly slug from the idea (e.g., "AI invoice tool for freelancers" → `ai-invoice-tool`).

## Step 2: Check Portfolio

Read `portfolio/registry.md` to ensure:
- No existing venture with the same or very similar slug
- No existing venture in the same market/space (flag overlap if found)

## Step 3: Parallel Research

Spawn two agents in parallel:

### Agent 1: Strategist
Spawn the `strategist` agent with this prompt:
```
Evaluate this business idea: "{idea description}"

Produce a structured idea brief covering:
1. Market Assessment (TAM/SAM/SOM, growth, timing)
2. Competitive Landscape (direct and indirect competitors)
3. Differentiation potential
4. Recommended business model and pricing
5. Risk assessment (top 3 risks)
6. Go/no-go recommendation with confidence level

If "go": recommend venture type (SaaS/Content/Marketplace/API/E-commerce/Service) and initial agent team composition.

Read templates/agents/ to understand available agent templates.
Read portfolio/guardrails.md for ethical boundaries.
Read knowledge/lessons.md for relevant past learnings.
```

### Agent 2: Researcher
Spawn the `researcher` agent with this prompt:
```
Conduct market research for this business idea: "{idea description}"

Produce a research brief covering:
1. Market size (TAM/SAM/SOM with sources)
2. Key market trends
3. Top 5 competitors with positioning, pricing, and weaknesses
4. Target customer segments
5. Pricing benchmarks

Cite all sources with URLs and dates. Use multiple sources for key claims.
```

## Step 4: Synthesize

Combine the strategist's evaluation and researcher's data into a unified idea brief.

Create `portfolio/ideas/{slug}.md` with:

```markdown
# Idea Brief: {Venture Name}

**Slug:** {slug}
**Date:** {today}
**Status:** Under Review

## The Idea
{Original idea description}

## Market Assessment
{From strategist + researcher}

## Competitive Landscape
{From researcher, enriched by strategist}

## Differentiation
{From strategist}

## Business Model
{From strategist}

## Risk Assessment
{From strategist}

## Recommended Team
{From strategist — which agents, why}

## Go/No-Go Recommendation
{Strategist's recommendation with confidence level}

### Key Assumptions to Validate
{What needs to be true for this to work}

## Raw Research
{Researcher's full output with sources}
```

## Step 5: Present to Founder

Display the idea brief to the founder in a clear, scannable format:

```
## Idea Brief: {Venture Name}

**Recommendation:** {GO / NO-GO} (Confidence: {HIGH/MEDIUM/LOW})

**One-liner:** {What it does in one sentence}

**Market:** {TAM} total market, {growth}% growing

**Top competitors:** {competitor 1}, {competitor 2}, {competitor 3}

**Differentiation:** {One sentence}

**Business model:** {Revenue model} at {pricing range}

**Top risks:**
1. {Risk 1}
2. {Risk 2}
3. {Risk 3}

**Recommended team:** {agent 1}, {agent 2}, {agent 3}

**Next step:** If you approve, I'll create a private GitHub repo, scaffold the agent team, and move to VALIDATION stage.
```

Ask the founder: "Should I proceed with bootstrapping this venture?"

## Step 6: On Approval

If the founder approves, proceed to the `venture-staffing` skill to design the team, then `venture-bootstrap` to create the repo.

If the founder says no, update the idea brief status to "Rejected" with the reason.
