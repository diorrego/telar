---
id: ADR-0003
status: accepted
date: 2026-11-24
decided_by: claude, on delegation from diego
superseded_by:
---

# ADR-0003: Two parts: `vault/` and `loom/`

## Context

Diego asked for two parts: a vault to record projects, QA and everything needed to develop Telar, and a second part holding Telar itself (its code, rules and how it works), named "core, or whatever name best represents it". The choice of name was delegated.

## Decision

- `vault/` holds the thinking: foundations, decisions, projects, QA, templates, views. Documentation only, ever.
- `loom/` holds Telar itself: the workshop defined as code.
- The name: *telar* is Spanish for loom. The vault is where the loom is designed; `loom/` is the loom. The metaphor carries the design: on a loom the warp threads are held under tension and the weft is woven through them. In Telar, checks, verification and rules are the warp and agents carry the weft.

## Consequences

- Every artifact in `loom/` traces back to a project in `vault/projects/`.
- Renaming is cheap while the loom has no code. After that, a rename needs a new ADR.

## Alternatives considered

- **`core`.** Generic; says nothing about what it holds.
- **`warp`.** The best fit for "the rules everything is woven through", but it collides with Warp, a company whose talks are among Telar's main sources.
- **`factory`.** Contradicts the workshop-first approach.
- **`engine` or `harness`.** Telar is not a harness; it uses existing ones.
