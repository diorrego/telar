---
id: ADR-0001
status: accepted
date: 2026-11-24
decided_by: diego
superseded_by:
---

# ADR-0001: Telar is its own repository, nested in the research folder

## Context

Telar comes out of a local research repository on agentic software factories (talk transcripts and notes). The research has its own history and purpose; Telar is the product built from it. Mixing them would blur sources with decisions.

## Decision

- Telar is an independent git repository in the `telar/` folder inside the research folder.
- Remote: `git@github.com:diorrego/telar.git`, default branch `main`. The repository is public.
- The research repository ignores `telar/`, so the two histories never mix.
- The research is read-only input. Telar references its sources by public URL and summarizes them in its own words in [`foundations/research.md`](../foundations/research.md). Transcripts are never copied here, and Telar's agents never edit files in the research repository.

## Consequences

- Two histories. Git commands run from the research folder do not see Telar; agents must work from `telar/` to work on Telar.
- Because Telar is public and the research is not, anything taken from the research must be a summary with attribution and a public link.

> **Note, 2026-11-24.** The rule that research material is never copied here is superseded by [ADR 0009](0009-research-evidence-in-the-vault.md): research evidence now lives in `vault/evidence/`, translated. The rest of this decision stands.

## Alternatives considered

- **A subfolder of the research repository.** One history, but sources and product decisions mixed, and the research would become public with Telar.
- **A git submodule.** Couples the two repositories for no benefit; the research does not need to pin Telar versions.
