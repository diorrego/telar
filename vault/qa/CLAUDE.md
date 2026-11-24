# CLAUDE.md, vault/qa/

QA for Telar has two inputs, kept apart because they are fixed differently, plus session notes.

| Folder | What goes there | ID and file name | Fixed by |
|---|---|---|---|
| `findings/` | Defects: something in the loom, in the vault, or in software built with Telar does not behave as specified | `F-0001-short-title.md` | A direct fix or a project plan |
| `corrections/` | A human had to push back on an agent: wrong approach, ignored rule, slop, repeated instruction, false "done" | `C-0001-short-title.md` | Encoding it in the workshop so it cannot recur |
| `sessions/` | Notes of one exploratory QA session | `YYYY-MM-DD-topic.md` | |

IDs are sequential per folder, zero padded to four digits, never reused.

## Findings

From `../templates/finding.md`. A finding must be **self-contained and actionable**:

- **Actual, expected, change.** What happens, what should happen, and what must change. Without the third part it is a complaint, not a finding.
- **Reproduction.** Exact steps, commit, and harness and model where relevant.
- **Evidence.** Output, screenshot, trace or `file:line`, linked from the note and stored next to it if it is a file.
- **Area.** One of `checks`, `verify`, `skills`, `rules`, `agents`, `workflows`, `evals`, `vault`, `docs`.

`status: open | triaged | fixing | fixed | verified | wont-fix`. `fixed` means the change is merged; `verified` means it was re-tested where it failed. Only `verified` or `wont-fix` (with a reason) closes a finding.

## Corrections: the corrections ledger

Corrections are the most valuable data Telar produces: each one says the workshop allowed an agent to do the wrong thing. From `../templates/correction.md`.

Log a correction when a human rejects an output, redirects an approach, repeats an instruction already given, or fixes something an agent claimed was done. Log it in the same session, in the human's words where possible.

Then propose how to encode it, at the **lowest layer of the trust pyramid** that can prevent it ([principle 4](../foundations/principles.md)):

| Layer | Encode as | Example |
|---|---|---|
| 1. Architecture | Change the code or API so the mistake cannot be expressed | Ban a construct that needs nuance to use well; split directories so a bad import cannot exist |
| 2. Check | A deterministic lint rule, type, boundary or test, whose error message explains how to fix the root cause | A lint rule that blocks timers used as quick fixes |
| 3. Verification | A runtime, property-based or formal verification that catches it | A feature map driven run that proves the sidebar still works |
| 4. Skill | A reusable procedure with its own CLI | A skill that always runs the app before claiming a UI change works |
| 5. Rule | A line in a `CLAUDE.md` or in `loom/rules/` | Only when the mistake needs judgment and no check can express it |

`status: logged | encoded | dismissed`.

- `encoded` requires `encoded_as` (the layer) and `encoded_in` (the commit or plan that did it).
- `dismissed` requires a reason in the log (one-off, the human was mistaken, superseded).
- While Telar has no code ([ADR 0005](../decisions/0005-documentation-before-code.md)), a correction stays `logged` with the proposed layer written in its "Encoding" section. Logged corrections are the backlog of the first loom projects.

**Recurrence.** If a correction repeats an earlier one, do not open a new file: increment `occurrences` in the original and add a dated line to its log. A correction with 3 or more occurrences that is still `logged` is a candidate for a project plan (born `proposed`, with `origin: C-NNNN`).

## Sessions

One note per exploratory QA session, from `../templates/session.md`: date, scope, setup (commit, harness, model), what was tried, and the IDs of the findings and corrections it raised. The session note links; the findings and corrections hold the detail.
