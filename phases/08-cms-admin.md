# Phase 8 – CMS + Admin

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


Skip this phase if you do not need CMS content management or an admin surface.

## Goal
- Implement a minimal CMS (flat-file or DB-backed)
- Provide an admin surface for users, content, and settings
- Keep admin access safe and clearly gated

## Inputs
- `docs/content-pages.md`
- `docs/journeys.md`
- `docs/ui-structure.md`
- `docs/data-models.md`
- `docs/assets.md`
- `docs/schema-cms.sql` (optional)

## Assumptions
- Phase 2/3 established core layouts and routes
- Phase 4 defined entities and roles
- Auth may or may not exist

## Constraints
- Keep CMS/admin modular and optional
- Avoid product-specific logic or hardcoded content
- Preserve existing structure and naming
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Decide CMS level:
   - Level A: Flat-file CMS (JSON/MD in repo, simple UI edits or export)
   - Level B: DB-backed CMS (tables like `pages`, `content_blocks`, `media`, `redirects`, `seo_meta`)
   Choose based on `{{DB_PROVIDER}}` and whether Phase 5 exists.
2. Implement CMS content flow:
   - Define content models and storage
   - Add basic create/update/publish flow
   - Wire marketing/static pages to CMS content
3. Build admin MVP under `/admin/*`:
   - Routes: `/admin`, `/admin/users`, `/admin/content`, `/admin/settings`
   - Modules: users/roles, content/pages, feature flags/settings
   - Optional: audit log viewer if events exist
   - Optional: impersonate user (explicit warning and opt-in only)
4. Add access controls:
   - If auth exists, require admin role for `/admin/*`
   - If no auth, gate admin locally and mark as non-production

## Acceptance criteria
- [ ] Phase 8 file exists and follows the standard structure
- [ ] Skip guidance is clear and visible
- [ ] CMS Level A/B decision guidance is present
- [ ] Admin route group and module list are defined
- [ ] Access controls are explicit and safe
- [ ] All `docs/*` references are valid

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- navigate to `/admin` -- page renders (or access denied if not authorized)
- [ ] If auth exists: confirm admin routes require admin role
- [ ] If no auth: confirm admin routes show a non-production warning
- [ ] Create or edit a content item -- changes persist (or confirm stub behavior)
- [ ] Check browser console -- no errors on admin routes

## Notes / common pitfalls
- Avoid building a full CMS; keep it minimal and fit-for-purpose.
- Do not expose admin without explicit gating and warnings.
- Keep content models aligned with `docs/content-pages.md`.
