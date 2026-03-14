---
name: qa-check
description: Run quality assurance checks on a deployed venture site
agent: qa
arguments:
  - name: venture
    description: Venture slug
    required: true
  - name: url
    description: Deployed URL to test
    required: true
---

# QA Check — Run Quality Assurance on a Deployed Venture

Run a comprehensive QA check on a deployed venture site and generate a report.

## Input

- **Venture:** `$ARGUMENTS.venture`
- **URL:** `$ARGUMENTS.url`

## Step 1: Prepare

1. Read the venture's `CLAUDE.md` to understand:
   - What the site does
   - Expected pages and routes
   - API endpoints
   - Known issues or limitations

2. Read `docs/` in the venture repo for feature specs and expected behavior.

3. Create the report directory if it doesn't exist:
   ```bash
   mkdir -p $PROJECTS_DIR/$ARGUMENTS.venture/qa/reports
   ```

## Step 2: Site Availability

1. Start a preview of the deployed URL:
   - Use `mcp__Claude_Preview__preview_start` with the venture URL
   - Take a screenshot of the homepage with `mcp__Claude_Preview__preview_screenshot`

2. Check HTTP status:
   ```bash
   curl -s -o /dev/null -w "%{http_code}" $ARGUMENTS.url
   ```

3. Check for redirects and verify final URL is correct.

## Step 3: Page-by-Page Review

For each major page/route on the site:

1. Navigate to the page using `mcp__Claude_Preview__preview_click` or direct URL
2. Take a screenshot with `mcp__Claude_Preview__preview_screenshot`
3. Get the DOM snapshot with `mcp__Claude_Preview__preview_snapshot`
4. Check console logs with `mcp__Claude_Preview__preview_console_logs` — flag any errors or warnings
5. Check network requests with `mcp__Claude_Preview__preview_network` — flag any failed requests (4xx, 5xx)

## Step 4: Link Validation

1. From the DOM snapshot, extract all links (`<a href="...">`)
2. Categorize them:
   - Internal navigation links
   - External links
   - Anchor links
   - CTA buttons
3. Click each internal link and verify it loads correctly
4. Flag any `href="#"` placeholders
5. For external links, verify they resolve:
   ```bash
   curl -s -o /dev/null -w "%{http_code}" {external_url}
   ```

## Step 5: Form Testing

For each form on the site:

1. Identify all form fields from the DOM snapshot
2. Fill the form with valid test data using `mcp__Claude_Preview__preview_fill`:
   - Use realistic but clearly test data (e.g., "QA Test User", "qa-test@example.com")
3. Submit the form using `mcp__Claude_Preview__preview_click`
4. Check for:
   - Success feedback (toast, redirect, thank you message)
   - Network request to API endpoint (should be 200)
   - No console errors
5. Test with invalid data:
   - Empty required fields
   - Invalid email format
   - Very long strings (500+ characters)
6. Verify validation messages appear

## Step 6: Content Scan

Using the DOM snapshots collected, scan for:

1. **Placeholder text** — Search for:
   - "Lorem ipsum"
   - "TODO", "FIXME", "HACK"
   - "[Name]", "[Company]", "{placeholder}"
   - "example.com" in visible text (not code)
2. **Fabricated content** — Flag anything that looks fake:
   - Testimonials with stock photo avatars
   - Statistics without sources
   - Company logos that don't match real companies
3. **Spelling and grammar** — Note obvious errors

## Step 7: Responsive Testing

1. Test at mobile width (375px):
   ```
   mcp__Claude_Preview__preview_resize with width=375
   ```
   - Take screenshot
   - Check for horizontal overflow
   - Verify navigation works (hamburger menu if applicable)

2. Test at tablet width (768px):
   - Take screenshot
   - Check layout transitions

3. Test at desktop width (1024px):
   - Take screenshot
   - Verify full layout

## Step 8: Performance Check

1. Check page load metrics using `mcp__Claude_Preview__preview_eval`:
   ```javascript
   JSON.stringify(performance.getEntriesByType('navigation')[0])
   ```

2. Check for large resources:
   ```javascript
   performance.getEntriesByType('resource')
     .filter(r => r.transferSize > 500000)
     .map(r => ({ name: r.name, size: r.transferSize }))
   ```

3. Flag any resources over 500KB.

## Step 9: Generate Report

1. Compile all findings into a QA report
2. Write the report to `qa/reports/YYYY-MM-DD.md` in the venture repo using the QA agent's output format
3. Set overall status:
   - **PASS** — No critical issues, 0-2 minor warnings
   - **WARN** — No critical issues but 3+ warnings
   - **FAIL** — Any critical issue (broken pages, form failures, console errors, placeholder text)

4. If FAIL: Log critical issues so the builder agent can address them in the next cycle
5. If PASS: Note in the venture's changelog that QA passed

## Step 10: Cleanup

1. Stop the preview session
2. Commit and push the QA report:
   ```bash
   cd $PROJECTS_DIR/$ARGUMENTS.venture
   git add qa/reports/
   git commit -m "QA report: $(date +%Y-%m-%d) — {PASS/WARN/FAIL}"
   git push
   ```
