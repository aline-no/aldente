![Aldente boilerplate header](images/aldente-boilerplate.webp)

# SaaS Boilerplate

## What it is
A reusable prompt + docs kit for building SaaS products with AI-assisted builders. Fill the docs, run the phases, and ship a clean, consistent app without rebuilding the fundamentals every time.

## Who it is for
Builders who want a structured, prompt-driven workflow that stays product-agnostic and tooling-flexible.

## What you get
- **[docs/](docs/)** -- product definition templates (what to build)
- **[prompt/](prompt/)** -- phased implementation prompts (what to build per phase)
- **[skills/](skills/)** -- operational guides for agents (how to operate: session protocol, quality gates, API patterns, QA)
- **[agents/](agents/)** -- tool-specific adapters for running phases
- A repeatable flow from idea to build
- Optional Phase 8 for CMS + Admin and Phase 11 for Launch + Audit

## Recommended stack (default)
- Frontend: React + Vite
- Styling: Tailwind CSS + shadcn/ui
- Backend/DB: Supabase (or any Postgres-compatible provider)
- Auth: Supabase Auth or Clerk
- Payments: Stripe
- Email: Resend or Postmark

## Works with
Codex, Claude Code, Cursor, Lovable (and other AI-assisted builders). See [setup.md](setup.md) and [agents/README.md](agents/README.md).

## Quick start
Start with [setup.md](setup.md) for the full workflow and phase map.

## Using with AI agents
See [AGENT_INSTRUCTIONS.md](AGENT_INSTRUCTIONS.md) and [agents/README.md](agents/README.md) for adapters and workflow notes.

Starter prompt and phase runner protocol: [agents/shared-protocol.md](agents/shared-protocol.md).

## License
MIT. See `LICENSE`.
