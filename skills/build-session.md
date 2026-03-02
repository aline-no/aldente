# Build Session

## Purpose

Define how an AI agent starts, executes, and ends a build session. This is the operating protocol that keeps agents focused, safe, and consistent across phases.

## When to Use

- Every time an agent starts working on a build phase
- When handing off between sessions (context window limit, different agent)
- When resuming work after a break

## Protocol

### Session Start

1. **Read the project instructions.** Read `AGENT_INSTRUCTIONS.md` and any project-level config (e.g., `CLAUDE.md`). This tells you the stack, conventions, and where docs live.
2. **Read the relevant docs.** For the current phase, read the specific `docs/*` files listed in the phase prompt. Don't skip inputs.
3. **Check git status.** Understand what's been done. Read recent commits. Don't duplicate work.
4. **Identify the scope.** One phase per session. State what you're building before you start.

### During the Session

5. **Build only what's in scope.** If you discover something outside scope, note it but don't do it.
6. **Reference docs for every decision.** If a doc specifies a pattern (component name, API endpoint, data type), use it exactly. Don't invent alternatives.
7. **Ask, don't assume.** If the docs are ambiguous or a decision isn't covered, stop and ask. Don't guess.
8. **Keep changes minimal.** Touch only the files needed for this phase. Don't refactor adjacent code, don't add features, don't "improve" things outside scope.

### Session End

9. **Verify the build compiles.** Run the build command. Fix any errors before continuing.
10. **Verify runtime.** Start the dev server and check:
    - Terminal output has no errors or unhandled warnings
    - If the phase touches UI: open the relevant page, confirm it renders
    - Check browser console for errors (failed network requests, CORS, undefined references)
    - If the phase touches API integration: confirm requests return data (or hit mock handlers without errors)
    - If something fails at runtime that compiled fine, fix it before committing
11. **Complete the phase's Verification section.** Each phase prompt includes specific verification steps. Run them.
12. **Commit with a clear message.** Format: `phase X: [what was done]`. One commit per logical unit of work.
13. **Summarize what was done.** List: files created/modified, decisions made, anything deferred.
14. **Flag blockers.** If something couldn't be completed, state what's blocked and why.

### Handoff Between Sessions

When context runs out or you're handing off to another agent:

15. **Write a session summary.** Include: what was completed, what's next, any open questions, any deviations from the docs.
16. **The next session starts at step 1.** Every session re-reads instructions and docs. No assumptions carry over.

## Rules

1. Never modify files outside the current phase's scope
2. Never skip reading project instructions and relevant docs
3. Never commit code that doesn't compile or fails at runtime
4. Never make architectural decisions that aren't in the docs -- flag them instead
5. One phase at a time. Finish and commit before starting the next
6. If a pre-commit hook fails, fix the issue and make a new commit. Never use `--no-verify`
7. Don't push to remote unless explicitly asked
