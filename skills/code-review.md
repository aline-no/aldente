# Code Review

## Purpose

Post-phase quality gate. Run this after completing a build phase to catch issues before moving on. Designed for AI agents reviewing their own work or reviewing another agent's output.

## When to Use

- After completing any build phase
- Before marking a phase as done
- When reviewing another agent's output before committing
- Before any deployment or handoff

## Checklist

Run through each category. Flag issues, don't fix them silently. Report what passes and what doesn't.

### 1. Scope Check
- [ ] Only files relevant to this phase were modified
- [ ] No features were added beyond what the docs specify
- [ ] No refactoring of code outside the current scope
- [ ] No new dependencies added without justification

### 2. Type Safety
- [ ] No `any` types (explicit or implicit)
- [ ] Props are typed, not inferred from usage
- [ ] API response types match `docs/data-models.md`
- [ ] Shared types live in the types directory, not duplicated

### 3. Component Quality
- [ ] Components do one thing
- [ ] No hardcoded strings that should be constants or props
- [ ] Loading and error states handled (not just the happy path)
- [ ] Empty states have context-specific messaging

### 4. Data Flow
- [ ] API calls use the typed client, not raw fetch/axios
- [ ] Query keys follow the project's convention
- [ ] No client-side data that should come from the API
- [ ] Filter/pagination state lives in URL params where appropriate

### 5. Accessibility Basics
- [ ] Interactive elements are keyboard-accessible
- [ ] Images have alt text
- [ ] Form inputs have labels
- [ ] Color is not the only way information is conveyed

### 6. Security
- [ ] No secrets in code (API keys, tokens, passwords)
- [ ] No `innerHTML` or `dangerouslySetInnerHTML` without sanitization
- [ ] Auth tokens handled via interceptor, not manually per request
- [ ] No user input rendered without escaping

### 7. Code Hygiene
- [ ] No commented-out code
- [ ] No console.log left in (except intentional debug logging)
- [ ] No unused imports or variables
- [ ] File and folder naming follows project conventions

### 8. Build Health
- [ ] Project compiles without errors
- [ ] No TypeScript errors
- [ ] No new warnings introduced
- [ ] Dev server starts

### 9. Runtime Verification
- [ ] Pages touched by this phase render without blank screens
- [ ] No console errors on page load
- [ ] No failed network requests (unless backend is intentionally unavailable)
- [ ] If API wiring was added: data loads or mock handlers respond correctly
- [ ] No unhandled promise rejections in terminal output
- [ ] Interactive elements added in this phase respond to clicks/input

### 10. Frontend QA (see `skills/frontend-qa.md`)
- [ ] Screenshots taken of pages touched by this phase and visually verified
- [ ] Accessibility audit (axe-core) run on changed pages -- no critical/serious violations
- [ ] Design system phase: responsive screenshots (mobile + tablet) verified
- [ ] Design system phase: Lighthouse audit passes thresholds (perf > 70, a11y > 90, bp > 80)

## Output Format

```
## Phase Review: [phase name]

### Passed
- [list what passed]

### Issues Found
- [issue]: [file:line] - [what's wrong and why]

### Deferred (out of scope)
- [things noticed but not in scope to fix]

### Verdict: PASS / FAIL
```

## Rules

1. Run the full checklist. Don't skip categories even if they seem irrelevant.
2. Report issues with file paths and line numbers.
3. Don't fix issues silently. Report them so the decision to fix is explicit.
4. A phase with security issues always fails.
5. A phase with type errors always fails.
6. Accessibility and code hygiene issues are warnings, not blockers (except in the design system phase, where they become blockers).
7. Runtime errors (console errors, failed requests, blank pages) always fail. Code that compiles but breaks at runtime is not done.
