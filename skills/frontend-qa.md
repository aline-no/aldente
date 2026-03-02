# Frontend QA

## Purpose

Visual and functional verification of frontend builds using CLI tools. Catches what code review misses: broken layouts, blank pages, accessibility failures, performance issues. Runs after each build phase.

## When to Use

- After completing a build phase (as part of code review)
- After wiring new API data or adding new pages
- Before declaring the design system phase complete
- When an agent needs to verify its own UI work

## Prerequisites

Install as dev dependencies in the project:

```bash
npm i -D playwright @axe-core/cli lighthouse
npx playwright install chromium
```

Add to `.env.example`:
```
# QA
VITE_DEV_PORT=5173
```

## Steps

### 1. Screenshot Verification

After each phase that touches UI, capture screenshots of affected pages.

```bash
# Start dev server in background (if not already running)
npm run dev &

# Wait for server to be ready
npx wait-on http://localhost:5173

# Screenshot specific pages
npx playwright screenshot http://localhost:5173/ screenshots/home.png
npx playwright screenshot http://localhost:5173/app screenshots/app.png
```

**What to check after reading the screenshot:**
- Page renders content (not blank, not a spinner stuck forever)
- Layout matches the expected structure from `docs/ui-structure.md`
- No obvious visual breakage (overlapping elements, missing sidebar, broken grid)
- Data displays where expected (tables have rows, charts have axes, cards have content)

**Responsive check (design system phase):**
```bash
# Mobile viewport
npx playwright screenshot --viewport-size=375,812 http://localhost:5173/ screenshots/home-mobile.png

# Tablet viewport
npx playwright screenshot --viewport-size=768,1024 http://localhost:5173/ screenshots/home-tablet.png
```

### 2. Accessibility Audit

Run axe-core against pages touched by this phase.

```bash
npx axe http://localhost:5173/
npx axe http://localhost:5173/app
```

**What to check:**
- No critical or serious violations
- Moderate violations flagged but not blocking (except in design system phase)
- Common catches: missing labels, low contrast, missing alt text, no focus indicators

### 3. Performance Audit (design system phase only)

Run Lighthouse in headless mode.

```bash
npx lighthouse http://localhost:5173/ --output=json --output-path=./lighthouse-home.json --chrome-flags="--headless=new" --only-categories=performance,accessibility,best-practices
```

**Thresholds:**
- Performance: > 70
- Accessibility: > 90
- Best Practices: > 80

Flag scores below thresholds but don't block the phase unless accessibility is below 80.

### 4. Smoke Test (optional, after data wiring)

For critical user flows, write a minimal Playwright test:

```typescript
// tests/smoke.spec.ts
import { test, expect } from '@playwright/test';

test('home page loads', async ({ page }) => {
  await page.goto('http://localhost:5173/');
  await expect(page.locator('h1')).toBeVisible();
});

test('app page loads with data', async ({ page }) => {
  await page.goto('http://localhost:5173/app');
  await expect(page.locator('[data-testid="main-content"]')).toBeVisible();
});
```

Run with:
```bash
npx playwright test tests/smoke.spec.ts
```

Smoke tests are not required for every phase. Add them for pages where data integration is complex or where blank-screen failures have happened before.

## Per-Phase Checklist

| Phase | Screenshots | Accessibility | Performance | Smoke tests |
|-------|------------|---------------|-------------|-------------|
| Setup (1-3) | All pages | Skip | Skip | Skip |
| Data wiring (4-5) | Changed pages | Changed pages | Skip | Critical flows |
| Integrations (6-9) | Changed pages | Changed pages | Skip | Integration points |
| Design system (10) | All pages + responsive | All pages | All pages | All flows |
| Launch audit (11) | All pages + responsive | All pages | All pages | All flows |

## Output Format

```
## Frontend QA: [phase name]

### Screenshots
- [page]: [pass/fail] - [notes]

### Accessibility (axe)
- [page]: [X critical, Y serious, Z moderate]
- Issues: [list if any]

### Performance (design system / launch only)
- [page]: Performance [score], Accessibility [score], Best Practices [score]

### Smoke Tests (if run)
- [X/Y passed]
- Failures: [list if any]

### Verdict: PASS / FAIL
```

## File Structure

```
project/
  tests/
    smoke.spec.ts       # Smoke tests (added as needed)
  screenshots/          # QA screenshots (gitignored)
  playwright.config.ts  # Playwright config (added on first use)
```

Add to `.gitignore`:
```
screenshots/
lighthouse-*.json
```

## Rules

1. Always start the dev server before running QA. Don't run against a build preview unless explicitly testing production builds.
2. Screenshots are disposable. Take them, read them, delete them. Don't commit screenshots to the repo.
3. Don't write E2E tests for every page. Smoke tests cover critical flows only.
4. Accessibility audit is not optional in the design system phase. It's a blocker.
5. Performance scores are guidelines, not hard gates (except accessibility > 80).
6. If mocks are enabled (`VITE_MOCK_API=true`), QA still works. It verifies the UI layer regardless of data source.
7. If Playwright is not installed in the project, install it before running QA. Don't skip QA because a dependency is missing.
