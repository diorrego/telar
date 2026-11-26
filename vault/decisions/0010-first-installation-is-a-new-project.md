---
id: ADR-0010
status: accepted
date: 2026-11-26
decided_by: diego (accepted 2026-11-26); written by claude
superseded_by:
---

# ADR-0010: The first installation is a new project, wondeya; woku waits

## Context

[ADR 0008](0008-telar-is-a-method-and-framework.md) made woku the first and only installation. On 2026-11-26 Diego changed Telar's first laboratory: instead of woku, an existing product with maintenance, the first installation is a new project that starts from zero, named wondeya, kept in a private repository. Telar stays public. In his words (translated): "I want to create with Telar a new project, with no maintenance, since it starts from zero, not like woku."

The two cases test different things:

- An existing product tests whether a running workshop, with legacy code, CI and habits, can adopt Telar. It is the case most workshops have.
- A new product tests whether a workshop can be built with Telar from its first commit: the project baseline in place before any code, rules before features, research before requirements (R2 in the [`core-definition` diagnosis](../projects/core-definition/v1/DIAGNOSIS.md)), and the one-person approval case (R4, G7), since one engineer builds it.

A new product also has no history, and some of Telar's measurement assumes one: version zero is "measured against the current mode (person + agent) over 10 to 15 real work items" ([critical review](../evidence/documents/2026-11-22-critical-review-and-version-zero.md)), and success is measured "against the way the team works today" ([vision](../foundations/vision.md)).

## Decision

1. **Wondeya is Telar's first installation.** Woku is no longer the first; Diego paused it as an installation (2026-11-26).
2. **Wondeya is private.** Its repositories, vault, users, data and domain rules stay in its private repository. This repository names wondeya as the first installation and says it is a new product started from zero; nothing more (confirmed by Diego on 2026-11-26).
3. **The method is applied by hand from wondeya's first commit:** vault, plans with a go, corrections ledger, decisions, evidence inventory. Wondeya's corrections and findings become the test data of `core-definition`, as woku's were meant to be; what they teach about Telar is written here as Telar findings, in Telar's words.
4. **`core-definition` keeps its goal.** Its woku-specific scenarios (S1, a woku work item; S3, the baseline test; S4, woku corrections) are retargeted to wondeya in a new iteration, [v2](../projects/core-definition/v2/PLAN.md). v1 keeps the status it reached.

## Consequences

- Supersedes decision 2 of ADR 0008 ("woku first, and only woku for now") and, for the first installation, decision 3. Decisions 1, 4 and 5 of ADR 0008 stand.
- On acceptance, in the same commit: the installations table in the vision, `README.md`, root `CLAUDE.md`, the glossary entry "Installation", and `core-definition` v2.
- A new question for `core-definition`: what "the current way of working" means in a project with no history. A candidate: from the first work item, record human minutes, corrections and cycle time from timestamps, and alternate items done through Telar's line by hand with items done by a person with an interactive agent.
- The project baseline (B-1 to B-11) is tested by building it rather than auditing it: the useful output is the order in which a new repository adds each item and what each one cost.
- Wondeya works in a local repository, with no hosted forge, until its first MVP (Diego, 2026-11-26). Baseline items that assume a forge (hosted CI, branch protection, required review) are tested later or through local equivalents, and the baseline has to say which items have them.
- The legacy case (woku) stays untested until a later installation; conclusions drawn from wondeya about adoption by an existing workshop are marked as such.

## Alternatives considered

- **Keep woku first ([ADR 0008](0008-telar-is-a-method-and-framework.md)).** Changed by Diego on 2026-11-26.
- **Woku and wondeya in parallel.** Two installations double the overhead for one maintainer; ADR 0008 already chose one at a time.
- **Telar developed with Telar first.** Deferred by ADR 0008.
