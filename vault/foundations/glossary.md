# Glossary

The vocabulary of Telar. Use these terms exactly. A new concept gets an entry in the same commit that introduces it. Sources in [research](research.md) and [evidence](../evidence/README.md). The same terms are used in the translated evidence.

| Term | Meaning |
|---|---|
| **Acceptance path** | A protected location for the acceptance tests of a work item, owned by product or QA; the builder's changes may not touch it. |
| **Benchmark** | A suite of real past tasks replayed against other models, harnesses or configurations to compare cost and quality on the workshop's own data (Lloyd). |
| **Builder** | The agent identity that implements a work item. |
| **Call-out** | Guidance injected into a stage's instructions when a condition holds. It orients and never blocks. Contrast with gate. |
| **Check** | A deterministic guardrail a machine enforces every time: lint rule, type, dependency boundary, test gate. Layer 2 of the trust pyramid. |
| **Code mode** | Letting an agent write code that orchestrates many tool calls outside its context window, instead of calling tools one by one (Ronacher). |
| **Core** | The framework part of Telar, in `core/`: what every installation shares. Its structure is defined by the [`core-definition`](../projects/core-definition/v1/PLAN.md) project before anything is built. |
| **Correction** | An instance of a person pushing back on an agent: rejecting an output, redirecting an approach, repeating an instruction, or finding a false "done". Logged as `C-NNNN`. Evidence that a rule is missing. |
| **Corrections ledger** | `vault/qa/corrections/`: every correction, its occurrences, and how it was encoded. |
| **Decision model** | A cheap, fast model (often a classifier) used at a branch point of a workflow instead of a full agent turn (Ronacher). |
| **Dossier** | The written record of one work item: product spec, technical spec, log, decisions, verification, summary, run records. Lets another session or person continue. |
| **Durable run** | An agent run that can be suspended, resumed and restarted without a person babysitting it (Ronacher). |
| **Encode** | Turn a correction into something that prevents it: an architecture change, a check, a verification, a skill, or, last, a prose rule. |
| **Evidence** | The research material in `vault/evidence/`: conversations, documents, prototype and figures, translated into English ([ADR 0009](../decisions/0009-research-evidence-in-the-vault.md)). |
| **Factory** | A code-defined closed loop that runs agents through the development cycle and continuously measures and improves them (Lloyd). The last step of the order rules, workshop, factory. |
| **Factory engineering** | Improving the system that builds the software (skills, context, model mix, evals), as opposed to product engineering (Lloyd). |
| **Feature map** | A map of a product's features from the user's point of view, giving people and agents shared names for things (Tan). |
| **Finding** | A defect: something does not behave as specified. Logged as `F-NNNN` in `vault/qa/findings/`. |
| **Forge** | The code hosting platform that holds repositories, changes, reviews and checks (GitHub first). |
| **Framework** | The reusable part of Telar that every installation runs and fills with its own rules and values. Contrast with method. |
| **Gate** | A deterministic condition that must hold for work to advance: an approval of a role on an exact revision, required checks, a status published by a given identity. Decided by code or a person, never by generated text. |
| **Go** | Diego's explicit instruction to implement a specific plan. Moves a plan from `proposed` to `active`. An answer to an open question is not a go. |
| **Handoff test** | A fresh session that reads only the dossier and the repositories can state where a work item is and what comes next. |
| **Harness** | The program that runs a model as a coding agent (Claude Code, Codex, OpenCode, Pi and others). Telar is not a harness; it uses them. |
| **Human gate** | A gate that requires a person's decision, with the evidence named in advance. |
| **Inner loop** | One person working with interactive agents on one change. |
| **Installation** | A workshop that uses Telar to model its rules. Wondeya, a new product started from zero, is the first and, for now, only one; woku is paused ([ADR 0010](../decisions/0010-first-installation-is-a-new-project.md)). |
| **Iteration** | One complete pass at a vault project, self-contained in its own `vN/` folder. |
| **Level** | Where an element of Telar belongs: **T** Telar invariant (the same in every installation); **M** Telar mechanism with project values; **B** project baseline (the project must provide it; Telar states the minimum and checks it); **P** project only (the project's own rules). Proposed in the `core-definition` diagnosis. |
| **Line** | The sequence of stages a work item follows, chosen by risk: light, standard or strict. |
| **Method** | The way of working Telar defines: model rules from corrections, encode them at the lowest layer, keep people at the decisions that matter, review evidence, measure against the current way of working. It can be followed by hand. |
| **Non-negotiable** | An element that must hold in every installation for Telar to work. Candidates are listed as N-01 onward in the `core-definition` diagnosis. |
| **Outer loop** | The development cycle from intake to operation, run as workflows. |
| **Owner** | Diego: the person who says go, reviews evidence and approves. |
| **Owner summary** | A summary a person can judge in about a minute at a decision point: what changed, why, the evidence, what is open (Ronacher's executive summary written before verification). |
| **Product engineering** | Building things that solve real problems for users (Lloyd). |
| **Product spec** | The long-lived description of what a feature must do: invariants and acceptance examples. Contrast with technical spec. |
| **Project baseline** | What a project's repositories must provide for Telar to work: CI workflows, branch protection, CODEOWNERS, lint, tests, an acceptance path, instruction files, a memory location, a verifier identity, the manifest. |
| **Research (stage)** | Investigating a need before agreeing the requirement, with sources and open questions as output; it may change the requirement or end in not building. |
| **Rule** | Anything a workshop depends on that should hold every time. In the trust pyramid, "rule" also names layer 5: prose guidance that requires judgment, the last resort. |
| **Score** | An online eval: a judge (model or person) that grades recorded runs on one failure mode (Lloyd). |
| **Self-improvement loop** | Agents aggregate failed scores and corrections into proposed changes, delivered as pull requests that a person approves (Lloyd). |
| **Skill** | A reusable procedure an agent follows for a recurring task, with the CLIs it calls. Layer 4. |
| **Slop** | Output that looks finished but does not fit: copied anti-patterns, needless code, unverified claims, comments justifying a patch. |
| **Stage** | A step in a line (for example triage, spec, build, verify, handoff). Also used for the steps of a workshop's growth (see [ADR 0006](../decisions/0006-workshop-before-factory.md)); phase 6 of `core-definition` settles that vocabulary. |
| **Technical spec** | The disposable plan of one work item: how the code will change. |
| **Trust pyramid** | The order in which trust is built, from most to least preferred. Tan's version: code, static analysis, verification, prose. Telar's: 1 architecture, 2 check, 3 verification, 4 skill, 5 rule. |
| **Vault** | `vault/`: the notebook where Telar is thought through. Documentation, not code. |
| **Verification** | Proving a change works by running it, by checking properties, or formally. Layer 3. Distinct from validation. |
| **Validation** | A domain person confirming that the result serves the real task. |
| **Verification artifact** | Evidence that a person can judge quickly, tied to a revision and an environment: screenshot, video, trace, check or test output, owner summary. |
| **Verifier** | The agent identity that verifies a work item; separate from the builder and without write access to code. |
| **Work item** | The unit of work: one need taken from intake to its outcome, with a stable identifier and a dossier. |
| **Workshop** | A team or organization that builds software with coding agents, with its people, repositories and rules. Telar is what a workshop uses to model its rules. Also Ronacher's "atelier", the step before the factory. |
