---
id: F-0001
status: verified
severity: low
area: vault
found: 2026-11-26
found_in: 1fed170
fixed_by: the commit that adds this note
updated: 2026-11-26
---

# F-0001: The board lists superseded plans as waiting for a go

## Actual

`vault/views/board.md`, "Plans waiting for a go" (the Dataview query and the grep at the top), lists every `proposed` plan, including iterations that another iteration superseded. Here it listed `core-definition` v1, which is `proposed` with `superseded_by: ../v2/PLAN.md`.

## Expected

A superseded iteration keeps the status it reached (`vault/projects/CLAUDE.md`) and does not wait for a go. "Active plans" already excludes superseded iterations with `!superseded_by`; "Plans waiting for a go" should too.

## Change

Add `AND !superseded_by` to the Dataview query, and filter the grep with `xargs grep -L "^superseded_by: *[^[:space:]]"`.

## Reproduction

1. At `1fed170`, from `vault/`: `grep -l "^status: proposed" projects/*/*/PLAN.md`.
2. It prints `projects/core-definition/v1/PLAN.md` beside v2.

## Evidence

Found in the first installation by a handoff test: a fresh agent session, reading only that repository, reported that its board listed a superseded plan as waiting. The installation's board is a copy of this one.

## Log

- 2026-11-26: Logged, fixed and verified: the fixed grep prints only `projects/core-definition/v2/PLAN.md`.
