# Phase 7 – Auth

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Implement authentication and role-based access
- Define protected routes and session state
- Support multiple providers (e.g., `{{AUTH_PROVIDER}}`)

## Inputs
- `docs/data-models.md`
- `docs/journeys.md`

## Assumptions
- Auth is required for `{{PRODUCT_NAME}}`
- Roles are defined in `docs/data-models.md`

## Constraints
- Keep auth provider replaceable
- Do not block public routes unnecessarily
- Preserve existing routing structure
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Implement login, signup, and logout flows.
2. Add session management and protected routes.
3. Implement role checks for sensitive areas.
4. Add account settings or profile basics.

## Acceptance criteria
- [ ] Auth flows function end-to-end
- [ ] Protected routes and role checks exist
- [ ] Session state is stable across reloads
- [ ] Output includes auth wiring and route guards

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- login and signup pages render
- [ ] Complete login flow -- session is established, protected route is accessible
- [ ] Reload a protected page -- session persists, user is not logged out
- [ ] Visit a protected route while logged out -- user is redirected to login
- [ ] Check browser console -- no auth-related errors

## Notes / common pitfalls
- If no auth is required, skip this phase.
- Avoid mixing auth logic with business logic.
