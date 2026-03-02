# Phase 4 – Data Model

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Define types and entities for `{{PRODUCT_NAME}}`
- Specify relationships and permissions
- Outline API surface assumptions

## Inputs
- `docs/data-models.md`
- `docs/schema-initial.sql` (optional)
- `docs/schema-cms.sql` (optional)

## Assumptions
- Core entities are known or can be derived
- DB provider is decided (`{{DB_PROVIDER}}`)

## Constraints
- Keep entities generic and product-agnostic
- Use placeholders for any product-specific fields
- Do not implement full DB integration yet
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Translate entities into typed models or schemas.
2. Define relationships and access rules.
3. Document API assumptions (REST/RPC, endpoints).
4. Align with optional SQL references if provided.

## Acceptance criteria
- [ ] Entities and relationships are clear
- [ ] Permissions and roles are specified
- [ ] API assumptions are documented
- [ ] Output is limited to data definitions and types

## Verification
- [ ] Run the build command -- project compiles without TypeScript errors
- [ ] Confirm all entity types are importable from the types directory
- [ ] If using Zod schemas: verify inferred types match entity interfaces
- [ ] Start the dev server -- pages that reference data types still render (even without data)

## Notes / common pitfalls
- If there is no data model, skip this phase.
- Avoid overfitting to one provider.
