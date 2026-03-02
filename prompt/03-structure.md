# Phase 3 – Structure

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Define routing strategy and component boundaries
- Map pages to modules and reusable components
- Align UI structure to product journeys

## Inputs
- `docs/ui-structure.md`
- `docs/content-pages.md`
- `docs/journeys.md`

## Assumptions
- Layout shells exist from phase 2
- The route map is defined in `docs/ui-structure.md`

## Constraints
- Do not rename existing routes unless necessary
- Keep page and component naming consistent
- Avoid product-specific logic or data
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Implement route structure for public and app areas.
2. Create page modules based on `docs/ui-structure.md`.
3. Add reusable components used across multiple pages.
4. Stub any missing pages with placeholder content.

## Acceptance criteria
- [ ] Routes are in place and navigable
- [ ] Page modules align with `docs/*`
- [ ] Shared components are extracted and reusable
- [ ] Output includes page and component structure updates

## Verification
- [ ] Start the dev server -- no errors in terminal output
- [ ] Navigate to every route defined in `docs/ui-structure.md` -- each page renders
- [ ] Click between routes -- navigation works without full page reloads
- [ ] Check browser console on each route -- no errors
- [ ] Confirm stubbed pages show placeholder content (not blank)

## Notes / common pitfalls
- If structure is already defined, skip this phase.
- Keep modules thin; avoid premature feature logic.
