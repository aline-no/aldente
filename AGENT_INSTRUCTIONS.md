# Agent Instructions

## Core principles
- Keep filenames and prompt structure stable.
- Do not create tool-specific prompt variants.
- Update `docs/*` references if anything moves.
- Prefer small, phase-scoped changes.

## How phases are executed
- Before reading any other docs, check for `docs/prd.md`. If it exists and `status: active`, read it first — it is the source of truth for scope, users, and acceptance criteria.
- If `docs/prd.md` is missing or `status: draft`, stop and ask before proceeding. Do not infer scope from other docs.
- Read the required `docs/*` inputs for the phase.
- Follow the phase prompt tasks step-by-step.
- Update only the files needed for that phase.
- Each phase includes a **Verification** section. Complete it before marking the phase done.

## Session protocol
Follow `skills/build-session.md` for how to start, execute, and end a build session. Key points:
- Re-read project instructions and docs at the start of every session.
- Build only what's in scope. Note out-of-scope issues but don't fix them.
- Verify both compile and runtime before committing.
- Write a session summary when handing off.

## Output expectations
- Each phase should produce the outputs listed in its acceptance criteria.
- Document deviations and missing inputs instead of guessing.

## Quality bar
- Type safety baseline: typed props, shared DTO/domain types, optional Zod with inferred types.
- Error handling: ErrorBoundary usage + centralized API wrapper.
- Accessibility: keyboard access, focus states, labels, empty/loading/error states.

## Quality gate
After completing a phase, run the checklist in `skills/code-review.md`. This covers:
- Scope check, type safety, component quality, data flow
- Accessibility, security, code hygiene
- Build health and runtime verification
- Frontend QA (screenshots, axe-core, Lighthouse) via `skills/frontend-qa.md`

A phase is not done until the quality gate passes.

## Skills reference
The `skills/` folder contains operational guides for agents:

| Skill | When to read |
|-------|-------------|
| `skills/build-session.md` | Every session (start, execute, handoff protocol) |
| `skills/code-review.md` | After every phase (quality gate checklist) |
| `skills/api-wiring.md` | Phases 4-5 (data model, DB flow) and when adding API endpoints |
| `skills/frontend-qa.md` | After any phase that touches UI, and required for Phase 10/11 |

## When to skip a phase
- Skip if the phase does not apply to the product scope.
- Remove or adjust downstream assumptions if you skip.
