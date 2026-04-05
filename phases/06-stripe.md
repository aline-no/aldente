# Phase 6 – Billing

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Define plans, entitlements, and billing flows
- Implement checkout and post-purchase states
- Support a provider like `{{PAYMENT_PROVIDER}}` (Stripe preferred)

## Inputs
- `docs/data-models.md`
- `docs/journeys.md`
- `docs/content-pages.md`

## Assumptions
- Billing is required for `{{PRODUCT_NAME}}`
- Plans and pricing are defined

## Constraints
- Keep billing logic isolated and replaceable
- Do not require production keys
- Avoid hardcoding pricing in multiple places
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Define plan and entitlement models.
2. Implement checkout flow and confirmation state.
3. Add webhook or callback handling stubs.
4. Add billing settings or customer portal access.

## Acceptance criteria
- [ ] Plans and entitlements are represented in the data model
- [ ] Checkout and confirmation flows exist
- [ ] Billing settings surface is available
- [ ] Output includes billing flow and integration points

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- navigate to the pricing/checkout page, confirm it renders
- [ ] Trigger checkout flow -- confirm redirect to payment provider or inline form loads
- [ ] Verify post-purchase state -- confirmation page or success state renders
- [ ] Check browser console -- no errors related to billing integration

## Notes / common pitfalls
- If there is no paid plan, skip this phase.
- Avoid mixing billing concerns with unrelated features.
