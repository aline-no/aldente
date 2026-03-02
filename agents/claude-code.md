# Claude Code Adapter

See [shared-protocol.md](shared-protocol.md) for the standard starter prompt and phase runner protocol.

Claude Code is strong at iterative refactors and detailed reasoning when implementing prompt-driven changes.

## Skills-friendly workflow

### The loop (do this every phase)
1. Paste the starter prompt from `agents/shared-protocol.md`.
2. Read `AGENT_INSTRUCTIONS.md`.
3. Read the relevant `docs/*` inputs for the phase.
4. Execute exactly one `prompt/XX-*.md`.
5. Complete the phase's Verification section.
6. Run the quality gate (`skills/code-review.md`).
7. Output a summary of changes + acceptance criteria pass/fail + blockers only if required.
8. STOP (do not proceed to the next phase).

Commit after each phase.

### Mapping Claude "skills" to phases
- Read inputs: summarize docs and call out missing info.
- Plan: max 5 bullets.
- Implement: do the work.
- Review: check references, naming consistency, missing outputs.
- Validate: tick acceptance criteria pass/fail.

### Guard rails (non-negotiable)
- No renames unless instructed.
- No invented files; create only what the phase requires.
- If inputs are missing, stop and ask; do not guess.
- Commit after each phase.

## How to run a phase

1. Open the phase file in `prompt/` (e.g., `prompt/03-structure.md`).
2. Provide the phase prompt as the instruction.
3. Supply the `docs/*` inputs listed in that phase.
4. Keep the docs visible for the entire run to avoid drift.

## Common pitfalls
- Phase drift across multiple prompts
- Assumption creep (auth/billing assumed when not in scope)
- Doc/code mismatch after edits
- Missing optional docs that still influence scope
- Mixing implementation with styling too early
- Introducing new folders without updating docs
