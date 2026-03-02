# Lovable Adapter

See [shared-protocol.md](shared-protocol.md) for the standard starter prompt and phase runner protocol.

Lovable is strong for UI scaffolding and rapid iteration with structured prompts and attached context.

## How to run a phase

1. Copy a phase prompt from `prompt/` (e.g., `prompt/02-layouts.md`).
2. Paste it into Lovable as the task.
3. Attach the `docs/*` files listed in the phase as context.
4. If context limits apply, prioritize `docs/ui-structure.md`, `docs/design-guidelines.md`, and `docs/journeys.md`.
5. Review changes and rerun the phase if needed.

## Common pitfalls
- Running phases without the required docs
- Over-polishing visuals before the design system phase
- Forgetting to update docs when assumptions change
- Mixing marketing and app routes unintentionally
