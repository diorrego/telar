---
id: ADR-0005
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0005: Documentation before code

## Context

Diego asked for no code for now: only the folder structure, the README, `CLAUDE.md` and `AGENTS.md` files, and the documents needed to start. The design of the core has not been decided, and the first projects have not been written.

## Decision

- The repository contains only Markdown documents and folder structure.
- `core/` holds folder contracts (`README.md` files) and agent instructions only.
- No code, configuration, schema or example file is added until a plan in `vault/projects/` is `active` and its current phase calls for it.

## Consequences

- The first projects are diagnoses and plans.
- Corrections can be logged but not yet encoded as checks; they stay `logged` with a proposed encoding and form the backlog of the first core projects.
- This decision ends when Diego says go on the first plan that requires code. That plan's log records it, and this ADR is then marked superseded by a short ADR that records the transition.

## Alternatives considered

- **Scaffold code now.** It would fix formats and tooling before any diagnosis. Rejected by Diego.
