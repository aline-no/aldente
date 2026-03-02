# Agent Adapters

AlDente has one canonical set of prompts in `prompt/`. Pick your tool and follow the adapter guide for how to run each phase.

## Shared protocol

All adapters use the same starter prompt and phase runner protocol: [shared-protocol.md](shared-protocol.md). Each adapter adds tool-specific guidance on top.

## Recommended flow

1. Read `agents/shared-protocol.md` for the starter prompt
2. Choose a tool adapter below
3. Run one phase at a time with the same prompt files
4. After each phase: commit, run the quality gate (`skills/code-review.md`), verify runtime
5. Move to the next phase

## Adapters

- Claude Code: [claude-code.md](claude-code.md) (includes skills-friendly workflow)
- Codex: [codex.md](codex.md)
- Cursor: [cursor.md](cursor.md)
- Lovable: [lovable.md](lovable.md)
