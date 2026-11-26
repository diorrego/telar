# Diagnosis: core-definition v2

## Inspection record

| Field | Value |
|---|---|
| Date | 2026-11-26 |
| Repository | telar |
| Branch | main |
| Commit | 6b97405 (before this iteration) |
| Harness and model | Claude Code, claude-opus-5-5 |
| Method | Read ADR 0010 (accepted today) and corrections C-0003 to C-0005 in full; re-read the parts of the [v1 diagnosis](../v1/DIAGNOSIS.md) and [v1 plan](../v1/PLAN.md) that name woku (found by search); took generic facts about the first installation from its private plan, which is not cited here ([ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md), decision 2) |

## Evidence inventory

Everything in the v1 inventory (E1 to E12) and everything v1 established (R1 to R19, C1 to C12, the levels, N-01 to N-44, B-1 to B-11, G1 onward) stands unless listed below.

| ID | Evidence | Date | Read | Contributes |
|---|---|---|---|---|
| V1 | [v1 diagnosis](../v1/DIAGNOSIS.md) and [v1 plan](../v1/PLAN.md) | 2026-11-24 | Partially re-read: every line that names woku | Which scenarios, decisions and items depend on the installation being woku |
| A10 | [ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md) | 2026-11-26 | In full | The first installation is a new product started from zero; woku is paused; the measurement question; the baseline tested by building; work in a local repository until its first MVP |
| K3 | [C-0003](../../../qa/corrections/C-0003-research-delegated-to-subagents.md) | 2026-11-26 | In full | Who reads the evidence; encoded as a rule, with a lower layer proposed |
| K4 | [C-0004](../../../qa/corrections/C-0004-plan-without-a-stated-deliverable.md) | 2026-11-26 | In full | A product plan without a stated deliverable; template change proposed |
| K5 | [C-0005](../../../qa/corrections/C-0005-product-proposed-through-its-risks.md) | 2026-11-26 | In full | A workshop non-negotiable applied to a product's behavior; diagnosis template and catalog scope proposed |
| I1 | The first installation's private plan (not cited) | 2026-11-26 | In full | Generic facts only: one engineer; a local repository with no hosted forge until its first MVP; code starts in its third phase; corrections logged from its first phase; a pilot with real users at the end |

## Question

What changes in `core-definition` now that its test case is a new product with no history, built by one engineer in a local repository, instead of an existing product with CI, habits and a team?

## Current state

1. **The installation changed.** ADR 0010 was accepted on 2026-11-26: the first installation is a new product started from zero; woku is paused. v1's S1 walks "a woku work item", S3 applies the baseline to woku, S4 models woku corrections, and D7 asks where woku's private analysis lives ([v1 plan](../v1/PLAN.md), lines 19, 21, 22 and 37).
2. **There is no history to measure against.** Telar measures "against the way the team works today" ([vision](../../../foundations/vision.md)) and the critical review measures version zero "against the current mode (person + agent) over 10 to 15 real work items". A new product has no current mode. ADR 0010 proposes a candidate: record human minutes, corrections and cycle time from the first work item, and alternate items done through Telar's line by hand with items done by a person with an interactive agent.
3. **There is no forge yet.** The installation works in a local repository until its first MVP. Of the baseline, B-1 (CI workflows), B-2 (branch protection with required review) and B-3 (CODEOWNERS) assume a hosted forge; B-8 (a verifier identity separate from the builder) does not, but has no place to be enforced without one. A local hook can run B-1's checks on every commit; nothing local replaces required review.
4. **One person builds and approves.** R4 and G7 named the one-person case; it is now the only case. N-03 already treats the one-person case as "two separate moments".
5. **Research is part of the method.** Asked whether the first installation does research before building, Diego said research "is always part of Telar's framework and method" (2026-11-26, translated). v1's D3 asks whether research is its own stage with output and gate; the statement supports research as a fixed part of the line, and does not by itself settle the stage question.
6. **A non-negotiable was applied outside its scope.** In the first installation's first plan, the agent used N-01 ("every transition with effects is decided by code or an authenticated person") to argue that the product should ask its users before acting; Diego rejected that framing (K5). The catalog does not say that its rows govern how software is built in the workshop and not what the product does for its users.
7. **The first corrections exist.** C-0001 to C-0005 are in this repository. C-0003 is encoded as a rule; C-0004 and C-0005 propose template changes and a catalog scope statement. The installation logs its own corrections from its first phase.

## Problems

| # | Problem | Evidence | Impact |
|---|---|---|---|
| P1 | S1, S3, S4 and D7 name woku | V1 | v1 cannot be run as written |
| P2 | Measurement assumes a current mode | Current state 2, A10 | S6 below: a protocol for a project with no history |
| P3 | Forge-dependent baseline items | Current state 3, I1 | The baseline must say, per item, its local equivalent or that it waits for a forge |
| P4 | The one-person case is the only case | Current state 4 | Approval rules are tested in their hardest form first |
| P5 | Catalog scope is unstated | K5 | A scope statement in the catalog; C-0005 is its first evidence |
| P6 | Templates lack "the request" and "deliverable" sections | K4, K5 | Candidates for the formats inventory (phase 5) |

## Constraints

- [ADR 0005](../../../decisions/0005-documentation-before-code.md): documentation only.
- [ADR 0008](../../../decisions/0008-telar-is-a-method-and-framework.md), decisions 1, 4 and 5, and [ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md): the installation's internal details stay in its private repository; this repository says only that it is a new product started from zero.
- Public repository.

## Options

| Topic | Options | Note |
|---|---|---|
| Measurement without history | (a) record per work item from the first one (human minutes, corrections, cycle time) and compare later items with earlier ones; (b) alternate items through Telar's line by hand with items done by a person with an interactive agent (ADR 0010's candidate); (c) both | (b) needs enough comparable items; the installation's phases give them only after its code starts |
| Baseline test | Audit (v1's S3 for woku) or build (ADR 0010) | ADR 0010 chose build: record the order in which each item enters and what it cost |

## Unknowns

| # | Unknown | How it gets known |
|---|---|---|
| U1 | Which of the installation's work items walk through the lifecycle model (S1) | Diego, when phase 1 starts |
| U2 | Whether a local equivalent exists for each forge-dependent baseline item | Phase 3, as the installation builds its repository |
| U3 | v1's U1 to U4 (about woku) | Paused with woku |
