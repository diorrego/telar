---
id: C-0001
status: encoded
date: 2026-11-24
by: diego
harness: claude-code
model: claude-opus-5-5
occurrences: 1
encoded_as: rule
encoded_in: "Plain names" rule in the root CLAUDE.md; "Decisions" rule in vault/CLAUDE.md; ADR-0003
updated: 2026-11-24
---

# C-0001: Metaphorical folder name instead of a plain one

## What the agent did

Asked to name the folder that holds Telar itself ("core, or whatever name best represents it"), the agent chose a metaphorical name (the English translation of the project name) and recorded its own delegated choice as `accepted` in ADR-0003.

## The correction

Diego: the name is strange as a folder name, in fact a bad name; it must be changed. Then: remove every reference to it, everywhere. (Translated from Spanish.)

## Why the workshop allowed it

- The delegation came with no naming guidance, and the agent favored a clever metaphor over a name that says what the folder holds.
- The name repeated the project name in another language, which tells the reader nothing new.
- The agent set aside the owner's own proposal (`core`) without a concrete problem with it.
- The agent marked a delegated decision `accepted`, so nothing asked Diego to review it.

## Encoding

Naming needs judgment; no check can tell a plain name from a clever one. So this correction is encoded at layer 5 (rule), in two places:

- Root `CLAUDE.md`, "Plain names": folders, files and components are named by what they hold, not by metaphor. When Diego proposes a name, use it unless there is a concrete problem with it, and state the problem.
- `vault/CLAUDE.md`, "Decisions": an ADR written by an agent is born `proposed` even when Diego delegated the choice, so delegated decisions always reach him for review.

The folder is `core/` ([ADR-0003](../../decisions/0003-vault-and-core.md)), and the metaphor was removed from every document.

## Log

- 2026-11-24: Logged (occurrence 1). Folder renamed to `core/`, metaphor removed everywhere, rules added in the same commit.
