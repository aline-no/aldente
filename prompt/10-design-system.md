# Phase 10 – Design System

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Apply visual tokens and component rules
- Ensure accessibility and consistent UI patterns
- Align UI with `{{BRAND_TONE}}`

## Inputs
- `docs/design-guidelines.md`
- `docs/assets.md`

## Assumptions
- Layouts and components exist
- Design guidelines are complete

## Constraints
- No large structural changes
- Do not introduce new design systems unless required
- Keep styles consistent across app and marketing

## Tasks
1. Implement tokens (colors, typography, spacing).
2. Update core components to match guidelines.
3. Apply accessibility rules (focus, contrast, labels).
4. Ensure consistency across marketing and app views.

## Acceptance criteria
- [ ] Tokens are applied globally
- [ ] Components follow defined rules
- [ ] Accessibility basics are covered
- [ ] Output includes style updates and component refinement

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- visually inspect key pages (screenshot recommended)
- [ ] Check responsive behavior -- mobile and tablet viewports render correctly
- [ ] Run accessibility audit (`npx axe http://localhost:5173/`) -- no critical or serious violations
- [ ] Verify focus states -- tab through interactive elements, confirm visible focus indicators
- [ ] Check consistency -- marketing and app views use the same tokens

## Notes / common pitfalls
- If a design system already exists, skip this phase.
- Avoid styling one-off screens differently.
