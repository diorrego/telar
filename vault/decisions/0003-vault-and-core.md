---
id: ADR-0003
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0003: Two parts: `vault/` and `core/`

## Context

Diego asked for two parts: a vault to record projects, QA and everything needed to develop Telar, and a second part holding Telar itself (its code, rules and how it works), named "core, or whatever name best represents it".

## Decision

- `vault/` holds the thinking: foundations, decisions, projects, QA, templates, views. Documentation only, ever.
- `core/` holds Telar itself: the workshop defined as code. In prose it is "the core".
- Every artifact in `core/` traces back to a project in `vault/projects/`.

## Consequences

- Renaming is cheap while the core has no code. After that, a rename needs a new ADR.
- The agent first gave the folder a metaphorical name; Diego rejected it the same day and chose `core`. That pushback is correction [C-0001](../qa/corrections/C-0001-metaphorical-folder-name.md), and it added the "Plain names" rule to the root `CLAUDE.md`.

## Alternatives considered

- **`workshop`, `kit`, `engine`.** Offered; Diego chose `core`.
- **A metaphorical name.** Rejected by Diego (C-0001).
- **`factory`.** Contradicts the workshop-first approach.
- **`harness`.** Telar is not a harness; it uses existing ones.
