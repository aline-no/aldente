# Phase 9 – Emails and Admin

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Define transactional email flows
- Provide a lightweight admin surface
- Keep both optional and modular

## Inputs
- `docs/journeys.md`
- `docs/content-pages.md`
- `docs/data-models.md`

## Assumptions
- `{{EMAIL_PROVIDER}}` is chosen (or can be stubbed)
- Admin needs are defined

## Constraints
- Do not build a full admin app unless required
- Keep emails template-based and reusable
- Preserve public/app separation
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Define key transactional emails and triggers.
2. Implement email templates or stubs.
3. Create an admin surface for core entities.
4. Add access controls for admin views.

## Acceptance criteria
- [ ] Emails exist for key journeys
- [ ] Admin surfaces cover core entities
- [ ] Access control is enforced
- [ ] Output includes email templates and admin routes

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- admin routes render
- [ ] Email templates render with sample data (preview or test send)
- [ ] Admin access controls work (protected if auth exists, gated locally if not)
- [ ] Check browser console -- no errors on admin or email preview routes

## Notes / common pitfalls
- If email/admin is not needed, skip this phase.
- Avoid hardcoding provider-specific logic.
