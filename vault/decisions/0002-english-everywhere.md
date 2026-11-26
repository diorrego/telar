---
id: ADR-0002
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0002: English everywhere in the repository

## Context

Diego works in Spanish, and the name Telar is Spanish. The repository is public, and the tools, harnesses and sources Telar builds on are documented in English.

## Decision

Everything that lands in the repository is in English: documents, notes, templates, IDs, folder and file names, commit messages, branch names and, later, code. Conversations with Diego may be in Spanish; their outcome is written in English. The name Telar stays as is.

## Consequences

- One vocabulary, fixed in [`foundations/glossary.md`](../foundations/glossary.md).
- Corrections logged in Spanish during a session are translated when written to the ledger, keeping the meaning of Diego's words.

> **Note, 2026-11-26.** Review pages in `vault/reviews/` are written in the language the user indicates, as views of English sources ([ADR 0011](0011-review-pages-before-decisions.md)).

## Alternatives considered

- **Spanish, or mixed.** Rejected by Diego.
