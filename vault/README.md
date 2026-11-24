# Telar vault

The workshop notebook for building Telar: why it exists, what was decided, what is being built, and what went wrong. Open this folder as an Obsidian vault or read it on GitHub; it is plain Markdown either way.

| Folder | Contents |
|---|---|
| `foundations/` | Vision, principles, research synthesis, glossary. The product definition. |
| `decisions/` | Architecture decision records, numbered. |
| `projects/` | Initiatives. Each iteration in its own `vN/` with `DIAGNOSIS.md`, `PLAN.md` and `CLOSEOUT.md`. |
| `qa/` | `findings/` (defects), `corrections/` (agent pushbacks to encode), `sessions/` (exploratory QA). |
| `templates/` | One template per note type. |
| `views/` | `board.md`: plans, findings, corrections and decisions by status (Dataview plugin). |

Conventions in short:

- The state of a plan, finding, correction or decision lives in its frontmatter, never in folder names.
- Plans are born `proposed` and are not implemented until Diego says go.
- A new approach to a project is a new `vN/` folder; iterations never mix.
- Every human correction of an agent is logged and, where possible, turned into a check.
- English, no em dashes, absolute dates, relative Markdown links.

Rules for agents: `CLAUDE.md` here, in `projects/` and in `qa/`.
