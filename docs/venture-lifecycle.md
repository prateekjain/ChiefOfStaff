# Venture Lifecycle

## Stages

```
IDEA → VALIDATION → MVP → LAUNCH → GROWTH → OPTIMIZATION → MATURE
                                                              ↘ KILLED (from any stage)
                                                              ↘ PAUSED (from any stage)
```

## Stage Details

### IDEA

**Where it lives:** ChiefOfStaff only (no venture repo yet)

**What happens:**
- Strategist evaluates business viability
- Researcher conducts initial market scan
- Competitive landscape analysis
- Go/no-go recommendation produced

**Entry criteria:** Founder submits idea via `/new-venture`

**Exit criteria (to advance to VALIDATION):**
- Idea brief completed with market data
- Strategist recommends "go"
- Founder approves

**Key outputs:**
- Idea brief (market size, competition, differentiation, risks)
- Go/no-go recommendation with rationale

---

### VALIDATION

**Where it lives:** Own GitHub repo (created at this stage)

**What happens:**
- Venture repo created with custom agent team
- Deep market research (TAM/SAM/SOM, trends, timing)
- Customer persona development
- Demand validation experiments designed and proposed
- Landing page tests, surveys, or waitlist signup tracking
- Competitive differentiation sharpened

**Entry criteria:** Idea approved, repo bootstrapped

**Exit criteria (to advance to MVP):**
- Evidence of demand (conversion rates, signup numbers, survey results)
- Clear customer persona defined
- Differentiation validated
- Business model hypothesis documented

**Key outputs:**
- `docs/market-research.md` — comprehensive market analysis
- `docs/user-personas.md` — target user profiles
- `docs/business-model.md` — revenue model hypothesis
- Validation experiment results in `data/`

**Agents typically active:** researcher, marketer

---

### MVP

**Where it lives:** Venture repo

**What happens:**
- Technical architecture designed
- Core feature set defined (minimal — one key value proposition)
- Prototype or MVP built
- Basic documentation written

**Entry criteria:** Validation positive, demand evidence documented

**Exit criteria (to advance to LAUNCH):**
- Working prototype with core feature
- User can complete the primary use case
- Basic documentation exists
- Architecture documented

**Key outputs:**
- `docs/architecture.md` — technical design
- `docs/requirements.md` — product requirements
- `src/` — working source code
- `docs/changelog.md` — initial version documented

**Agents typically active:** builder, researcher (for ongoing context)

---

### LAUNCH

**Where it lives:** Venture repo

**What happens:**
- Go-to-market plan executed
- Landing page finalized
- Initial outreach to potential users
- First users onboarded
- Feedback collection started
- CRM pipeline set up (HubSpot)

**Entry criteria:** MVP complete and functional

**Exit criteria (to advance to GROWTH):**
- First paying customers or significant active users
- At least one feedback loop established
- Retention signal observed (users return)
- Revenue or clear path to revenue

**Key outputs:**
- `docs/gtm-strategy.md` — go-to-market plan
- `marketing/` — landing pages, copy, assets
- CRM pipeline in HubSpot
- Initial user feedback documented

**Agents typically active:** marketer, sales-ops, builder (for fixes)

---

### GROWTH

**Where it lives:** Venture repo

**What happens:**
- Growth experiments designed and run
- Funnel optimization (acquisition → activation → retention → revenue → referral)
- Content marketing, SEO, distribution strategy
- Sales pipeline management
- Customer feedback incorporated into product

**Entry criteria:** Revenue or active users, retention signal

**Exit criteria (to advance to OPTIMIZATION):**
- Consistent month-over-month growth
- Clear scaling path identified
- Acquisition channels proven
- Unit economics understood (even if not yet profitable)

**Key outputs:**
- Growth experiment results in `data/`
- Updated `metrics/` with funnel data
- Content in `marketing/`
- Sales pipeline data in CRM

**Agents typically active:** marketer, sales-ops, builder, finance (added at this stage)

---

### OPTIMIZATION

**Where it lives:** Venture repo

**What happens:**
- Unit economics optimized (reduce CAC, improve LTV)
- Cost reduction and automation
- Process efficiency improvements
- Expansion planning (new features, markets, segments)

**Entry criteria:** Growth proven, scaling path clear

**Exit criteria (to advance to MATURE):**
- Profitable or clear path to profitability
- Operations largely automated
- Growth sustainable without constant intervention

**Key outputs:**
- Financial analysis in `metrics/`
- Automation documentation in `docs/`
- Expansion proposals in `plans/`

**Agents typically active:** finance, builder, marketer

---

### MATURE

**Where it lives:** Venture repo

**What happens:**
- Maintenance and monitoring
- Incremental improvements
- Light-touch agent attention
- Revenue continues with minimal intervention

**Agents typically active:** All agents on reduced schedule

---

### KILLED

**Where it lives:** Venture repo (archived)

**What happens:**
- Post-mortem document generated
- Key learnings extracted to `knowledge/lessons.md` (in ChiefOfStaff)
- GitHub repo archived
- Portfolio registry updated

**Triggered by:** `/kill-venture slug` from any stage

---

### PAUSED

**Where it lives:** Venture repo (preserved)

**What happens:**
- Scheduled tasks disabled
- No active agent work
- State fully preserved for potential resumption

**Triggered by:** `/pause-venture slug` from any stage

## Stage Transition Rules

1. **All transitions require founder approval** — except PAUSED and KILLED which require explicit founder command
2. **Exit criteria must be documented** — the chief-of-staff presents evidence before recommending advancement
3. **New agents may be added** at stage transitions (e.g., sales-ops at Launch, finance at Growth)
4. **Skipping stages is not allowed** — every venture goes through each stage in order
5. **Regression is possible** — a venture can move back (e.g., Growth → Validation if market signals change)
