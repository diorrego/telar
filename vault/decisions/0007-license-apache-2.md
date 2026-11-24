---
id: ADR-0007
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0007: License: Apache-2.0

## Context

Telar is a public kit meant to be adopted by other people and companies ([research](../foundations/research.md), section 4, decision 11). The kit design written during the research (2026-11-22) proposed Apache-2.0 for the whole repository. Diego asked to adopt the proposed license now.

## Decision

The whole repository (documentation now; code and schemas later) is licensed under the **Apache License 2.0**. The canonical text is in `LICENSE` at the repository root.

Why Apache-2.0:

- **Explicit patent grant, with a termination clause.** It matters to a company evaluating adoption, and MIT does not include one.
- **Permissive.** Anyone can use, modify and embed it in their own products. The goal is adoption.
- **Compatible** with including the kit in MIT or Apache projects.
- **No trademark grant.** The name Telar stays with its maintainer even though the code is free.

## Consequences

- No `NOTICE` file for now. One is added if third-party notices or an attribution line become necessary.
- If a company contributes its own code, confirm who holds the copyright before publishing it.
- The research also proposed accepting contributions under the **Developer Certificate of Origin** (a `Signed-off-by` line on each commit, checked automatically) instead of a CLA, with a single maintainer documented in a `GOVERNANCE.md`. That is not adopted yet; it gets its own ADR when the repository opens to contributions.
- This is not legal advice.

## Alternatives considered

- **MIT.** Simpler, but no explicit patent grant.
- **AGPL.** Network copyleft discourages exactly the companies Telar wants as adopters.
- **BSL or other source-available licenses.** Same problem, and not open source.
