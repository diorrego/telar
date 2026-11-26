---
id: C-0003
status: encoded
date: 2026-11-26
by: diego
harness: claude-code
model: claude-opus-5-5
occurrences: 1
encoded_as: rule
encoded_in: "Read the evidence yourself" in the root CLAUDE.md
updated: 2026-11-26
---

# C-0003: Research and repository review delegated to subagents

## What the agent did

Asked for a diagnosis and a plan that needed an exhaustive review of three repositories and current web research, the agent launched three background subagents (an architecture review of one repository and two web research briefs) to read on its behalf and return summaries, while it read the rest itself.

## The correction

Diego: "don't use subagents, it's a very important task for you to lose the context; do it in logical parts as you plan." (Translated from Spanish.)

## Why the workshop allowed it

- No rule said who must read the evidence behind a diagnosis.
- The agent optimized for wall-clock time over the detail a diagnosis needs. A subagent returns a summary; the details it drops are the ones Diego reviews, and the agent cannot tell what was dropped.
- The evidence inventory rule ([`vault/projects/CLAUDE.md`](../../projects/CLAUDE.md)) asks whether each item was read in full, partially or not at all, but did not say that a summary written by another agent is not a reading.
- It shares a root with [C-0002](C-0002-shallow-proposal-without-evidence.md) (a quick, complete-looking answer over a grounded one), but the mistake and its fix differ: C-0002 was proposing before reading; this is reading through someone else. Logged separately; if it recurs under either form, both entries are reviewed together.

## Encoding

Who reads is a choice the session makes, and the harness offers delegation as a normal tool, so this is encoded at layer 5 (rule):

- Root `CLAUDE.md`, "Dogfooding": research, diagnoses and plans are written from sources the session read itself, in logical parts announced to Diego up front; reading is not delegated to subagents, and a subagent's summary does not count as read in an evidence inventory.

Candidate for a lower layer once configuration is allowed ([ADR 0005](../../decisions/0005-documentation-before-code.md)): a project setting that denies the subagent tool in sessions working on the vault, if the harness supports denying it per project.

## Log

- 2026-11-26: Logged (occurrence 1). The three subagents were stopped before they returned; the review was done in parts by the session itself. Rule added to the root `CLAUDE.md` in the same commit.
