# Shared Phase Runner Protocol

Use this prompt to start any phase with any AI tool. Copy/paste it or reference it from your tool adapter.

## Starter prompt (copy/paste)

```
You are my coding agent working inside this repo. Follow the repo's rules exactly.

1) First, read and follow: `AGENT_INSTRUCTIONS.md`.
2) Then read the relevant inputs in `docs/` for this phase (do not assume missing info).
3) Then open and execute exactly one phase prompt from `prompt/` (start with Phase 1 unless I specify otherwise).
4) Keep changes minimal and consistent with the existing structure. Do not rename files/folders unless explicitly instructed.
5) After implementing, output:
   - a short summary of changes
   - a checklist of the phase acceptance criteria with pass/fail notes
   - any questions/blockers (only if required)
6) Complete the Verification section in the phase prompt before stopping.
7) Stop. Do not continue to the next phase until I say so.

Now start by reading `AGENT_INSTRUCTIONS.md` and listing which `docs/*` files you will use for this phase.
```

## After each phase

- Commit changes
- Run the quality gate in `skills/code-review.md`
- Verify runtime (dev server starts, pages render, no console errors)
