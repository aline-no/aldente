![Aldente boilerplate header](images/aldente-boilerplate.webp)

# SaaS Boilerplate

## What it is
A reusable prompt + docs kit for building SaaS products with AI-assisted builders. Fill the docs, run the phases, and ship a clean, consistent app without rebuilding the fundamentals every time.

## Who it is for
Builders who want a structured, prompt-driven workflow that stays product-agnostic and tooling-flexible.

## Before you start

Aldente is the **build layer**. It assumes you've already defined what to build.

Before running Phase 01, you need:
- A problem statement (what breaks today, for whom)
- A primary user type
- A scope boundary (what's in, what's out)
- User stories with testable acceptance criteria

Fill `docs/prd.md` first. It's the source of truth that all other docs derive from. Phase 01 should not start until the PRD is marked `status: active`.

If the product isn't defined yet, define it before opening this repo. For a structured discovery and PRD authoring workflow that feeds directly into Aldente, see [prd-please](https://github.com/yesplease-studio/prd-please).

## What you get
- **[docs/](docs/)** -- product definition templates (what to build) — start with `docs/prd.md`
- **[prompt/](prompt/)** -- phased implementation prompts (what to build per phase)
- **[skills/](skills/)** -- operational guides for agents (how to operate: session protocol, quality gates, API patterns, QA)
- **[agents/](agents/)** -- tool-specific adapters for running phases
- A repeatable flow from defined product to shipped app
- Optional Phase 8 for CMS + Admin and Phase 11 for Launch + Audit

## Recommended stack (default)
- Frontend: React + Vite
- Styling: Tailwind CSS + shadcn/ui
- Routing: React Router
- Data fetching: TanStack Query
- Backend/DB: Supabase (or any Postgres-compatible provider)
- Auth: Supabase Auth or StackAuth
- Payments: Stripe
- Email: Resend or Postmark
- Testing: Vitest (unit) + Playwright (e2e)

## Works with
Codex, Claude Code, Cursor, Lovable (and other AI-assisted builders). See [setup.md](setup.md) and [agents/README.md](agents/README.md).

## Quick start
Start with [setup.md](setup.md) for the full workflow and phase map.

## Using with AI agents
See [AGENT_INSTRUCTIONS.md](AGENT_INSTRUCTIONS.md) and [agents/README.md](agents/README.md) for adapters and workflow notes.

Starter prompt and phase runner protocol: [agents/shared-protocol.md](agents/shared-protocol.md).

## License
MIT. See `LICENSE`.
