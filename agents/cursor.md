# Cursor Adapter

See [shared-protocol.md](shared-protocol.md) for the standard starter prompt and phase runner protocol.

Cursor is good for fast, interactive edits and refactors while keeping phase scope tight.

## How to run a phase

1. Open the phase file in `phases/` (e.g., `phases/04-data-model.md`).
2. Paste the phase prompt into Cursor's instruction panel.
3. Open the listed `docs/*` inputs in the editor or attach them via context selection.
4. Apply changes, complete the Verification section, and validate against acceptance criteria.

## Common pitfalls
- Not including the `docs/*` inputs in context
- Editing more than one phase at a time
- Skipping acceptance criteria checks
- Renaming files without updating references
