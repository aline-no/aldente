# Architecture Decision Records

Technical decisions that affect structure, infrastructure, or patterns. One entry per significant decision.

**Relationship to PRD:** The PRD (`docs/prd.md`) defines requirements — what to build. ADRs document the technical decisions made to address those requirements — why this approach, what alternatives were rejected.

Build agents read this before making implementation choices. Do not override an accepted ADR without updating this file first.

---

## Template

```
## ADR-NNN: [Title]
**Status:** proposed | accepted | deprecated
**Date:** YYYY-MM-DD
**PRD refs:** (optional — US-01, OQ-02, etc.)

### Context
What situation requires a decision? What constraints exist?

### Decision
What was decided?

### Rationale
Why this choice? What makes it better than alternatives for this context?

### Alternatives considered
- **Option A:** why rejected
- **Option B:** why rejected

### Consequences
What becomes easier? What becomes harder or requires more care?
```

---

<!-- Add ADRs below this line -->
