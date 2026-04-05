![Aldente boilerplate header](images/aldente-boilerplate.webp)

# Aldente

**A SaaS boilerplate for building with AI-assisted tools.** Fill the docs, run the phases, ship a clean app — without rebuilding the fundamentals every time.

Aldente is the **build layer**. It gives you product definition templates, phased implementation prompts, and operational guides for agents. It stays product-agnostic and tooling-flexible.

## Before you start

Aldente assumes the product is already defined. Before running Phase 01, you need:
- A problem statement (what breaks today, for whom)
- A primary user type
- A scope boundary (what's in, what's out)
- User stories with testable acceptance criteria

Fill `docs/prd.md` first. It's the source of truth all other docs derive from. Phase 01 does not start until the PRD is `status: active`.

If the product isn't defined yet, define it before opening this repo. For a structured discovery and PRD authoring workflow that feeds directly into Aldente, see [prd-please](https://github.com/yesplease-studio/prd-please).

## What you get

| Folder | Purpose |
|--------|---------|
| `docs/` | Product definition templates — start with `prd.md`, then `adr.md` as technical decisions are made |
| `phases/` | 11 phased implementation prompts |
| `skills/` | Operational guides for agents: session protocol, quality gates, API patterns, QA |
| `agents/` | Tool-specific adapters for Claude Code, Cursor, Codex, Lovable |

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

Stack is a default, not a requirement. The method is tool-agnostic.

## Extends with

Aldente covers discovery → build. Two external tools extend the workflow for teams that need more:

- **[prd-please](https://github.com/yesplease-studio/prd-please)** — structured discovery and PRD authoring before Aldente. Produces a Strategic PRD that feeds directly into `docs/prd.md`.
- **[Archgate](https://github.com/archgate/cli)** — enforces ADRs via pre-commit hooks and CI/CD. Adds a `.rules.ts` enforcement layer on top of Aldente's lightweight `docs/adr.md`.

## Works with

**[Claude Code](agents/claude-code.md)** — best for complex multi-phase builds and iterative refactors. Includes a skills-friendly workflow loop, guard rails, and phase-by-phase reasoning. Recommended for production builds.

**[Lovable](agents/lovable.md)** — best for UI scaffolding and rapid iteration. Paste the phase prompt, attach the docs, review and repeat. Strong for Phases 01-03 and 10.

Also works with Codex, Cursor, and other AI-assisted builders. The phases are the same — only execution mechanics differ. See [agents/](agents/) for all adapters.

## Get started

See [setup.md](setup.md) for the full workflow, phase map, and doc order.

For AI agents: [AGENT_INSTRUCTIONS.md](AGENT_INSTRUCTIONS.md) and [agents/shared-protocol.md](agents/shared-protocol.md).

## License

MIT. See `LICENSE`.

---

Aldente is created and maintained by [Line Hjartarson](https://www.linkedin.com/in/linehjartarson/) at [Aline](https://aline.no).
