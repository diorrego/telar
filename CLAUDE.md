# CLAUDE.md, Telar

Instructions for coding agents working in this repository. `AGENTS.md` is a symlink to this file, so harnesses that read either one get the same rules. Edit `CLAUDE.md` only. Human onboarding is in `README.md`.

## What Telar is

Telar is an agentic software workshop: the checks, verification, skills, rules, agent definitions, workflows and evals with which a small team builds high-quality software with coding agents. It is built workshop first, factory later ([ADR 0006](vault/decisions/0006-workshop-before-factory.md)).

`vault/foundations/vision.md` and `vault/foundations/principles.md` are the product definition. Read them before proposing anything.

## Current phase: documentation only

There is **no code** in this repository, and none is written until a plan in `vault/projects/` has `status: active` and its current phase calls for code ([ADR 0005](vault/decisions/0005-documentation-before-code.md)). Until then the work is research synthesis, decisions, diagnoses and plans, and the folder contracts in `loom/*/README.md`. If a task seems to need code, write or update the plan instead and stop there.

## Repository map

| Path | What it is | Rules |
|---|---|---|
| `vault/` | The workshop notebook: foundations, decisions, projects, QA, templates, views | `vault/CLAUDE.md` |
| `vault/projects/` | One folder per initiative, each iteration self-contained in `v1/`, `v2/`... | `vault/projects/CLAUDE.md` |
| `vault/qa/` | Findings (defects), corrections (times a human had to push back on an agent), exploratory sessions | `vault/qa/CLAUDE.md` |
| `loom/` | Telar itself: the workshop defined as code. Folder contracts only, for now | `loom/CLAUDE.md` |

Read a folder's `CLAUDE.md` before working in it.

## Hard rules

- **English only.** Every file, note, ID, commit message and branch name. Diego may talk to you in Spanish; what lands in the repository is English.
- **No em dashes.** Use commas, colons, parentheses or periods.
- **Plans are born `proposed`.** Nothing in a plan is implemented until Diego explicitly says go for that plan. Answering an open question is not a go. See `vault/projects/CLAUDE.md`.
- **The research is read-only input.** The folder that contains this repository (`../`) is a separate research repository. Reference its sources by public URL; never copy transcripts here and never edit files there.
- **Decisions are recorded.** A choice that constrains future work (structure, naming, tooling, scope) gets an ADR in `vault/decisions/`. Never silently reverse an accepted ADR: write a new one that supersedes it.
- **Document as you go.** Plans, logs and indexes are updated in the same commit as the change they describe, not after.
- **Public repository.** No secrets, credentials, personal data, or internal details of other companies' systems.
- **Mirror rule.** A folder that needs its own rules gets a `CLAUDE.md` and, next to it, a relative symlink created with `ln -s CLAUDE.md AGENTS.md`. Never create `AGENTS.md` as a regular file ([ADR 0004](vault/decisions/0004-claude-md-canonical-agents-md-symlink.md)).

## Dogfooding: Telar is built the way it says software should be built

- **Log corrections.** When Diego corrects you (rejects an output, redirects an approach, repeats an instruction, or finds that something you called done is not), log it in `vault/qa/corrections/` before the session ends, following `vault/qa/CLAUDE.md`. Corrections are the raw material of Telar.
- **Encode low.** When proposing how to prevent a mistake, prefer the lowest layer of the trust pyramid: architecture, then a deterministic check, then verification, then a skill, and a prose rule only as a last resort (principle 4 in `vault/foundations/principles.md`).
- **Summarize for the owner.** Before closing a substantial piece of work, give Diego a summary he can judge in a minute: what changed, why, what evidence shows it works, what is still open.

## Session routine

1. `git pull` at the start.
2. Read `vault/views/board.md` (or use the grep commands at its top) to see what is proposed, active and open.
3. Before touching a project, read its latest `vN/PLAN.md`.
4. When a change is complete, commit with an English message in the imperative mood and push. While the repository is documentation only, changes go straight to `main`. Once code exists, code goes through a branch and a pull request.
