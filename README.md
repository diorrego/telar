# Telar

Telar is a method, and the open framework that implements it, with which an agent-assisted software workshop models its own rules: who can start work, what must be approved, what an agent may touch, what counts as done. Each rule is written down, placed at the layer that enforces it, and measured. The first installation is wondeya, a new product started from zero ([ADR 0010](vault/decisions/0010-first-installation-is-a-new-project.md)).

> **Status: design phase, documentation only.** There is no code yet ([ADR 0005](vault/decisions/0005-documentation-before-code.md)). The current project, [`core-definition`](vault/projects/core-definition/v2/PLAN.md), defines what the core must contain before any of it is built.

## The idea

Coding agents get better every few months. The attention of the people directing them does not. Telar starts from that constraint.

The order comes from the research: first rules, contracts and tests; then the workshop, where people review inside the flow and push back; then the factory, where agents run the development cycle and everything is measured. Every time a person has to correct an agent, a rule is missing; Telar records the correction and encodes it at the lowest layer that prevents it, preferring a deterministic check over another line of instructions.

Read more in the [vision](vault/foundations/vision.md) and the [principles](vault/foundations/principles.md).

## Repository layout

```
telar/
├── CLAUDE.md            instructions for coding agents (AGENTS.md is a symlink to it)
├── LICENSE              Apache License 2.0
├── vault/               the workshop notebook
│   ├── foundations/     vision, principles, research synthesis, glossary
│   ├── decisions/       architecture decision records (ADRs)
│   ├── evidence/        the research: conversations, documents, prototype, figures (translated)
│   ├── projects/        one folder per initiative, one subfolder per iteration (v1/, v2/...)
│   ├── qa/              findings, agent corrections, exploratory sessions
│   ├── templates/       templates for every note type
│   └── views/           board.md: plans, findings and corrections by status
└── core/                the framework every installation shares (being defined; no code yet)
```

The vault is where Telar is thought through. The core is the framework; its structure is defined in a vault project before anything lands in it.

## Where to start

- **Humans:** [vision](vault/foundations/vision.md), then [principles](vault/foundations/principles.md), then the [board](vault/views/board.md).
- **Agents:** [CLAUDE.md](CLAUDE.md). Every `CLAUDE.md` in this repository has an `AGENTS.md` symlink next to it, so harnesses that read either file get the same instructions.

The vault works as an Obsidian vault (the board uses the Dataview plugin), but every note is plain Markdown and reads fine on GitHub.

## Origin

Telar comes out of research on agentic software factories: a literature review, a conceptual framework, pilot designs, a critical review of those designs against recent studies, and talks by Armin Ronacher, Lauren Tan and Zach Lloyd. The material itself, translated, is in [vault/evidence/](vault/evidence/README.md); the synthesis, with every reference and the decisions each one drove, is in [vault/foundations/research.md](vault/foundations/research.md).

## License

Apache License 2.0. See [LICENSE](LICENSE) and [ADR 0007](vault/decisions/0007-license-apache-2.md).
