---
id: ADR-0004
status: accepted
date: 2026-11-24
decided_by: diego (mirror requested); claude (symlink as the mechanism)
superseded_by:
---

# ADR-0004: `CLAUDE.md` is canonical; `AGENTS.md` is a symlink

## Context

Claude Code reads `CLAUDE.md`. Other harnesses (Codex, Pi, Cursor and more) read `AGENTS.md`. Diego asked for `CLAUDE.md` files mirrored as `AGENTS.md`. Mirroring by copying drifts: in an earlier vault that kept the two in sync by copying, several `AGENTS.md` files had fallen out of date with their `CLAUDE.md`.

## Decision

- `CLAUDE.md` is the only file edited.
- `AGENTS.md` is a relative symlink in the same folder (`ln -s CLAUDE.md AGENTS.md`).
- Today this applies to the repository root, `vault/`, `vault/projects/`, `vault/qa/` and `core/`. Every new folder with its own `CLAUDE.md` gets the symlink in the same commit.

The mirror holds by construction, not by discipline: a deterministic mechanism over a prose rule ([principle 3](../foundations/principles.md)). No sync script is needed.

## Consequences

- Git stores symlinks. On a Windows checkout without symlink support, `AGENTS.md` becomes a text file containing the path; that platform is not a target today.
- An editor or tool that replaces the symlink with a regular file on save breaks the mirror. A future check in the core should verify that every `AGENTS.md` is a symlink to its sibling `CLAUDE.md`.

## Alternatives considered

- **Copies kept in sync by a script.** Drifts when the script is not run, and it is code.
- **`AGENTS.md` canonical, with `CLAUDE.md` importing it (`@AGENTS.md`).** Works in Claude Code, but Diego asked for `CLAUDE.md` as the source.
