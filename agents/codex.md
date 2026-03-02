# Codex Adapter

See [shared-protocol.md](shared-protocol.md) for the standard starter prompt and phase runner protocol.

Codex is good at implementing structured changes across multiple files and keeping prompt constraints consistent across phases.

## How to run a phase

1. Open the phase file in `prompt/` (e.g., `prompt/02-layouts.md`).
2. Provide the phase prompt to Codex as the task.
3. Attach or reference the relevant `docs/*` files listed in the phase.
4. If unsure which docs, attach `docs/ui-structure.md`, `docs/design-guidelines.md`, and `docs/journeys.md` as baseline context.
5. Ask Codex to implement changes, complete the Verification section, and summarize outputs.

## Common pitfalls
- Skipping a required `docs/*` input
- Over-styling before the design system phase
- Introducing product-specific logic too early
- Changing file paths without updating references
