---
description: Design a custom agent team for a venture based on its type and stage
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Agent
---

# Venture Staffing — Design a Custom Agent Team

Design the right agent team for a venture based on its type, stage, and specific needs.

## Input

Venture slug: `$ARGUMENTS`

## Step 1: Read Context

1. Read `portfolio/ideas/{slug}.md` for the idea brief and strategist's team recommendation
2. Read all templates in `templates/agents/` to understand available agent types
3. Read `knowledge/ecosystem/_index.md` for the ecosystem tool catalog
4. Read `knowledge/ecosystem/_recommendations.md` for venture-specific recommendations
5. Read `portfolio/guardrails.md` for operating rules
6. Read `knowledge/lessons.md` for relevant team design lessons

## Step 2: Determine Venture Type

Based on the idea brief, classify the venture:

| Type | Indicators |
|------|-----------|
| **SaaS** | Software product, subscription/recurring revenue, specific user workflows |
| **Content/Media** | Blog, newsletter, course, media property, ad or subscription revenue |
| **Marketplace** | Connects buyers and sellers, takes commission/fee, two-sided |
| **API/Dev Tool** | Developer-facing, usage-based pricing, technical integration |
| **E-commerce** | Physical or digital product sales, inventory, fulfillment |
| **Service** | Consulting, agency, freelance, time-based billing |

## Step 2.5: Consult Ecosystem Catalog

Filter the ecosystem catalog (`_index.md`) for entries matching the venture type and stage:

1. **Filter by relevance** — Only consider entries with Score >= 60
2. **Classify each match:**
   - **Agent Enhancement** — Can improve an existing venture agent's capabilities (e.g., a web scraping tool for a researcher agent)
   - **Skill Component** — Can be incorporated into a venture skill or workflow (e.g., an SEO analysis tool for a content pipeline)
   - **Future-Stage Addition** — Not needed at current stage, but valuable later (note which stage)
   - **Reference Only** — Worth knowing about, no immediate integration needed
3. **Check `_recommendations.md`** for any scout-generated recommendations specific to this venture

Carry these classifications forward into Step 6 output.

## Step 3: Select and Customize Agents

### Base Team (all ventures get these):
- **researcher** — Always needed for ongoing market awareness
- **qa** — Always needed to catch quality issues before and after deployment

### Type-Specific Additions:

**SaaS:**
- `builder` — Core engineering (customize for the tech domain)
- `marketer` — Growth and distribution (customize for B2B vs B2C)
- `sales-ops` — Pipeline management (if B2B; delay to Launch stage if B2C)

**Content/Media:**
- `writer` — Content creation (customize for content type: blog, newsletter, course)
- `marketer` — SEO, distribution, audience growth (customize for content channels)

**Marketplace:**
- `builder` — Platform engineering
- `marketer` — Supply and demand acquisition
- Create custom `supply-agent` and `demand-agent` if sides have very different needs

**API/Dev Tool:**
- `builder` — API engineering, SDK development
- `writer` — Documentation, tutorials, developer guides
- Create custom `devrel` agent for developer community engagement

**E-commerce:**
- `builder` — Storefront, checkout, integrations
- `marketer` — Product marketing, ads, email
- Create custom `operations` agent for inventory/fulfillment

**Service:**
- `marketer` — Lead generation, positioning
- `sales-ops` — Client pipeline, proposals
- `writer` — Case studies, thought leadership

### Stage-Appropriate Agents:
- **VALIDATION stage:** Start lean — researcher + 1-2 others
- **MVP stage:** Add builder (if not already)
- **LAUNCH stage:** Add marketer and/or sales-ops
- **GROWTH stage:** Add finance agent
- Note which agents will be added at future stages

## Step 4: Customize Each Agent

For each selected agent, customize the template:

1. **Read the template** from `templates/agents/{agent}.md`
2. **Modify the role definition** to be venture-specific:
   - Add venture context (what it does, who it's for)
   - Add domain-specific expertise (e.g., "understand accounting workflows" for an invoicing tool)
   - Adjust principles for the venture's approach
3. **Adjust tool access** if needed:
   - Add HubSpot tools for sales-ops
   - Add specific MCP tools relevant to the venture
4. **Add venture-specific instructions** under "When Working on This Venture"

## Step 5: Design Venture Skills

Based on the venture type and stage, design initial skills:

Common skills to include:
- `research-update` — Periodic market research refresh
- `status-report` — Generate venture status for ChiefOfStaff health checks

Type-specific skills:
- SaaS: `build-feature`, `track-metrics`
- Content: `publish-content`, `seo-audit`
- Marketplace: `supply-outreach`, `demand-outreach`

## Step 6: Output Team Design

Write the team design to `portfolio/ideas/{slug}-team.md`:

```markdown
# Team Design: {Venture Name}

**Venture Type:** {type}
**Current Stage:** VALIDATION

## Agent Team

### Starting Team (VALIDATION)
| Agent | Template | Key Customizations |
|-------|----------|-------------------|
| {agent} | {template} | {what was customized} |

### Future Additions
| Agent | Added At | Reason |
|-------|----------|--------|
| {agent} | {stage} | {why} |

## Custom Agents (not from templates)
{Description of any custom agents created}

## Skills
| Skill | Purpose |
|-------|---------|
| {skill} | {what it does} |

## Ecosystem Tools
| Tool | Category | Score | Classification | Integration Notes |
|------|----------|-------|----------------|-------------------|
| {tool} | {category} | {score} | {agent-enhancement/skill-component/future-stage/reference} | {how to integrate} |

## Venture-Specific Tool Access
{Any special MCP tools or integrations needed}

## Tool Access Plan
ChiefOfStaff grants tools based on stage. Here's what this venture gets:

| Stage | Tools Granted | Notes |
|-------|--------------|-------|
| VALIDATION | Research, Build, Deploy (landing page) | {customization notes} |
| MVP | + Full build, Database setup | {customization notes} |
| LAUNCH | + Outreach, Social publishing, Email | {customization notes} |
| GROWTH | + CRM (HubSpot), Analytics | {customization notes} |

See `portfolio/guardrails.md` Stage → Capabilities Matrix for the full reference.
```

## Step 7: Confirm with Founder

Present the team design and ask: "This is the proposed team for {venture}. Should I proceed with bootstrapping the repo?"

On approval, hand off to the `venture-bootstrap` skill.
