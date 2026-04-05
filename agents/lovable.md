# Lovable Adapter

See [shared-protocol.md](shared-protocol.md) for the standard starter prompt and phase runner protocol.

Lovable is strong for UI scaffolding and rapid iteration with structured prompts and attached context. Best for Phases 01-03 (scaffold, layouts, structure) and Phase 10 (design system polish).

## Plan mode

Lovable's plan mode shows a proposed plan before executing. Use it — it changes the workflow meaningfully:

- Review the plan before approving. Check it matches the phase scope and hasn't pulled in out-of-scope work.
- If the plan includes changes outside the phase boundary, reject it and tighten the prompt before rerunning.
- Plan mode makes the one-phase-at-a-time discipline easier to enforce: you can see what's coming rather than cleaning up after it.

The original constraint of "one small prompt at a time" was a workaround for unpredictable output. With plan mode, you can give the full phase prompt and use the plan review as your control point instead.

## How to run a phase

1. Read `docs/prd.md` and `docs/adr.md` before starting. Know the scope and any locked technical decisions.
2. Copy a phase prompt from `prompt/` (e.g., `prompt/02-layouts.md`).
3. Paste it into Lovable as the task. Enable plan mode.
4. Attach the `docs/*` files listed in the phase as context.
   - If context limits apply, prioritise: `docs/prd.md`, `docs/ui-structure.md`, `docs/journeys.md`, `docs/design-guidelines.md`.
5. Review the plan. Approve only if it stays within the phase scope.
6. Review the output and complete the phase's Verification section before moving on.

Commit or checkpoint after each phase.

## What Lovable is good at in this workflow

- Phases 01-03: project scaffold, layout shells, route and component structure
- Phase 10: design system polish, component refinement, visual consistency
- Quick UI iteration when the docs are well-defined

## What to hand off to Claude Code

- Phases 04-05: data model and DB flow wiring (Supabase, SQL, typed hooks)
- Phase 07: auth flows, protected routes, role-based access
- Anything requiring precise TypeScript types, complex state, or multi-file refactors

## Guard rails

- One phase at a time. Never combine phases in a single prompt.
- Attach required docs for every phase — Lovable has no memory of previous sessions.
- Do not polish visuals before Phase 10. Use shadcn defaults in earlier phases.
- If Lovable adds something outside the phase scope, remove it before the next phase.

## Common pitfalls

- Running phases without the required docs attached
- Over-polishing visuals before the design system phase (Phase 10)
- Forgetting to update docs when Lovable makes assumptions that deviate from them
- Mixing marketing and app routes unintentionally
- Letting Lovable carry state assumptions across phases — it doesn't remember
