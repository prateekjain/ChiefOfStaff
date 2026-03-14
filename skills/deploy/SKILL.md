---
description: Deploy a venture's code to Vercel and/or set up Supabase — run by ChiefOfStaff
argument-hint: "<venture-slug>"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - mcp__notion__notion-update-page
  - mcp__notion__notion-fetch
  - mcp__notion__notion-search
---

# Deploy Venture

Deploy a venture's code to Vercel and/or set up a Supabase project. This skill is executed by ChiefOfStaff — ventures do not self-deploy.

## Input

Venture slug: `$ARGUMENTS`

## Step 1: Read Context

1. Read `portfolio/registry.md` to find the venture and confirm stage allows deployment
2. Read the venture's `CLAUDE.md` for current deployment state (check for existing URLs)
3. Read `portfolio/guardrails.md` to confirm free-tier deployment is allowed at this stage

## Step 2: Pull Latest Code

```bash
cd $PROJECTS_DIR/{slug} && git pull --quiet
```

## Step 3: Pre-Deployment Quality Gate (MANDATORY)

Before deploying, verify the code meets quality standards. **If any check fails, DO NOT deploy — fix the issue first.**

```bash
cd $PROJECTS_DIR/{slug}

# 1. Build must pass
npm run build 2>&1

# 2. Check for placeholder links (href="#")
grep -r 'href="#"' src/ --include="*.tsx" --include="*.ts" --include="*.jsx" --include="*.js" || echo "PASS: No placeholder links"

# 3. Check for console.log in API routes (should use real storage)
grep -r 'console.log' src/app/api/ --include="*.ts" --include="*.js" | grep -v 'console.error' || echo "PASS: No console.log in API routes"

# 4. Check for fake/placeholder content
grep -rEi '(lorem ipsum|\[Name\]|\[Company\]|TODO:|FIXME:)' src/ --include="*.tsx" --include="*.ts" || echo "PASS: No placeholder content"

# 5. Check for proper metadata
grep -r 'metadata' src/app/layout.tsx || echo "WARNING: No metadata found in layout"
```

If any checks fail, fix the issues before proceeding to deployment.

## Step 4: Deploy to Vercel

If the venture has deployable code in `src/` or has a `package.json`:

```bash
cd $PROJECTS_DIR/{slug}
vercel --yes --prod 2>&1
```

Capture the deployment URL from output.

If this is the first deployment, also link the project:
```bash
vercel link --yes 2>&1
```

**Important:** Only use Vercel's free (Hobby) tier. If the deployment would require a paid plan, stop and submit a Spending approval instead.

## Step 5: Set Up Supabase (if needed)

If the venture needs a database/auth (check `docs/architecture.md`):

```bash
# Only if no Supabase project exists yet
supabase init 2>&1  # In the venture directory
supabase start 2>&1  # For local development
```

For remote Supabase (production), the founder needs to have a Supabase account. Check if one exists:
```bash
supabase projects list 2>&1
```

If no account/project exists, submit a Spending approval to the Decisions DB for Supabase setup.

## Step 6: Record Deployment URLs

1. Update the venture's `CLAUDE.md` — add/update the Deployment section:
   ```
   ## Deployment
   - **Live URL**: {vercel-url}
   - **Vercel Project**: {project-name}
   - **Supabase Project**: {project-ref} (if applicable)
   - **Last Deployed**: {date}
   ```

2. Update `portfolio/registry.md` with the live URL

3. Update the Notion Ventures DB entry with the live URL (in the Repo URL or a note)

4. Log in the venture's `docs/changelog.md`:
   ```
   ## {date}: [Deployment] Deployed to Vercel
   Live at: {url}
   ```

## Step 7: Post-Deployment Verification

Check that the deployment is live and functional:
```bash
# Basic health check
curl -s -o /dev/null -w "%{http_code}" {deployment-url}

# Check for server errors in the response
curl -s {deployment-url} | head -50
```

## Step 8: Trigger QA Check

After deployment, run the QA agent to verify everything works end-to-end:
- Use the `qa-check` skill with the venture slug and deployment URL
- QA agent will test all forms, links, responsiveness, and console errors
- If QA finds critical issues, fix and redeploy before reporting success

Report: "Deployed {venture} to {url}. Status: {http_code}. QA: {pass/fail}."
