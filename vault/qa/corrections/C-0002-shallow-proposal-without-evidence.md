---
id: C-0002
status: encoded
date: 2026-11-24
by: diego
harness: claude-code
model: claude-opus-5-5
occurrences: 1
encoded_as: architecture
encoded_in: vault/evidence/ (evidence moved into the repository); "Evidence inventory" rule in vault/projects/CLAUDE.md; core/ emptied until a plan defines it (ADR 0008)
updated: 2026-11-24
---

# C-0002: Proposals made without working through the evidence

## What the agent did

Across the first session, the agent proposed structure and scope before reading the research it was built on:

- It wrote the vision, the principles and a seven-folder layout for `core/` from the five talks alone, without the research conversations and documents in the research workspace, which it had not found.
- After finding some of those documents, it read the documents but not the conversations, and proposed a definition, new `core/` folders and a quick first project ("woku models its rules"), while the conversations held requirements Diego had stated (research before requirements, instructions in YAML, teams of two or more, channels, isolated environment, read-only operational access, the order rules then workshop then factory).

## The correction

Diego: "I feel you're taking this very lightly." "Core is programming; we must define in the vault what will be done, in a project." "There is a lot of information in the OpenResearch sessions." "All the chats are extremely important." "In fact you should move them to the vault as evidence." (Translated from Spanish.)

## Why the workshop allowed it

- The evidence lived outside the repository, in a tool workspace the agent did not know about, so nothing pointed to it.
- No rule required a diagnosis to list and read the existing evidence before proposing.
- `core/` accepted structure before any plan defined it, so a guess looked like a design.
- The agent optimized for a quick, complete-looking answer over a grounded one.

## Encoding

- **Layer 1, architecture.** The evidence now lives in the repository, in [`vault/evidence/`](../../evidence/README.md), translated and indexed, so a session cannot miss it. `core/` holds only its instructions and a placeholder until a plan defines it ([ADR 0008](../../decisions/0008-telar-is-a-method-and-framework.md)).
- **Layer 5, rule.** [`vault/projects/CLAUDE.md`](../../projects/CLAUDE.md): a diagnosis starts with an evidence inventory that lists every relevant item in `vault/evidence/` and states whether it was read in full, partially or not at all. Proposals about structure or scope cite the evidence they rest on.
- **Candidate check (later).** When code is allowed: a check that fails if `core/` contains files not listed in an accepted structure ADR.

## Log

- 2026-11-24: Logged (occurrence 1). Evidence moved into the vault; rule added; `core/` emptied; first project `core-definition` opened with a full evidence inventory.
