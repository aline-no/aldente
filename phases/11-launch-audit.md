# Phase 11 – Launch + Audit

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


Skip this phase if you are not approaching launch or do not need a structured audit.

## Goal
- Confirm launch readiness across product, security, and operations
- Run a pragmatic code audit and fix high-risk issues
- Create a clear ship checklist

## Inputs
- `docs/content-pages.md`
- `docs/journeys.md`
- `docs/ui-structure.md`
- `docs/data-models.md`
- `docs/assets.md`

## Assumptions
- Core features and routes are in place
- Any optional phases required for launch are complete

## Constraints
- Keep checklist short and actionable
- Focus on shipping, not new features
- Preserve existing structure and naming

## Tasks
1. Run the launch checklist (see below) and log results.
2. Perform the code audit (see below) and fix or document issues.
3. Confirm rollback plan and backups (if applicable).
4. Update any missing legal/SEO assets.

## Acceptance criteria
- [ ] Phase 11 file exists and follows the standard structure
- [ ] Skip guidance is clear and visible
- [ ] Launch checklist is included
- [ ] Code audit checklist is included
- [ ] All `docs/*` references are valid

## Verification
- [ ] Run full build -- project compiles and builds for production without errors
- [ ] Run Lighthouse audit on key pages -- performance > 70, accessibility > 90, best practices > 80
- [ ] Run accessibility audit (`npx axe`) on all public pages -- no critical or serious violations
- [ ] Search codebase for `{{` -- no unresolved placeholders remain
- [ ] Confirm all legal pages render and are linked from the footer
- [ ] Confirm rollback plan is documented and tested

## Notes / common pitfalls
- Do not ship with placeholder content or empty legal pages.
- Avoid last-minute scope changes; fix only launch blockers.

## Launch checklist
Product/UX
- [ ] Core journeys complete and testable
- [ ] Empty/loading/error states present
- [ ] Copy reviewed for placeholders

Security & Privacy
- [ ] Admin routes protected or locally gated
- [ ] Secrets are in env vars (not committed)
- [ ] Privacy/terms pages exist and match product scope

Performance
- [ ] Critical pages load within target budgets
- [ ] Images optimized and lazy-loaded where appropriate

Observability
- [ ] Error tracking and basic logging in place
- [ ] Key events are captured (signup, purchase, core task)

Data & migrations (if DB)
- [ ] Migrations are tracked and reversible
- [ ] Seed data is available for local/dev

Payments (if applicable)
- [ ] Webhook handling tested in sandbox
- [ ] Plan/entitlement mapping verified

Email deliverability (if applicable)
- [ ] SPF/DKIM/DMARC configured
- [ ] Templates render across major clients

Legal pages
- [ ] Privacy and terms pages linked from footer
- [ ] Data retention policy documented

SEO + OpenGraph (if marketing pages exist)
- [ ] Titles and meta descriptions set
- [ ] OG images present for key pages

Rollback plan + backups
- [ ] Rollback steps documented
- [ ] Backups enabled (DB and assets)

## Code audit checklist
- Dependency audit: remove unused deps, review vulnerable packages
- Env vars: validate required vars and defaults
- AuthZ checks: admin endpoints and route guards verified
- Input validation: schemas (e.g., Zod) on all external inputs
- Error handling: user-safe errors and internal logging
- Logging: no secrets or PII in logs
- Rate limiting: note endpoints that need throttling
- DX cleanup: dead code, TODOs, naming consistency, folder hygiene
- Accessibility: keyboard navigation, focus states, labels, contrast
