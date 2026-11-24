---
id: ADR-0009
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0009: Research evidence lives in the vault, translated

## Context

[ADR 0001](0001-separate-repository.md) kept the research as read-only input outside this repository and said its sources would be referenced, not copied. Most of the research, however, was not in the research repository: it lived in a tool workspace (three conversations, nine documents, a prototype, figures). The agent missed it for most of a session (correction [C-0002](../qa/corrections/C-0002-shallow-proposal-without-evidence.md)). Diego said all the conversations are extremely important and asked to move them into the vault as evidence, well organized and translated into English.

## Decision

- [`vault/evidence/`](../evidence/README.md) holds the research evidence: the conversations, the working documents, the paper, the prototype and the figures, ordered by date.
- Evidence is translated into English ([ADR 0002](0002-english-everywhere.md)). Each file says what it was translated from, when, and where the original is kept. Translation is faithful: no summarizing or improving.
- Because the repository is public, the translation removes absolute local paths, private links, and woku-internal details (file paths, commit hashes, repository names), marking each removal as `[redacted: reason]`. The originals stay unchanged in the research workspace.
- The five talk transcripts are not copied: they are third-party content. They are cited by public link in [`research.md`](../foundations/research.md).
- Evidence is not edited after it lands, except to fix a translation error or a missed redaction, and each fix is noted in the evidence index.

## Consequences

- This supersedes the part of ADR 0001 that said research material is never copied here. The rest of ADR 0001 stands.
- Diagnoses cite evidence by its path in `vault/evidence/` and must inventory it (rule in [`vault/projects/CLAUDE.md`](../projects/CLAUDE.md)).
- Presentation material generated from the documents (two landing pages and their covers) is listed in the index but not included.

## Alternatives considered

- **Keep evidence outside and link to it.** It is what caused C-0002, and the workspace is local and private.
- **Copy the originals in Spanish.** Breaks ADR 0002, and the originals contain local paths and woku-internal details that should not be public.
