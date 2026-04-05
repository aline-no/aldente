# Product Requirements Document

Purpose: define the problem, users, scope, and acceptance criteria for `{{PRODUCT_NAME}}` before any build phase begins. All other docs derive from this.

Fill this first. Mark `status: active` when scope is agreed. Phase 01 will not start until this file is active.

---

```yaml
id: PRD-001
title: "{{PRODUCT_NAME}}"
status: draft
phase: MVP | prototype | POC
owner: {{OWNER}}
created: {{DATE}}
```

---

## Problem

[One paragraph. What exists today, what breaks, what users are forced to do manually or can't do at all. Not the solution — the gap.]

## Users

| Type | Description |
|------|-------------|
| Primary | {{PRIMARY_USER}} — {{what they do and what they need}} |
| Secondary | (optional) |

## Scope

**In scope:**
- {{core feature 1}}
- {{core feature 2}}
- {{core feature 3}}

**Out of scope (not this version):**
- {{excluded feature 1}}
- {{excluded feature 2}}

## User Stories

Each story maps to a user journey in `docs/journeys.md`. The "Done when" condition is testable by someone who was not in the room.

| ID | As a... | I want to... | Done when... |
|----|---------|--------------|--------------|
| US-01 | {{user type}} | {{action}} | {{testable condition}} |
| US-02 | {{user type}} | {{action}} | {{testable condition}} |

## Open Questions

Unresolved before build starts. Each needs an owner and a target resolution date.

| ID | Question | Owner | Target |
|----|----------|-------|--------|
| OQ-01 | {{question}} | {{name}} | {{date}} |

---

## Definition of ready

This PRD is ready to move to Phase 01 when:
- [ ] Problem statement is specific (not generic)
- [ ] Primary user type is named
- [ ] Scope in/out list is agreed
- [ ] Every user story has a testable "Done when" condition
- [ ] No P0 open questions remain unresolved
- [ ] `status` is set to `active`
