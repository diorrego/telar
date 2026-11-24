---
id: ADR-0006
status: proposed
date: 2026-11-24
decided_by: proposed by claude; the workshop framing is diego's
superseded_by:
---

# ADR-0006: Workshop before factory: three stages

## Context

Diego framed Telar as an agentic software *workshop*. The research points the same way:

- Ronacher argues for building the workshop (the atelier) before the factory, because human attention, not agent capability, is the limit.
- Tan shows that trust foundations (deterministic checks, verification) are the prerequisite to automation: "if your inner coding loop produces slop, automating that loop just produces more slop".
- Lloyd defines the factory as a code-defined closed loop that measures and improves agents, but calls it overkill for an individual and valuable from about 10 engineers.

See [`foundations/research.md`](../foundations/research.md).

## Decision

Telar is built in three stages. Each starts only when the previous one meets its exit criteria, defined in [`foundations/vision.md`](../foundations/vision.md).

1. **Workshop.** The inner loop.
2. **Loop.** The outer loop.
3. **Factory.** Scale.

> **Note, 2026-11-24.** The mapping of these stages to `core/` folders was withdrawn by [ADR 0008](0008-telar-is-a-method-and-framework.md). The sequence itself is an input to the maturity phase of the [`core-definition`](../projects/core-definition/v1/PLAN.md) project, together with the order Diego stated on 2026-11-24 (rules, contracts and tests; then the workshop; then the factory). That phase proposes whether this ADR is accepted as revised or superseded.

## Consequences

- No orchestration, cloud sandboxes, benchmarks or model routing until the workshop stage has exit evidence.
- The exit criteria are themselves proposals and get refined by the first projects.

## Alternatives considered

- **Factory first.** Build the full loop now and improve it with scores. Rejected in this proposal: it would amplify an inner loop that has not earned trust, and it is oversized for one engineer.
- **No stages.** Build whatever is most useful next. Simpler, but it loses the rule that automation waits for trust.
