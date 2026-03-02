# Phase 2 – Layouts

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Build the app shell and layout patterns
- Ensure responsive behavior across core views
- Add empty/loading/error states scaffolding

## Inputs
- `docs/ui-structure.md`
- `docs/design-guidelines.md`
- `docs/assets.md`

## Assumptions
- Phase 1 established basic project structure
- Brand tokens and layout direction exist

## Constraints
- Preserve existing routing and file structure
- Use `{{BRAND_TONE}}` and `{{DESIGN_REFERENCES}}` as style guidance
- No product-specific copy beyond placeholders
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Implement marketing and app layout shells.
2. Add responsive layout rules and breakpoints.
3. Create base empty/loading/error state components.
4. Wire layout usage for primary routes.

## Acceptance criteria
- [ ] Layouts render cleanly on mobile and desktop
- [ ] Empty/loading/error states exist and are reusable
- [ ] Layouts map to `docs/ui-structure.md`
- [ ] Output is limited to layout and shell structure

## Verification
- [ ] Start the dev server -- no errors in terminal output
- [ ] Navigate to each primary route -- layouts render without blank screens
- [ ] Resize the browser to mobile width -- layout responds (no horizontal scroll, no overlapping elements)
- [ ] Check browser console -- no errors or warnings on any route

## Notes / common pitfalls
- If layouts are already complete, skip this phase.
- Avoid hardcoding content; use placeholders or generic copy.
