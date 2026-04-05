# SaaS Boilerplate Setup

## What this repo is
A prompt + docs boilerplate for building SaaS products with AI-assisted builders without spaghetti code. You fill the docs, then run the prompts in phases to incrementally build a clean, scalable app.

## Choose your build tool
- Codex → [agents/codex.md](agents/codex.md)
- Claude Code → [agents/claude-code.md](agents/claude-code.md)
  - Includes a skills-friendly workflow loop + phase runner template.
- Cursor → [agents/cursor.md](agents/cursor.md)
- Lovable → [agents/lovable.md](agents/lovable.md)

The phases are the same; only execution mechanics differ.

## Recommended stack (default)
- Frontend: React + Vite
- Styling: Tailwind CSS + shadcn/ui
- Routing: React Router
- Data fetching: TanStack Query
- Backend/DB: Supabase (or any Postgres-compatible provider)
- Auth: Supabase Auth or StackAuth
- Payments: Stripe
- Email: Resend or Postmark
- Testing: Vitest (unit) + Playwright (e2e)

## Quick start
1. Clone or fork the repo.
2. Decide your build tool (Codex, Claude Code, Cursor, Lovable, or another agent).
3. Fill out `docs/` in this order:
   - [docs/prd.md](docs/prd.md) — **start here**. Problem, users, scope, user stories. Mark `status: active` before Phase 01.
   - [docs/adr.md](docs/adr.md) — technical architecture decisions. Add entries as significant choices are made during the build.
   - [docs/content-pages.md](docs/content-pages.md)
   - [docs/journeys.md](docs/journeys.md)
   - [docs/ui-structure.md](docs/ui-structure.md)
   - [docs/design-guidelines.md](docs/design-guidelines.md)
   - [docs/data-models.md](docs/data-models.md)
   - [docs/assets.md](docs/assets.md)
   - [docs/schema-initial.sql](docs/schema-initial.sql) (optional)
   - [docs/schema-cms.sql](docs/schema-cms.sql) (optional)
4. Run the prompts in `prompt/` in order (default):
   - [prompt/01-setup.md](prompt/01-setup.md)
   - [prompt/02-layouts.md](prompt/02-layouts.md)
   - [prompt/03-structure.md](prompt/03-structure.md)
   - [prompt/04-data-model.md](prompt/04-data-model.md)
   - [prompt/05-db-flow.md](prompt/05-db-flow.md)
   - [prompt/06-stripe.md](prompt/06-stripe.md)
   - [prompt/07-auth.md](prompt/07-auth.md)
   - [prompt/08-cms-admin.md](prompt/08-cms-admin.md) (optional)
   - [prompt/09-emails-admin.md](prompt/09-emails-admin.md)
   - [prompt/10-design-system.md](prompt/10-design-system.md)
   - [prompt/11-launch-audit.md](prompt/11-launch-audit.md) (optional)

## Boilerplate variables
Placeholders appear across `docs/` and `prompt/`. Replace them with your product info before or during a phase.

Common placeholders:
- `{{PRODUCT_NAME}}`, `{{ONE_LINER}}`, `{{TARGET_USERS}}`
- `{{CORE_FEATURES}}`, `{{PAGES}}`
- `{{TECH_STACK}}`, `{{DB_PROVIDER}}`, `{{AUTH_PROVIDER}}`, `{{PAYMENT_PROVIDER}}`, `{{EMAIL_PROVIDER}}`
- `{{BRAND_TONE}}`, `{{DESIGN_REFERENCES}}`

How to replace:
- Manual find/replace is enough. Use repo-wide search for `{{` to catch all placeholders.

## Preparation checklist
- PRD ready: `docs/prd.md` filled with problem, users, scope, user stories — `status: active`
- Product basics: name, one-liner, audience
- Feature scope and pages
- Design direction and tone
- Data model basics
- Integrations: DB, auth, payments, email, admin tooling
- Base env template: create `.env.example` with required keys (no secrets)

## Phase map
| Phase file | When to use | Inputs required | Output expectation |
| --- | --- | --- | --- |
| [prompt/01-setup.md](prompt/01-setup.md) | Starting a new build | [docs/prd.md](docs/prd.md) (required, must be active), [setup.md](setup.md), all other [docs/](docs/) you have so far | Repo conventions, tooling decisions, baseline architecture |
| [prompt/02-layouts.md](prompt/02-layouts.md) | After setup | [docs/ui-structure.md](docs/ui-structure.md), [docs/design-guidelines.md](docs/design-guidelines.md) | App shell, layouts, responsive structure |
| [prompt/03-structure.md](prompt/03-structure.md) | After layouts | [docs/ui-structure.md](docs/ui-structure.md), [docs/content-pages.md](docs/content-pages.md), [docs/journeys.md](docs/journeys.md) | Route structure and component boundaries |
| [prompt/04-data-model.md](prompt/04-data-model.md) | When data entities are known | [docs/data-models.md](docs/data-models.md), optional [docs/schema-initial.sql](docs/schema-initial.sql) and [docs/schema-cms.sql](docs/schema-cms.sql) | Types/entities and API assumptions |
| [prompt/05-db-flow.md](prompt/05-db-flow.md) | When you need DB/backend flow | [docs/data-models.md](docs/data-models.md), [docs/schema-initial.sql](docs/schema-initial.sql) and [docs/schema-cms.sql](docs/schema-cms.sql) | DB integration plan and data flow wiring |
| [prompt/06-stripe.md](prompt/06-stripe.md) | If billing is required | [docs/data-models.md](docs/data-models.md), [docs/journeys.md](docs/journeys.md) | Billing flows, plans, entitlements |
| [prompt/07-auth.md](prompt/07-auth.md) | If auth is required | [docs/data-models.md](docs/data-models.md), [docs/journeys.md](docs/journeys.md) | Auth flows, roles, protected routes |
| [prompt/08-cms-admin.md](prompt/08-cms-admin.md) | Optional CMS and admin surface | [docs/content-pages.md](docs/content-pages.md), [docs/journeys.md](docs/journeys.md), [docs/ui-structure.md](docs/ui-structure.md), [docs/data-models.md](docs/data-models.md), [docs/assets.md](docs/assets.md), [docs/schema-cms.sql](docs/schema-cms.sql) | CMS/admin surfaces ready for content ops |
| [prompt/09-emails-admin.md](prompt/09-emails-admin.md) | If email/admin is required | [docs/journeys.md](docs/journeys.md), [docs/content-pages.md](docs/content-pages.md) | Transactional emails and admin surfaces |
| [prompt/10-design-system.md](prompt/10-design-system.md) | For UI polish and consistency | [docs/design-guidelines.md](docs/design-guidelines.md) | Tokens, components, and accessibility |
| [prompt/11-launch-audit.md](prompt/11-launch-audit.md) | Optional launch readiness and audit | [docs/content-pages.md](docs/content-pages.md), [docs/journeys.md](docs/journeys.md), [docs/ui-structure.md](docs/ui-structure.md), [docs/data-models.md](docs/data-models.md), [docs/assets.md](docs/assets.md) | Launch checklist and code audit results |

## Skipping optional phases
- No DB: skip phase 5, remove DB references from `docs/data-models.md` and `docs/schema-*.sql`, and ensure later phases do not assume persistence.
- No payments: skip phase 6 and remove pricing/billing references in docs and prompts.
- No auth: skip phase 7 and remove protected routes, roles, and account flows.
- No email/admin: skip phase 9 and remove email templates/admin panel assumptions.

## Recommended workflow
- Paste one phase prompt at a time.
- Attach the relevant `docs/*` files as context inputs.
- Read `skills/build-session.md` for the full session protocol (start, execute, verify, handoff).
- After each phase:
  - Complete the phase's **Verification** section (each prompt has one).
  - Run the quality gate in `skills/code-review.md`.
  - Commit or checkpoint changes.
  - Keep the file structure stable before moving to the next phase.
- For phases that wire data (4-5), also read `skills/api-wiring.md` for API client and mock data patterns.
- For phases that touch UI, use `skills/frontend-qa.md` for screenshots, accessibility, and performance checks.

## Phase runner template (tool-agnostic)
Use this copy block in any tool:
- Read: [docs/](docs/) (list the inputs for this phase)
- Execute: [prompt/](prompt/) (choose the correct `XX-...md`)
- Output expectations: list the acceptance criteria from the phase
- If inputs are missing, stop and ask before proceeding

## Repo conventions
- `docs/` contains your source-of-truth product definitions.
- `prompt/` contains phased prompts to implement those docs.
- Use consistent naming:
  - Pages: `KebabCase` for routes (`/pricing`, `/app/settings`)
  - Components: `PascalCase` (`PricingTable`, `BillingCard`)
  - Entities: `snake_case` for tables, `PascalCase` for types
- Definition of done per phase:
  - Phase 1: baseline structure and decisions documented
  - Phase 2: layouts and responsive shells render
  - Phase 3: routes and modules map cleanly to docs
  - Phase 4: data entities and relationships defined
  - Phase 5: data flow is wired (or explicitly deferred)
  - Phase 6: billing flow is defined (or skipped)
  - Phase 7: auth flow is defined (or skipped)
  - Phase 8: CMS/admin surfaces defined (or skipped)
  - Phase 9: email/admin surfaces defined (or skipped)
  - Phase 10: UI tokens and component rules applied
  - Phase 11: launch checklist and audit completed (or skipped)
