# CLAUDE.md, core/

The core is Telar itself: the workshop defined as code. `README.md` here describes the layout; each folder's `README.md` is the contract for what it holds.

## Current phase

Documentation only ([ADR 0005](../vault/decisions/0005-documentation-before-code.md)). The only files allowed here are this file, `AGENTS.md`, and the `README.md` contract of each folder. Do not add code, configuration, schemas or example files until a plan in `../vault/projects/` is `active` and its current phase says to.

## Hard rules

- **Traceability.** Every artifact in the core traces to a project iteration (`vault/projects/{project}/vN/`) and, when it encodes a correction or fixes a finding, to its ID (`C-0001`, `F-0001`). The commit message cites it.
- **Pyramid order.** When choosing where something goes, prefer `checks/` over `verify/` over `skills/` over `rules/`. A new rule must say why no check, verification or skill could express it.
- **Thin and replaceable.** Nothing here assumes one harness or one model unless the folder contract says so. Do not build what a better model will make unnecessary; when a model makes a core piece unnecessary, remove it and record that in the plan log.
- **Few dependencies, open formats.** Prefer plain files (Markdown, YAML, JSON) and standard tools. A new dependency needs a written reason in the plan.
- **Error messages teach.** A failing check says what is wrong and how to fix the root cause, so an agent reading it fixes the cause instead of patching around it.
- **No escape hatches in prose.** Do not add comments or docs that justify not doing the right thing. A real exception is encoded (an explicit allowlist in the check), not explained.
- **Contracts first.** Changing what a folder holds means updating its `README.md` in the same commit, and an ADR if it changes the layout.
- **Stage order.** Stage 2 folders (`agents/`, `workflows/`, `evals/`) stay empty until the workshop stage meets its exit criteria in `../vault/foundations/vision.md` ([ADR 0006](../vault/decisions/0006-workshop-before-factory.md)).
- **Telar is its own first target.** Whatever the core provides must be usable on this repository.
