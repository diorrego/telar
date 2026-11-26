# CLAUDE.md, vault/

Instructions for coding agents working in the Telar vault. Human overview in `README.md`.

The vault is **documentation, not code**. It holds the thinking behind Telar; the core (`../core/`) holds Telar itself. From here the core is referenced (path, commit), never copied.

## Map

| Folder | What it is | Detail |
|---|---|---|
| `foundations/` | `vision.md`, `principles.md`, `research.md`, `glossary.md`. The product definition | this file, "Foundations" |
| `decisions/` | ADRs named `NNNN-kebab-title.md`, indexed in `decisions/README.md` | this file, "Decisions" |
| `evidence/` | The research conversations, documents, prototype and figures, translated, ordered by date, indexed in `evidence/README.md` | this file, "Evidence" |
| `projects/` | One folder per initiative, each iteration self-contained in `vN/` | `projects/CLAUDE.md` |
| `qa/` | `findings/`, `corrections/`, `sessions/` | `qa/CLAUDE.md` |
| `reviews/` | Review pages: standalone HTML pages, named `YYYY-MM-DD-topic.html`, that Diego reads before he decides | this file, "Review pages" |
| `templates/` | One template per note type. Copy a template to create a note; never edit it in place for a specific note | |
| `views/` | `board.md`: Dataview queries over frontmatter. It filters; it never holds state | |

## Foundations

- `vision.md` says what Telar is, what it is not, and the staged roadmap. `principles.md` lists the principles every design must respect, each traced to its source. `research.md` synthesizes the sources. `glossary.md` fixes the vocabulary.
- Changes to vision or principles are product decisions: propose them to Diego, do not just edit. If a change reverses something, it needs an ADR.
- Use glossary terms exactly. A new concept gets a glossary entry in the same commit that introduces it.
- New research (a talk, paper or post) gets a section in `research.md`: public link, key claims with timestamps or page numbers, and how it supports or challenges the principles. Claims are attributed to their authors; Telar's own positions are marked **Telar**.

## Decisions

- One ADR per decision, from `templates/decision.md`. Numbered sequentially, never renumbered, never deleted.
- `status: proposed | accepted | superseded`. An ADR written by an agent is born `proposed`, even when Diego delegated the choice; only Diego accepts it ([C-0001](qa/corrections/C-0001-metaphorical-folder-name.md)).
- To change an accepted decision, write a new ADR and set `superseded_by` in the old one.
- Keep the index in `decisions/README.md` in sync, in the same commit.
- ADRs are presented for acceptance with their review page, and the ADR records the page's path.

## Review pages

- Every decision asked of Diego (accept ADRs, say go to a plan, answer open decisions) and every review of research, a diagnosis, a design or a model comes with a review page ([ADR 0011](decisions/0011-review-pages-before-decisions.md)). A request without its page is incomplete.
- Contents follow `templates/review.md`: what is asked, one line per decision, the context, diagrams for every design, model or flow, each decision with its options and recommendation, and what comes next.
- Claude Code publishes the page as a private Artifact; other harnesses give the path of the HTML file. The page is saved here in every case, as a standalone document, and the plan log or the ADR records its path and link.
- Pages are in the language the user indicates (Spanish, for Diego) and link to their English sources. When a page and its source disagree, the source wins and the page is rebuilt.
- This repository is public: a page here holds nothing private. An installation's pages stay in its own repository.

## Evidence

- `evidence/` is the record of the research Telar comes from ([ADR 0009](decisions/0009-research-evidence-in-the-vault.md)). Read the relevant items before proposing anything; a diagnosis lists what it read (`projects/CLAUDE.md`).
- Each file starts with its provenance: what it was translated from, when, and where the original is kept.
- Evidence is faithful: never summarize, reword or "improve" it. The only allowed edits fix a translation error or a missed redaction, and each one is noted in `evidence/README.md`.
- The repository is public: absolute local paths, private links and installation-internal details (paths, commit hashes, repository names) are redacted as `[redacted: reason]`.
- New evidence (a new research conversation or document) is added with the same conventions and a row in the index, in the same commit.

## Frontmatter is the state

Every plan, finding, correction and ADR carries the YAML frontmatter defined by its template. A status change updates the `updated` field and the note's log in the same commit. `views/board.md` only filters.

## Writing rules

- English. No em dashes. Short sentences; tables for comparisons; evidence over adjectives.
- Links are relative Markdown links (`[text](../path.md)`), not wikilinks, so they work on GitHub and in Obsidian.
- Dates are absolute (`2026-11-24`), never "yesterday" or "last week".
- Evidence cites `file:line`, commit hashes, or URLs with timestamps.
- No secrets and no personal data. The repository is public.
- In the vault, a finished change is committed and pushed (a local commit is not enough).
