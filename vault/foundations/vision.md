# Vision

## In one line

Telar is an agentic software workshop: the environment, tools and habits with which a small team, starting with one engineer, builds ambitious, high-quality software with coding agents, without losing understanding of what it ships.

## Why a loom

*Telar* is Spanish for loom. On a loom the warp threads are fixed and held under tension, and the shuttle carries the weft across them, fast. The cloth is only as good as the warp. In Telar, checks, verification and rules are the warp; agents carry the weft; the software is the cloth. Speed comes from the shuttle, quality from the warp, and the weaver's attention goes to the pattern.

## The problem

- Coding agents keep getting better under the same harness. They now run for many minutes per task, and the volume of code they produce keeps growing.
- Human attention does not grow. Starting a project got easy; maintaining one did not. The human sets the pace.
- Agents are rewarded for finishing, not for fit. Without a strong environment, volume turns into slop, and agents copy the slop they find.
- Automating a loop that produces slop produces more slop, at a higher token bill.

## The thesis: workshop before factory

A software factory (a code-defined, closed loop that runs agents through the whole development cycle and measures and improves them) is where this ends up. But a factory amplifies whatever its inner loop produces.

So Telar builds the workshop first: an environment where agent output is trustworthy because it is constrained by deterministic checks, proven by verification artifacts, and reviewed by a human only where judgment matters. Every correction a human makes is treated as a defect of the workshop and encoded so it does not recur. The factory comes later, built on that foundation by the same mechanism.

## What Telar is

- **A loom:** the workshop defined as code (checks, verification, skills and rules first; agents, workflows and evals later), versioned, and applied to a target repository.
- **A method:** the corrections ledger, the trust pyramid, review based on evidence, owner summaries, and plans that wait for a human go.
- **Its own first user:** Telar is built with Telar.

## What Telar is not

- Not a coding agent or a harness. It uses existing ones (Claude Code, Codex, Pi and others) and stays thin enough to switch between them.
- Not a prompt collection. Prose is the last layer, not the first.
- Not an "AI teammate" or a swarm of personal agents.
- Not a cloud factory product, at least not before the workshop works.

## Stages

Proposed in [ADR 0006](../decisions/0006-workshop-before-factory.md). Each stage starts when the previous one meets its exit criteria.

| Stage | Focus | Loom folders | Exit criteria (proposed) |
|---|---|---|---|
| 1. Workshop | The inner loop: one human with interactive agents. Trust layers, corrections ledger, verification artifacts, owner summaries | `checks/`, `verify/`, `skills/`, `rules/` | Corrections per session trend down over a sustained period; a typical change is accepted on verification evidence instead of a line by line read; every recurring correction is encoded |
| 2. Loop | The outer loop: workflows as code, recorded runs, scores, self-improvement proposals as pull requests to the loom | `agents/`, `workflows/`, `evals/` | An idea runs to a shipped change through the loop with human gates only at spec review and product review; at least one loom improvement proposed from scores is accepted |
| 3. Factory | Scale: unattended runs, benchmarks on own data, model routing, durable and suspendable runs, sandboxes | to be defined | to be defined |

## How success is measured

Candidate metrics. The projects that build them define them precisely.

| Metric | What it tells | Source |
|---|---|---|
| Corrections per session | Is the workshop learning? | Ronacher |
| Recurrence of corrections | Do encodings work? | Telar |
| Revert rate | Is trust justified? (reference point: about 0.5% at high volume) | Tan |
| Share of changes accepted on evidence | Is review shrinking to artifacts? | Tan, Lloyd |
| Human interactions per change | How much attention does a change cost? | Lloyd |
| Cost per change, cycle time | Is it efficient? | Lloyd |
| Size of `loom/rules/` | Is prose turning into checks? | Telar |

## Open questions

- How the loom is installed in a target repository: copied, generated, vendored, or as a package.
- Which harness comes first, and how much harness-specific packaging is acceptable.
- Where run records and verification artifacts live, and what is kept.
- Local only, or local plus cloud sandboxes, and from which stage.
- Which real product is the first target besides Telar itself.
- Build or borrow for stage 2 and stage 3 infrastructure (orchestration, sandboxes, inference).
