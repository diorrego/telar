# CLAUDE.md, core/

The framework part of Telar: what every installation shares. It is code, and its structure is not defined yet.

## Hard rule

This folder holds only `CLAUDE.md`, its `AGENTS.md` symlink and `README.md` until two things are true: the vault project [`core-definition`](../vault/projects/core-definition/v1/PLAN.md) has ended in an accepted ADR that defines the structure of `core/`, and a later plan is `active` and its current phase calls for building it ([ADR 0005](../vault/decisions/0005-documentation-before-code.md), [ADR 0008](../vault/decisions/0008-telar-is-a-method-and-framework.md)).

Do not add folders, contracts, schemas, examples or placeholders here to "prepare" for that structure. A guessed structure looks like a design and preempts the project that must define it (correction [C-0002](../vault/qa/corrections/C-0002-shallow-proposal-without-evidence.md)).

## When the structure exists

These rules will apply, and the structure ADR may refine them:

- **Generic only.** Nothing specific to an installation (woku or any other) lives here. Project rules, values and content live in the project's repositories.
- **Traceability.** Every artifact traces to a vault project iteration and, when it encodes a correction or fixes a finding, to its ID. The commit message cites it.
- **Lowest layer first.** Prefer a check over a verification over a skill over a prose rule (principle 4).
- **Thin and replaceable.** No assumption of one harness or model unless the structure ADR says so. Few dependencies, open formats.
- **Error messages teach.** A failing check says what is wrong and how to fix the root cause.
