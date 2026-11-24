# Glossary

The vocabulary of Telar. Use these terms exactly. A new concept gets an entry in the same commit that introduces it. Sources in [research](research.md).

| Term | Meaning |
|---|---|
| **Benchmark** | A suite of real past tasks replayed against other models, harnesses or core versions, to compare cost and quality on Telar's own data (Lloyd). Lives in `core/evals/`. |
| **Check** | A deterministic guardrail a machine enforces every time: lint rule, type, dependency boundary, test gate. Layer 2 of the trust pyramid. Lives in `core/checks/`. |
| **Code mode** | Letting an agent write code that orchestrates many tool calls outside its context window, instead of calling tools one by one (Ronacher). |
| **Core** | Telar itself: the workshop defined as code, in `core/`. |
| **Correction** | An instance of a human pushing back on an agent: rejecting an output, redirecting an approach, repeating an instruction, or finding a false "done". Logged as `C-NNNN`. Treated as a defect of the workshop. |
| **Corrections ledger** | `vault/qa/corrections/`: every correction, its occurrences, and how it was encoded. |
| **Decision model** | A cheap, fast model (often a classifier) used at a branch point of a workflow instead of a full agent turn (Ronacher). |
| **Durable run** | An agent run that can be suspended, resumed and restarted without a human babysitting it (Ronacher's durable agents). |
| **Encode** | Turn a correction into something in the workshop that prevents it: an architecture change, a check, a verification, a skill, or, last, a rule. |
| **Factory** | A code-defined closed loop that runs agents through the development cycle and continuously measures and improves them (Lloyd). Telar's stage 3. |
| **Factory engineering** | Improving the system that builds the software (skills, context, model mix, evals), as opposed to product engineering (Lloyd). |
| **Feature map** | A map of an application's features from the user's point of view, giving humans and agents shared names for things (Tan). Lives in `core/verify/`. |
| **Finding** | A defect: something does not behave as specified. Logged as `F-NNNN` in `vault/qa/findings/`. |
| **Go** | Diego's explicit instruction to implement a specific plan. Moves the plan from `proposed` to `active`. An answer to an open question is not a go. |
| **Harness** | The program that runs a model as a coding agent (Claude Code, Codex, Pi and others). Telar is not a harness; it uses them. |
| **Human gate** | A point in a workflow where a human must approve, with the evidence named in advance. |
| **Inner loop** | One human working with interactive agents on one change. The focus of stage 1. |
| **Iteration** | One complete pass at a project, self-contained in its own `vN/` folder. |
| **Outer loop** | The development cycle from idea to monitoring, run as workflows. The focus of stage 2. |
| **Owner** | Diego: the person who says go, reviews evidence and approves. |
| **Owner summary** | A summary the owner can judge in about a minute: what changed, why, the evidence, what is open. Adapted from Ronacher's executive summary written before verification. |
| **Product engineering** | Building things that solve real problems for users, through the workshop (Lloyd). |
| **Rule** | Prose guidance that requires judgment. Layer 5, the last resort. Lives in `core/rules/` or in a `CLAUDE.md`. |
| **Score** | An online eval: a judge (model or human) that grades recorded runs on one failure mode (Lloyd). Lives in `core/evals/`. |
| **Self-improvement loop** | Agents aggregate failed scores and corrections into proposed changes to the core, delivered as pull requests that a human approves (Lloyd). |
| **Skill** | A reusable procedure an agent follows for a recurring task, with the CLIs it calls. Layer 4. Lives in `core/skills/`. |
| **Slop** | Output that looks finished but does not fit: copied anti-patterns, needless code, unverified claims, justifications for not doing the right thing. |
| **Stage** | One of Telar's three phases: workshop, loop, factory ([ADR 0006](../decisions/0006-workshop-before-factory.md)). |
| **Target repository** | A repository the core is applied to. Telar is its own first target. |
| **Trust pyramid** | The order in which trust is built, from most to least preferred. Tan's version has four layers (code, static analysis, verification, prose). Telar's has five: 1 architecture, 2 check, 3 verification, 4 skill, 5 rule. |
| **Vault** | `vault/`: the notebook where Telar is thought through. Documentation, not code. |
| **Verification** | Proving a change works by running it, by checking properties, or formally. Layer 3. Lives in `core/verify/`. |
| **Verification artifact** | Evidence an agent produces that a human can judge quickly: screenshot, video, state chart, trace, check or test output, owner summary. |
| **Workshop** | Ronacher's atelier: an environment where a skilled human uses powerful tools to build more ambitious, higher quality software. Telar's stage 1, and what Telar is. |
