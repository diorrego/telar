---
id: ADR-0008
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by: "0010-first-installation-is-a-new-project.md (decision 2, and decision 3 for the first installation)"
---

# ADR-0008: Telar is a method and framework; woku first; core defined by a project

## Context

The first version of the vision described Telar as "an agentic software workshop" for a small team, built with itself. The research conversations had already settled that Telar is a public kit others adopt, with woku as its first installation ([evidence](../evidence/README.md)). Asked to research the definition and propose one, the agent found precedents for "method plus framework" (Scrum as a purposefully incomplete framework), for extracting a framework from a first application (Rails from Basecamp; the "three examples" pattern), and for self-hosting and its risks. Diego answered the resulting questions on 2026-11-24.

## Decision

1. **Definition.** Telar is a method, and the open framework that implements it, with which an agent-assisted software workshop models its own rules: each rule the workshop depends on (who starts work, what must be approved, what an agent may touch, what counts as done) is written down, placed at the layer that enforces it, and measured.
2. **Woku first, and only woku for now.** Woku is the first and, for now, only installation. Telar is built by serving woku as its use case, and keeps abstracting what is generic out of what woku needs.
3. **Woku is named.** This public repository names woku as the first installation. Woku's internal details (repositories, paths, people, data, domain rules) stay in woku's private repositories.
4. **Telar developed with Telar comes later.** This repository uses the method by hand (plans, corrections, decisions), but it is not an installation yet. A public example project is also deferred.
5. **Core is defined before it is built.** `core/` is code. Its structure is defined first in a vault project, [`core-definition`](../projects/core-definition/v1/PLAN.md). The seven subfolders created in the first commit are withdrawn: they were an unreviewed hypothesis. Until a structure ADR is accepted, `core/` holds only its `CLAUDE.md`, `AGENTS.md` and a `README.md` placeholder.

## Consequences

- The vision, glossary, README and root instructions describe Telar with this definition.
- [ADR 0006](0006-workshop-before-factory.md) loses its folder mapping; its stage sequence becomes an input to the maturity phase of `core-definition`.
- What Telar provides and what each project provides are separated by level (Telar invariant, Telar mechanism with project values, project baseline, project only), as proposed in the `core-definition` diagnosis.

## Alternatives considered

- **A workshop for one team, built with itself first.** The first version of the vision. Rejected: it ignored the research decisions, and Diego wants woku served first.
- **Three installations now (woku, Telar itself, a public example).** Proposed by the agent from the "three examples" pattern. Diego chose only woku for now.
- **Add `core/method/` and `core/formats/` now.** Rejected by Diego: core is code; define it in a project first.
