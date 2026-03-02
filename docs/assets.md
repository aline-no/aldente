# Assets

Purpose: track visual and legal assets needed for `{{PRODUCT_NAME}}` so phases that depend on them (setup, design system, launch audit) have a single reference.

## Template

### Brand assets
- Logo (SVG + PNG): `[path or URL]`
- Favicon (ICO + SVG): `[path or URL]`
- OG image (1200x630): `[path or URL]`
- App icon (if applicable): `[path or URL]`

### Empty state illustrations
- No data / first-time: `[path or description]`
- No results (search/filter): `[path or description]`
- Error state: `[path or description]`
- Success / completion: `[path or description]`

### Legal content
- Privacy policy: `[drafted / placeholder / URL]`
- Terms of service: `[drafted / placeholder / URL]`
- Cookie policy (if applicable): `[drafted / placeholder / URL]`

### Third-party assets
- Font files or CDN links: `[list]`
- Icon library: `[e.g., Lucide, Heroicons]`
- Stock images or illustrations: `[source and license]`

## Notes
- Keep paths relative to the repo root where possible.
- Mark assets as `placeholder` if using temporary versions during build phases.
- Replace all placeholders before Phase 11 (launch audit).

## Example

Brand assets
- Logo: `public/logo.svg`
- Favicon: `public/favicon.ico`
- OG image: `public/og-image.png`

Empty state illustrations
- No data: inline SVG placeholder (replace in Phase 10)
- Error state: generic error component with icon

Legal content
- Privacy policy: placeholder (draft before launch)
- Terms of service: placeholder (draft before launch)
