# core

Telar itself: the workshop defined as code. Everything an agentic workshop needs to make agent output trustworthy, versioned so it can be diffed, branched, rolled back, and improved by agents through pull requests.

> **Status: empty by design.** Each folder has a `README.md` that is its contract: what belongs there and what does not. Formats, languages, and how the core is installed into a target repository are decided by the first core projects in [`../vault/projects/`](../vault/projects/), not here.

## Layout

Folders are grouped by stage ([ADR 0006](../vault/decisions/0006-workshop-before-factory.md)). Within the workshop stage they follow the trust pyramid: the earlier the layer, the more it is preferred when encoding a correction.

| Stage | Folder | Pyramid layer | Holds |
|---|---|---|---|
| 1. Workshop | [`checks/`](checks/) | 2. Check | Deterministic guardrails: lint rules, dependency boundaries, type and test gates |
| 1. Workshop | [`verify/`](verify/) | 3. Verification | Verification that produces artifacts a human can judge: runtime drivers, feature maps, property-based and formal specs |
| 1. Workshop | [`skills/`](skills/) | 4. Skill | Reusable procedures for agents, with the CLIs they call |
| 1. Workshop | [`rules/`](rules/) | 5. Rule | Prose guidance that requires judgment. The smallest layer, and it should shrink |
| 2. Loop | [`agents/`](agents/) | | Agent definitions: role, model, harness, tools, permissions |
| 2. Loop | [`workflows/`](workflows/) | | The development loop as declarative definitions: stages, transitions, human gates |
| 2. Loop | [`evals/`](evals/) | | Scores over recorded runs, benchmarks replayed from past tasks, self-improvement proposals |

Layer 1 of the pyramid (architecture) has no folder on purpose: it lives in the code of the repository the core is applied to. Stage 3 (factory: unattended runs, sandboxes, durable runs, model routing) gets folders when it gets a plan.

## Targets

The core is applied to a target repository. Telar is its own first target: the core must be able to check and verify itself.
