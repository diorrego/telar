---
id: C-0006
status: encoded
date: 2026-11-26
by: diego
harness: claude-code
model: claude-opus-5-5
occurrences: 1
encoded_as: rule
encoded_in: ADR-0011; "Show decisions on a review page" in the root CLAUDE.md; "Review pages" and "Decisions" in vault/CLAUDE.md; plan state rules and stage 6 in vault/projects/CLAUDE.md; templates/review.md
updated: 2026-11-26
---

# C-0006: Decisions asked for in text, without a visual page

## What the agent did

Asked Diego to decide from Markdown files and tables in chat: the go for core-definition v1 and v2, the first installation's plans, and its eight ADRs. A visual page was produced only when he asked for one ("make me an artifact in Spanish to read decisions 1 to 8").

## The correction

Diego: "I see a problem in Telar here: create an artifact when Claude Code is used, or, if another agent such as Codex or OpenCode is used, create an HTML file that diagrams and shows visually the designs, decisions and models it generates, to approve decisions before implementing. This will speed up decision-making and the understanding of the research and the later design." (Translated from Spanish.)

It repeats an instruction from the research (R16, 2026-11-24): "inside the flow, you have to include your review; that is what HTML pages or Claude artifacts are for, they speed up explanations through diagrams."

## Why the workshop allowed it

- R16 was recorded only as a candidate non-negotiable (N-26) inside a proposed plan, not as a working rule. The method's owner review stage asked for "a one-minute summary" without saying what form it takes.
- No template existed for a review page, and nothing said where it lives or how it is delivered when the harness has no artifacts.
- Markdown in the repository is an agent's natural output, so a request for a decision looked complete without a page.

## Encoding

- **Layer 5, rule.** Root `CLAUDE.md` ("Show decisions on a review page"), `vault/CLAUDE.md` ("Review pages", "Decisions"), `vault/projects/CLAUDE.md` (plan state rules, stage 6). The first installation's instructions get the same rule.
- **Layer 4, procedure.** [`templates/review.md`](../../templates/review.md): what a page contains, where it is saved, and how each harness delivers it.
- **Candidate layer 2, check (once code is allowed).** A plan or an ADR in `proposed` without a linked review page fails. Recorded in core-definition v2.

## Log

- 2026-11-26: Logged (occurrence 1, repeating R16). Encoded as rules and a template; [ADR 0011](../../decisions/0011-review-pages-before-decisions.md) proposed for the details. First pages: Telar's own for this change, and the first installation's eight ADRs.
- 2026-11-26: Diego accepted ADR 0011 ("está bien"), with pages in the language the user indicates.
