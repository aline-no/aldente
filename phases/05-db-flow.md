# Phase 5 – Database + Backend Flow

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Define data flow between UI and backend
- Implement core read/write paths
- Keep Supabase as a first-class option, but stay provider-agnostic

## Inputs
- `docs/data-models.md`
- `docs/schema-initial.sql` (optional)
- `docs/schema-cms.sql` (optional)

## Assumptions
- `{{DB_PROVIDER}}` is chosen (Supabase or alternative)
- Entities from phase 4 exist

## Constraints
- Do not hardcode provider-specific logic unless required
- Keep data flows minimal and focused on core journeys
- Preserve existing structure
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Map UI actions to backend operations.
2. Implement repositories or API calls for core entities.
3. Add data loading and mutation patterns (with error states).
4. Document provider-specific setup if using Supabase.

## Acceptance criteria
- [ ] Core CRUD flows exist for key entities
- [ ] Error/loading states are wired to data flow
- [ ] Provider setup is documented where needed
- [ ] Output includes data flow wiring and backend integration points

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- no errors in terminal output
- [ ] Navigate to pages with data -- they render loading states, then data (or empty states if no backend)
- [ ] If using mocks (`VITE_MOCK_API=true`): confirm mock data appears in the UI
- [ ] Check browser console -- no failed network requests (unless backend is intentionally unavailable)

## Notes / common pitfalls
- If there is no DB or backend, skip this phase.
- Avoid coupling UI too tightly to a single provider.
