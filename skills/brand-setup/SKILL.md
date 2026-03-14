---
description: Research domains, validate business names, and generate a brand kit for a venture
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - WebSearch
  - WebFetch
---

# Brand Setup

Research and establish brand identity for a venture. This skill is run during VALIDATION stage (or when transitioning to MVP).

## Input
Venture slug: `$ARGUMENTS`

## Step 1: Read Context
1. Read the venture's `CLAUDE.md` for name, one-liner, target audience
2. Read `docs/market-research.md` for competitive landscape
3. Read `docs/gtm-strategy.md` if it exists for positioning

## Step 2: Name Validation
Research whether the venture name works:
1. **Trademark search**: WebSearch for "[name] trademark" and "[name] software" to check for conflicts
2. **Competitor conflict**: Check if any direct competitor uses a similar name
3. **Pronunciation/spelling**: Is it easy to say, spell, and remember?
4. **SEO potential**: WebSearch the name — how crowded are the results?
5. If the current name has issues, propose 3-5 alternatives with pros/cons

## Step 3: Domain Research
Check domain availability and alternatives:
1. **Primary domain**: Check `[name].com`, `[name].ai`, `[name].io`, `[name].co` using WebFetch to check DNS/WHOIS
2. **Alternative domains**: Try variations — `get[name].com`, `use[name].com`, `try[name].com`, `[name]app.com`, `[name]hq.com`
3. **Social handle availability**: WebSearch for the name on Twitter/X, LinkedIn, GitHub
4. **Recommendations**: Rank top 3 domain options by preference with estimated cost

Use this approach to check domains:
```
WebFetch: https://rdap.verisign.com/com/v1/domain/[name].com
```
If it returns domain data = taken. If 404 = likely available.

For .ai/.io domains:
```
WebSearch: "[name].ai domain" OR check via WebFetch to a WHOIS API
```

## Step 4: Brand Kit Generation
Create `docs/brand-kit.md` in the venture repo with:

### Identity
- **Name**: [Final name]
- **Tagline**: [Short tagline, 5-8 words]
- **One-liner**: [Elevator pitch, 1 sentence]
- **Boilerplate**: [2-3 sentence company description for bios, footers, etc.]

### Voice & Tone
- **We sound like**: [3 adjectives — e.g., confident, knowledgeable, approachable]
- **We don't sound like**: [3 things to avoid — e.g., corporate, salesy, condescending]
- **Audience language**: [Key terms the target audience uses naturally]
- **Example sentences**: [3 examples of on-brand copy vs off-brand copy]

### Visual Identity
- **Primary color**: [Hex code + name — based on industry/audience psychology]
- **Secondary color**: [Hex code]
- **Accent color**: [Hex code — for CTAs, highlights]
- **Background**: [Light/dark preference with hex]
- **Typography**: [Font recommendations — heading + body]
- **Icon style**: [Lucide/outline, filled, etc.]

### Domain & Handles
- **Recommended domain**: [Top pick with reasoning]
- **Alternative domains**: [2-3 backup options]
- **Social handles**: [Availability status for Twitter, LinkedIn, GitHub]
- **Email**: hello@[domain]

### Stage-Based Rollout
| Stage | Brand Assets |
|-------|-------------|
| VALIDATION | Brand name, colors, landing page tone, shared social posts |
| MVP | Own domain, own email, brand guidelines doc, Twitter/X account |
| LAUNCH | Full social presence, content templates, email templates |
| GROWTH | PR kit, partnership materials, branded assets |

## Step 5: Update Venture Docs
1. Add brand kit reference to venture's `CLAUDE.md`
2. Update the venture's landing page CSS variables if colors differ from current
