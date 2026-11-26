# Vision

## In one line

Telar is a method, and the open framework that implements it, with which an agent-assisted software workshop models its own rules ([ADR 0008](../decisions/0008-telar-is-a-method-and-framework.md)).

## What "modeling its own rules" means

Every workshop already has rules: who can start work, what must be approved and by whom, what an agent may touch, how a change is verified, what counts as done. Most of them live in people's heads, in chat history or in a long instruction file that agents follow about 60% of the time ([research](research.md), R13).

Modeling a rule means three things:

1. **Written down**, in a versioned place, with the decision or correction that created it.
2. **Placed at the layer that enforces it**: the architecture if possible, then a deterministic check, then a verification, then a skill, and prose only when judgment is unavoidable (principle 3).
3. **Measured**: the workshop can tell whether the rule works, for example whether the correction that created it stops recurring.

Every time a person has to correct an agent, a rule is missing. That correction is Telar's raw material.

## The problem

- Coding agents keep getting better under the same harness. They run for many minutes per task, and the volume of code they produce keeps growing.
- Human attention does not grow. Starting a project got easy; maintaining one did not. The human sets the pace.
- Agents are rewarded for finishing, not for fit. Without a strong environment, volume turns into slop, and agents copy the slop they find.
- Automating a loop that produces slop produces more slop, at a higher token bill.

## The thesis: rules, then the workshop, then the factory

The order Diego took from the research (2026-11-24): first rules, contracts and tests; then the workshop, where people review inside the flow and push back; then the factory, where agents triage, specify, build, review and verify, everything is measured, and the factory proposes how to avoid its own repeated mistakes. The factory lives in an environment isolated from people's machines and works where people already work.

A factory amplifies whatever its inner loop produces, so the order matters. What the factory learns returns to the workshop as new rules.

## Installations

An installation is a workshop that uses Telar to model its rules.

| Installation | Role | Status |
|---|---|---|
| wondeya | First installation: a new product started from zero, built with Telar from its first commit. Telar keeps abstracting what is generic out of what it needs ([ADR 0010](../decisions/0010-first-installation-is-a-new-project.md)) | Current, and the only one for now |
| woku | An existing product with its own history: the case of a running workshop adopting Telar | Paused ([ADR 0010](../decisions/0010-first-installation-is-a-new-project.md)) |
| Telar itself | Telar developed with Telar | Later. Meanwhile this repository uses the method by hand: plans with a go, corrections ledger, decisions |
| A public example project | Proof that any workshop can adopt Telar from the README alone | Later |

An installation's rules, repositories and data stay in its private repositories. This repository holds only what is generic.

## What Telar is

- **A method:** model rules from corrections, encode them at the lowest layer, keep humans at the decisions that matter, review evidence instead of diffs, measure against the way the team works today.
- **A framework:** the part every installation shares (`core/`). Its structure is being defined in the [`core-definition`](../projects/core-definition/v1/PLAN.md) project, before any of it is built.

## What Telar is not

- Not a coding agent or a harness. It uses existing ones (Claude Code, Codex, OpenCode and others) and stays thin enough to switch between them.
- Not a prompt collection. Prose is the last layer, not the first.
- Not an "AI teammate" or a swarm of personal agents.
- Not a hosted platform. Infrastructure is an adoption barrier; the first version needs only a forge, an agent CLI and Markdown ([research](research.md), section 4).

## How success is measured

Per accepted change, against the way the team works today (a person with an interactive agent), on the same tasks and criteria, from timestamps rather than impressions. The precise definitions are part of `core-definition`.

| Metric | What it tells | Source |
|---|---|---|
| Human minutes per accepted change (clarify, review, intervene) | What a change costs in attention | Critical review; Lloyd |
| Corrections at 14 and 30 days, and reverts | Whether accepted changes were really good | Critical review; Tan |
| Corrections per session, and their recurrence | Whether the workshop is learning, and whether its rules work | Ronacher; Telar |
| Cost per accepted change, including failed attempts | Whether it is efficient | Critical review; Lloyd |
| Cycle time and time waiting for a person | Where the time goes | Conceptual framework; Lloyd |
| Share of changes accepted on evidence rather than a line by line read | Whether review is shrinking to artifacts | Tan; Lloyd |

## Open questions

The full list is in the [`core-definition` diagnosis](../projects/core-definition/v1/DIAGNOSIS.md). The ones that shape the vision:

- Whether "done" means merged or verified in production, for the first version.
- Whether research is its own stage, with its own decision, from the first version.
- When the isolated, always-available environment arrives, and with what entry criteria.
- How context is managed: a fresh session per stage, a compaction threshold, or both.
