# CLAUDE.md, vault/projects/

Every initiative to build or change Telar starts here: diagnosed, planned, tracked and closed. One folder per project, each iteration self-contained in `v1/`, `v2/`...

## Hard rule: one folder per iteration

```
projects/{project}/v1/   first complete iteration
projects/{project}/v2/   new approach: new diagnosis, new scope
```

- Project folder names are short kebab-case nouns (`corrections-ledger`, `verification-artifacts`).
- **Never** leave files loose in the project root: everything lives inside its `vN/`.
- Open `vN+1/` when the project is approached again (new diagnosis, different scope, rework of what shipped). The new diagnosis may cite the previous version; its files never mix with it.

## Contents of an iteration

| File | What it is |
|---|---|
| `DIAGNOSIS.md` | The current state before proposing anything, with an inspection record (date, repository, branch, commit, method) and an **evidence inventory**. Evidence as `file:line`, URL, or a path in `vault/evidence/`. From `../templates/diagnosis.md`. |
| `PLAN.md` | Editable checklist by phases, with frontmatter state and a dated log. Ticked **during** the work, not at the end. The source of truth for progress. From `../templates/plan.md`. |
| `CLOSEOUT.md` | What was learned, which corrections were encoded, what moves to the next iteration. From `../templates/closeout.md`. |
| Supporting files | Lowercase names, free form: `evidence.md`, `review.md`, `notes-{topic}.md`, verification artifacts. |

## Plan state

Every `vN/PLAN.md` starts with this frontmatter. The state lives here, not in folders; `../views/board.md` filters it.

```yaml
---
status: proposed      # proposed | active | shipped | dropped
origin: diego         # diego | claude | agent | F-0001 | C-0001 (the finding or correction that triggered it)
updated: 2026-11-24   # date of the last status change
superseded_by:        # optional: ../vN/PLAN.md when another iteration takes over its pending work
---
```

| Status | Meaning | Who sets it |
|---|---|---|
| `proposed` | Plan written, waiting for Diego's go. May have open decisions | Whoever writes the plan |
| `active` | Diego said go. Covers implementation, verification, review and release | The agent, logging the date and Diego's words |
| `shipped` | What the plan promised works where it is meant to run and was verified there (stage 8) | The agent, with the evidence |
| `dropped` | Rejected, paused without a date, or no longer meaningful. Reason in the log | Diego, or the agent at Diego's request |

Rules:

- **A plan is presented with its review page.** The diagnosis and the plan reach Diego as a visual page, with the open decisions drawn and the recommendation for each ([ADR 0011](../decisions/0011-review-pages-before-decisions.md)). The log records the page's path.
- **Writing a plan ends at `proposed`.** No agent implements a `proposed` plan. It moves to `active` only when Diego explicitly asks for that plan ("go with X", "implement it"). Answering an open decision is not a go.
- Plans created by agents (for example from a recurring correction) are born `proposed` with the triggering ID as `origin`, and never trigger implementation by themselves.
- A status change updates `updated` and the log in the same commit.
- A new iteration that absorbs pending work of an old one sets `superseded_by` in the old one; the old one keeps the status it reached.

## End to end execution

An iteration exists so that something works in a real workshop, not to leave documents or code behind. Each stage has a reviewable output; without it the stage is not done.

| # | Stage | Reviewable output |
|---|---|---|
| 1 | Goal | Observable scenarios: who does what and what they see (for example: "Diego rejects an agent's use of a banned API; in the next session a check blocks it before review"). No scenarios, no design. |
| 2 | Diagnosis | `DIAGNOSIS.md` against the real state: the core, the target repository, harness and model capabilities, the research. |
| 3 | Plan | `PLAN.md` in vertical phases: each phase leaves one scenario working end to end, not a loose layer. Per scenario: how it is verified, what evidence remains, who does what. Open decisions are asked before building. |
| 4 | Implementation | Only once code is allowed ([ADR 0005](../decisions/0005-documentation-before-code.md)). Tests first, one commit per phase, plan and log updated before each commit. |
| 5 | Local verification | Each scenario run for real. Evidence (verification artifacts) saved in the iteration folder. What cannot be verified locally is said in writing. |
| 6 | Owner review | Diego gets a review page (ADR 0011) with the evidence and a one-minute summary, and tests what involves his judgment. Iterate until his OK. |
| 7 | Release | Merged through a pull request with Diego's OK, and versioned. |
| 8 | Verification in use | Each scenario checked in a real workshop (Telar's own repository or a real product repository). Only then is the plan `shipped`. |
| 9 | Closeout | `CLOSEOUT.md`: what was learned, which corrections became checks, what moves to the next iteration. Nothing is left half-done without a note. |

Reportable states, in this order: **planned**, **implemented**, **verified locally**, **approved by Diego**, **verified in use**. "Done" is only said of the last one. A status report says, per scenario, which state it is in and what is missing. A green test suite does not move anything past "implemented".

## Project index

Keep this table updated when a project is created or an iteration changes state. It is descriptive; the frontmatter of each `PLAN.md` is the source of truth.

| Project | What it is | State |
|---|---|---|
| [`core-definition`](core-definition/v2/PLAN.md) | Define what the core must contain: the non-negotiables from research to production, each classified as Telar invariant, Telar mechanism with project values, project baseline or project only; the first installation (wondeya) as the test case | v2 `proposed` 2026-11-26 (retargets v1 to the new first installation, ADR 0010); v1 superseded |

## Rules when working here

- Before touching a project, read its latest `vN/PLAN.md`.
- **A diagnosis starts with an evidence inventory**: every relevant item in `vault/evidence/` (and any other source), each marked read in full, partially, or not read. Proposals about structure or scope cite the evidence they rest on ([C-0002](../qa/corrections/C-0002-shallow-proposal-without-evidence.md)).
- Diagnoses are written against reality: cite the repository, branch and commit inspected.
- Plans are living checklists: tick phases when completed and update the log in the same commit.
- A plan states what is out of scope. Deciding what not to build is part of the plan.
