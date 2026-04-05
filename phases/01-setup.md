# Phase 1 – Setup

This phase is tool-agnostic.
Before running: ensure the agent can read the required `docs/*` inputs.
See `AGENT_INSTRUCTIONS.md` and `agents/README.md` for guidance.


## Goal
- Establish repo conventions for `{{PRODUCT_NAME}}`
- Decide baseline architecture and tooling
- Align on how `docs/` and `phases/` are used

## Inputs
- `setup.md`
- `docs/assets.md`
- `docs/design-guidelines.md`
- `docs/ui-structure.md`

## Assumptions
- `{{TECH_STACK}}` is either chosen or can be decided now
- The app does not have established conventions yet

### Guard rails: structure, type safety, and crash protection
Tasks
- Ensure folders exist: `src/components/ui`, `src/components/features`, `src/hooks`, `src/lib`, `src/types`, `src/validations`
- Type safety baseline:
  - add prop types for components
  - define shared DTO/domain types
  - define form payload types
  - optional Zod validation with inferred types
- Error handling baseline:
  - add `src/components/ErrorBoundary.tsx`
  - wrap the app/router root with `ErrorBoundary`
  - define async error strategy:
    - centralize API calls in `src/lib/*`
    - return typed results or throw typed errors
    - user-friendly error UI states (no white screens)

#### Minimal usage (wrap the app root)

If you have `src/main.tsx`:

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { ErrorBoundary } from "./components/ErrorBoundary";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <ErrorBoundary>
      <App />
    </ErrorBoundary>
  </React.StrictMode>
);
```

If you want to use a router layout, you can also wrap the top-level layout component instead.

## Constraints
- Keep structure stable; do not introduce new top-level folders unless required
- Use placeholders consistently (e.g., `{{PRODUCT_NAME}}`)
- Avoid project-specific logic or data
- Do not apply final styling or polish; leave visual refinement for Phase 10.

## Tasks
1. Define folder and file conventions for the build target.
2. Document baseline architecture decisions (routing, data layer, UI layers).
3. Create or update a minimal project skeleton for `{{PRODUCT_NAME}}`.
4. Add `.env.example` with required keys (no secrets).
5. Add a short usage note explaining how to run the remaining phases.

## Acceptance criteria
- [ ] Conventions are explicit and easy to follow
- [ ] Baseline architecture choices are recorded
- [ ] Skeleton compiles or renders without feature logic
- [ ] This phase outputs or updates the core project structure
- [ ] Folders exist and are referenced in `docs/ui-structure.md`
- [ ] Minimal TS typing coverage (no accidental `any`)
- [ ] `ErrorBoundary` exists and is used
- [ ] Async errors are handled consistently via a centralized approach
- [ ] ErrorBoundary template exists at `src/components/ErrorBoundary.tsx`
- [ ] API wrapper exists at `src/lib/api.ts`
- [ ] Shared API types exist at `src/types/api.ts`

## Verification
- [ ] Run the build command -- project compiles without errors
- [ ] Start the dev server -- no errors in terminal output
- [ ] Open the root route in a browser -- page renders (not blank)
- [ ] Check browser console -- no errors or failed requests
- [ ] Confirm `ErrorBoundary` catches a thrown error (temporarily throw in a component, verify fallback renders)

## Notes / common pitfalls
- If this phase does not apply (existing mature project), skip it.
- Avoid over-building; focus on a clean foundation.
- Skip or adjust this if you are not using React/Vite; keep the intent.
