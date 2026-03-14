---
description: Move a venture to the next lifecycle stage
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Agent
  - mcp__notion__notion-update-page
  - mcp__notion__notion-search
---

# /advance-venture — Move to Next Stage

## Input
Venture slug: `$ARGUMENTS`

If no argument, ask: "Which venture should I advance? Provide the slug."

## Step 1: Read Current State

1. Read `portfolio/registry.md` to find the venture's current stage
2. Pull latest from the venture repo
3. Read venture state: `CLAUDE.md`, `plans/current.md`, `metrics/`, `docs/changelog.md`

## Step 2: Determine Next Stage

```
IDEA → VALIDATION → MVP → LAUNCH → GROWTH → OPTIMIZATION → MATURE
```

## Step 3: Validate Exit Criteria

Read `docs/venture-lifecycle.md` for the exit criteria of the current stage.

Assess whether each criterion is met based on the venture's state files. Present evidence:

```
## Stage Transition: {current} → {next}

### Exit Criteria Assessment

| Criterion | Met? | Evidence |
|-----------|------|----------|
| {criterion 1} | Yes/No | {evidence from venture state} |
| {criterion 2} | Yes/No | {evidence} |

### Recommendation
{Recommend advancing or explain what's still needed}
```

## Step 4: Founder Approval

Present the assessment and ask: "Should I advance {venture} from {current} to {next}?"

## Step 5: On Approval

1. Update `CLAUDE.md` in the venture repo:
   - Change stage
   - Update current focus for the new stage
   - Update success metrics for the new stage

2. Add new agents if stage requires it:
   - LAUNCH: Consider adding marketer, sales-ops
   - GROWTH: Consider adding finance
   - Read team design from `portfolio/ideas/{slug}-team.md` for planned additions

3. Update `docs/changelog.md`:
   ```
   ## {date}: [Milestone] Advanced to {next stage}

   Venture moved from {current} to {next}. Exit criteria met: {summary}.
   ```

4. Log the decision in venture's `decisions/`:
   ```
   ## {date}: Stage Transition — {current} → {next}

   **Context**: {summary of state}
   **Decision**: Advance to {next}
   **Rationale**: {exit criteria evidence}
   **Decided by**: Founder (approved)
   ```

5. Update `plans/current.md` with new stage objectives

6. Commit and push venture repo

7. Update `portfolio/registry.md` with new stage

8. Update Notion ventures database

## Step 6: Report

```
{Venture Name} advanced from {current} to {next}.

{If agents added}: New agents added: {list}
Next focus: {new stage objectives}
```
