# UI Structure

Purpose: define route map, layouts, and module breakdown for `{{PRODUCT_NAME}}`.

## Template
### Route map
- Public routes: `{{PAGES}}`
- App routes: `/app/*`
- Auth routes: `/login`, `/signup`, `/reset`
- Legal routes: `/privacy`, `/terms`

### Layout patterns
- Marketing layout: header, hero, sections, footer
- App layout: sidebar/nav, top bar, content
- Settings layout: tabs or left nav

### Page modules
- Page: `/pricing`
  - Modules: pricing tiers, FAQ, CTA
- Page: `/app/dashboard`
  - Modules: summary cards, activity, quick actions

### Reusable components
- Navigation: header, footer, sidebar
- UI blocks: cards, tables, forms, modals
- Feedback: empty, loading, error states

### Frontend folder structure (recommended)
src/
components/
ui/         // shadcn/ui + shared primitives only
features/   // feature-level components grouped by domain
contexts/     // shared React contexts (cross-cutting only, not feature state)
hooks/        // reusable React hooks
lib/          // utilities (fetchers, formatters, config)
types/        // shared TypeScript types (DTOs, domain types)
validations/  // zod schemas (forms + API payloads)

Rules
- `components/ui` = reusable primitives, no business logic
- `components/features` = feature components, can import ui primitives
- shared API/domain types live in `types/`
- validations in `validations/` and infer TS types where possible
- keep API calls centralized in `lib/` (e.g. `lib/api.ts`) to avoid scattered error handling
- Recommended defaults (optional): `src/components/ErrorBoundary.tsx`, `src/lib/api.ts`, `src/types/api.ts`

### Admin routes (optional)
- `/admin` dashboard
- `/admin/users`
- `/admin/content`
- `/admin/settings`

## Example
Route map
- Public: `/`, `/pricing`, `/about`
- App: `/app`, `/app/settings`

Layout patterns
- App layout: sidebar + top bar + content

Reusable components
- `PricingTable`, `PlanCard`, `FeatureList`
