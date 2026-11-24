# Telar

Telar (Spanish for *loom*) is an agentic software workshop: the environment, tools and habits with which a small team, starting with one engineer, builds ambitious, high-quality software with coding agents without losing understanding of what it ships.

> **Status: design phase, documentation only.** There is no code yet. See [ADR 0005](vault/decisions/0005-documentation-before-code.md).

## The idea

Coding agents get better every few months. The attention of the people directing them does not. Telar starts from that constraint.

Before automating anything (the "software factory"), Telar builds the workshop: a codebase and an environment where agent output can be trusted because it is constrained by deterministic checks, proven by verification artifacts, and reviewed by a human only where judgment is needed. Every time a human has to correct an agent, the correction is treated as a defect of the workshop and encoded so it does not happen again. Automation and self-improving loops come later, built on that foundation with the same mechanism.

Read more in the [vision](vault/foundations/vision.md) and the [principles](vault/foundations/principles.md).

## Repository layout

```
telar/
├── CLAUDE.md            instructions for coding agents (AGENTS.md is a symlink to it)
├── vault/               the workshop notebook
│   ├── foundations/     vision, principles, research synthesis, glossary
│   ├── decisions/       architecture decision records (ADRs)
│   ├── projects/        one folder per initiative, one subfolder per iteration (v1/, v2/...)
│   ├── qa/              findings, agent corrections, exploratory sessions
│   ├── templates/       templates for every note type
│   └── views/           board.md: plans, findings and corrections by status
└── loom/                Telar itself: the workshop defined as code (contracts only, for now)
    ├── checks/  verify/  skills/  rules/      stage 1: workshop
    └── agents/  workflows/  evals/            stage 2: loop
```

The vault is where Telar is thought through. The loom is Telar itself. Nothing lands in `loom/` without a project in `vault/projects/` that explains why.

## Where to start

- **Humans:** [vision](vault/foundations/vision.md), then [principles](vault/foundations/principles.md), then the [board](vault/views/board.md).
- **Agents:** [CLAUDE.md](CLAUDE.md). Every `CLAUDE.md` in this repository has an `AGENTS.md` symlink next to it, so harnesses that read either file get the same instructions.

The vault works as an Obsidian vault (the board uses the Dataview plugin), but every note is plain Markdown and reads fine on GitHub.

## Origin

Telar comes out of research on agentic software factories, mainly talks by Armin Ronacher, Lauren Tan and Zach Lloyd. The research lives in a separate repository; its synthesis is in [vault/foundations/research.md](vault/foundations/research.md).
