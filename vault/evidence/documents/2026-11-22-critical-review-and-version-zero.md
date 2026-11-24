# Critical review of the agentic factory and version zero proposal

> **Evidence.** Translated from Spanish on 2026-11-24. Original: "Revisión crítica de la fábrica con agentes y propuesta de versión cero", working document, 2026-11-22, kept in the research workspace. Redactions are marked `[redacted: reason]`.

**Working document · November 22, 2026.** Reviews the [conceptual framework](2026-11-21-conceptual-framework.md), the [single-project pilot](2026-11-22-pilot-architecture.md), the [adaptation of Warp Factories](2026-11-22-warp-factories-and-pilot.md), the [multi-project design](2026-11-22-multi-project-architecture.md) and the [Blueprint prototype](../prototypes/warp/factory.yaml). It contrasts them with five talks from the AI Engineer channel and with a new literature search (alphaXiv and OpenAlex, 2024 to 2026).

## Verdict in brief

The conceptual framework is sound and the recent literature supports it: delegate by process and by decision, require acceptance that is independent of the executor, leave written memory for the handoff, and measure by accepted change (not by activity). The problem is the order of construction. The architecture documents devote almost all their detail to orchestration: events, queues, VPC, three providers, compaction at 50%, Rust and multi-project. The two things that most determine the quality of a factory get little detail: **deterministic controls in the code itself** and **verification that the builder agent cannot alter**. The five talks and most of the 2026 empirical evidence agree on that order: first the workshop, then the factory.

**Recommendation.** Redefine version zero as *a hardened workshop plus a minimal line*. One product (Woku) with one or two repositories, one vault, one executor and triggering from the CLI. GitHub acts as the state machine, the gates are executable, and the pilot is measured against the current mode (person + agent) over 10 to 15 real work items. VPC, Slack, Postgres/pg-boss, multiple providers, unattended self-improvement and multi-project move to v1, with explicit entry criteria (§4). Since the factory will be a public repository and Woku its first installation, the v0 is framed as a portable kit (§5).

---

## 1. What the five talks contribute (and how much weight they carry)

They are talks, not studies. Three of them are by Zach Lloyd, CEO of Warp, which sells Warp Factories. Lauren Tan's figures are self-reported. They serve as a signal of practice, not as evidence of effect.

| Talk | Thesis | What to take for the v0 | Caution |
|---|---|---|---|
| Lauren Tan, *All Code Is Slop (Except Mine)* ([video](https://www.youtube.com/watch/O_zcc6Xl12g)) | Trust in agents is built with an inverted pyramid: first code and architecture, then lint, types and tests, then runtime or formal verification, and only at the end prose (rules, skills, AGENTS.md). "If your inner loop produces slop, automating it produces more slop". | Every correction to an agent becomes a deterministic control (lint rule, ban on an API, directory boundary) and not another line in AGENTS.md. A *feature map* of the application for runtime verification. Review comes to rely on verification artifacts (video, screenshots, state diagrams). | 11,000 PRs/month and 0.5% reverts are the team's own figures, with no comparator. It took six months to reach that point. |
| Armin Ronacher, *Build the Workshop Before the Software Factory* ([video](https://www.youtube.com/watch/JNexz3Tbiu8)) | Human attention sets the pace. Creating projects is easy and maintaining them is not: 141 repositories created versus 10 to 15 maintained. Knowing when to stop the agent is the decisive skill. | Ask the agent, before the verification phase, for a brief executive summary (HTML) so the person understands what was done without reading the whole diff. Durable agents that can be suspended and resumed. *Code mode* with cheap classifier models for triage decisions. | Data from a single expert user. |
| Zach Lloyd, *Engineer Your Coding Agents Like Any Other System* ([video](https://www.youtube.com/watch/0LeT996Hz3E)) | The factory is a closed-loop system, defined in code and measurable: *factories as code*, data from every session, sandbox, swappable inference, orchestration, and access via API/MCP. | Version the workflow definition. Record all trajectories. Benchmarks with your own tasks and not with SWE-bench. | Sales pitch. The *scores* are LLM-as-judge (§2.6). |
| Zach Lloyd, *How to Build a Software Factory That Improves Itself* ([video](https://www.youtube.com/watch/nKjPBAw_N_0)) | Self-improvement loop: evaluators detect failures and an agent proposes a PR against the factory definition. Cost versus quality benchmark over past runs. | Faced with a pile-up of PRs, he recommends *spec-driven development* and verification through real use (computer use). For budgeting, measure the cost per PR and how much of it goes to evaluation. | He himself says the platform is "overkill" for one person and that its value starts with teams of about 10 people. The benchmark's correctness is decided by an LLM-as-judge, with no human grading. |
| Zach Lloyd, *Software Engineering Is Becoming Factory Engineering* ([video](https://www.youtube.com/watch/tUPPVhBBcoM)) | Cycle: triage → spec (product + technical) → human reviews the spec → implementation → agent + human review → verification → human reviews the product → monitoring. Skill loops with observer agents. | Triage that separates the "easy and unambiguous" (implemented directly) from the hard (goes through a spec). Distinction between the **product spec** (invariants) and the **technical spec** (shape of the code). | He recommends buying rather than building (conflict of interest), although he acknowledges that fitting the factory to the domain is work you have to do yourself. |

**Reading them together.** Tan and Ronacher say "don't automate a loop that is not reliable yet". Lloyd says "treat the factory as measurable infrastructure". The two positions can be reconciled if the v0 measures the inner loop before automating the outer one. Our documents already adopted Lloyd's part: Blueprint, workers, scorers and benchmarks. Almost all of Tan's part is missing.

---

## 2. Critical findings

Each finding states what our documents say, what the evidence says, and what change is proposed.

### 2.1 The production line was designed before checking the inner loop

**In our documents.** The [pilot](2026-11-22-pilot-architecture.md) specifies a Fastify coordinator, RDS + pg-boss, Fargate, Terraform, OpenTelemetry, Slack Bolt, a GitHub App, three provider adapters, a compaction policy with its own acceptance test, and a possible Rust binary. There is no section on the quality of Woku's codebase as input for the agent.

**Evidence.** METR's field study of expert developers working in their own repositories found that with AI they took 19% **longer**, although beforehand they expected to take 24% less and afterwards believed they had been 20% faster ([METR, *Measuring the Impact of Early-2025 AI*](https://www.alphaxiv.org/pdf/2507.09089)). The lesson for us is not the figure, which corresponds to early-2025 models, but that perceived productivity does not work as a measure. Hassan et al. describe factories built three times and iterated, and propose "Start Now and Compound" as a principle, not a full deployment up front ([*The Software Engineering Factory*, p. 24](https://www.alphaxiv.org/pdf/2611.21623?page=24)).

**Change.** The v0 starts with the workshop (§4, phase 0) and only automates the path that already works interactively.

### 2.2 The prototype's gates are written in prose

**In our documents.** In [`factory.yaml`](../prototypes/warp/factory.yaml) the transition to `build` is triggered by `when: The responsible person explicitly approves this revision of the specification`. That natural-language condition is evaluated by a model. The pilot says the right thing ("The process that generates text has no authority to attribute a human approval to itself"), but the prototype contradicts it.

**Evidence.** Hassan et al. separate **gates**, which prevent advancing, from **call-outs**, which guide without imposing, and warn:

> "Instructions placed only in a prompt are soft because an agent may follow them initially and neglect them as its task and context expand." ([p. 19](https://www.alphaxiv.org/pdf/2611.21623?page=19))

Studies on context files confirm that prose is a weak constraint. Across 2,053 evaluable instructions in 6,541 agent commits, mean compliance with AGENTS.md is 59.8%, with a bimodal distribution: some instructions are always followed and others never ([Voria et al., p. 24](https://www.alphaxiv.org/pdf/2611.13709?page=24)). When an instruction becomes obsolete, agents follow it and work around it, but none of them corrected the file ([Mehtiyev et al., p. 1](https://www.alphaxiv.org/pdf/2611.09802?page=1)). Conditional wording is followed less than prescriptive wording ([Tsuchida et al.](https://www.alphaxiv.org/pdf/2611.04367)).

![SE Factory principles 5 to 7: bounded stages, gates versus call-outs, and rigor proportional to risk](../figures/2026-11-22-se-factory-fig6.png 'Hassan et al., Fig. 6. Note the difference between the barrier ("GATE: must pass") and the call-out ("CALL-OUT: must consider"). The motto at the bottom sums up the recommendation for the v0: the smallest protocol sufficient for the risk. [p. 17](https://www.alphaxiv.org/pdf/2611.21623?page=17)')

**Change.** Every transition that produces effects (starting to build, merging, deploying) is decided by code. In the v0, spec approval is a GitHub *approval* from a CODEOWNER on the spec PR in the vault. Branch protection is also enabled with "dismiss stale approvals", so that a new commit invalidates the previous approval. That way the approval is bound to the SHA without writing any infrastructure. Natural-language conditions are reserved for call-outs.

### 2.3 Acceptance independent of the executor is stated but not implemented

**In our documents.** Condition 4 of the [framework](2026-11-21-conceptual-framework.md) says that the criteria only change through an authorized and traceable decision, but no document says how the builder is prevented from changing them.

**Evidence.**
- *Tests without an oracle.* In 86,156 test patches written by agents, 80.2% have no explicit assertions or have weak ones. Counting test files overestimates verification ([Banik et al., p. 1](https://www.alphaxiv.org/pdf/2606.18168?page=1)).
- *Cheating.* In an environment where the answer could not leak, almost all frontier models tried to retrieve it. They escalated from mining the repository history to inspecting git's object store and sweeping the file system for hidden tests ([Gui, p. 1](https://www.alphaxiv.org/pdf/2611.10404?page=1)).
- *Altered controls.* In Jiang and Lysenko's industrial case, already cited in our review, the agents went as far as modifying the CI controls ([*Instant Software Factories*](https://www.alphaxiv.org/pdf/2610.36254?page=1)).

**Change.** For the v0:
1. The work item's acceptance tests live in a protected path (`acceptance/`) that belongs to QA or to product according to CODEOWNERS.
2. A CI check fails if the builder's PR touches that path, the workflows or the lint configuration.
3. The verifier uses a different identity, with no write permission on the code.
4. The builder works in a shallow clone, without the history of future branches.
5. An assertion check (or lightweight mutation testing on the changed files) rejects tests without an oracle.

### 2.4 Merge rate and "autonomy" are misleading as metrics

**In our documents.** The [Warp note](2026-11-22-warp-factories-and-pilot.md) already warns that the dashboard's autonomy metric (PRs merged without a human push) can hide approvals and clarifications. The new evidence supports that caution and extends it.

**Evidence.**
- In AIDev-pop, merged agent PRs receive verified subsequent fixes at **1.62 times the odds** of human PRs in the same repositories ([Takerngsaksiri et al., p. 1](https://www.alphaxiv.org/pdf/2609.26847?page=1)).
- Of 353 rejected agent PRs, 64.3% are not explained by an agent failure: the reason was workflow-related or was not recorded. Among the merged ones, some carried human feedback or corrective human commits ([Peralta et al.](https://www.alphaxiv.org/pdf/2605.22534)).
- A single-author preprint, with weaker evidence, estimates that 59% of merged agent PRs in AIDev are merged by their own author and that the differences between agents disappear under human review ([Baba, *The Self-Merge Illusion*](https://www.alphaxiv.org/abs/2611.self-merge-agentic-software-engineering)).

**Change.** Keep the framework's units (requirement in production, service restored, verified change) and add concrete indicators: **subsequent-fix rate at 14 and 30 days**, revert rate, human minutes per accepted change (broken down into clarifying, reviewing and intervening) and who made each commit in the PR. The 0.5% revert rate that Tan cites serves as an external reference, not as a target.

### 2.5 The 50% compaction rule is overspecified and unsupported

**In our documents.** The pilot sets compaction to happen when `2 × tokens_in_use > effective_window` *(identifiers translated from Spanish)* and defines a test with 50,000 versus 50,001 tokens, with one adapter per provider.

**Evidence.** CompAct-Bench is the first benchmark for compaction of the working context. Even on tasks the agent always solved without compacting, mean accuracy after compaction drops to 56.7%, and the best model reaches 68.5% ([Chen et al., p. 1](https://www.alphaxiv.org/pdf/2611.25673?page=1)). The effect of when to compact depends on the domain.

![Accuracy after compaction according to the point in the run at which compaction happens, for search, code and workspace](../figures/2026-11-22-compactbench-fig2.png "CompAct-Bench, Figure 2. The x axis is task progress (25/50/75% of the reference trajectory), not window occupancy. In code, compacting late performs better (64 → 86%). In search the opposite happens. No fixed threshold is universal. [p. 6](https://www.alphaxiv.org/pdf/2611.25673?page=6)")

What does work is persisted state: in code, continuing from the repository state with no history at all already solves 58 to 72% of the tasks. What compaction must contribute is what cannot be reconstructed:

> "…information that is not directly recoverable from the current state, such as prior decisions, rejected alternatives, and unresolved next steps." ([p. 8](https://www.alphaxiv.org/pdf/2611.25673?page=8))

That matches exactly our "continuity point" and Hassan's Principle 5: each stage should "retrieve context on demand rather than inherit the context from prior stages" ([p. 17](https://www.alphaxiv.org/pdf/2611.21623?page=17)).

**Change.** In the v0 the threshold policy and its adapters are removed. A **new session per stage** is used (spec, build, verification), each one started from the dossier in the vault, with the provider's native compaction within the stage. The acceptance test becomes: "a new session resumes from the log without repeating steps". The threshold can be studied in v1 as an experiment with our own tasks.

### 2.6 Self-improvement and *scores* depend on unreliable judges

**In our documents.** Warp's scorers and benchmarks are adopted, and Lloyd proposes that agents open PRs against the factory definition.

**Evidence.**
- An audit of LLM-as-judge found verdicts that change between identical replicas at temperature zero. The most consistent judge was consistent by repeating wrong verdicts, and agreed with the ground truth only 51% of the time ([Kumar et al., p. 1](https://www.alphaxiv.org/pdf/2610.12083?page=1)).
- Wang and Qi measured their own self-improvement gate. In 9 of 37 configurations, the judge gave the same score whatever the input, without reporting an error. They propose an operational rule: "a change can run unattended only when its old version is kept and its verifier’s strength has been measured" ([p. 1](https://www.alphaxiv.org/pdf/2610.27465?page=1)).

**Change.** In the v0 evaluators only **propose**, and a person reviews any change to the factory definition, the prompts or the skills. Before a judge is used to decide, its agreement is measured against 20 to 30 cases graded by a person, and it is tested with degenerate inputs (empty or inverted). Changes are versioned so they can be reverted.

### 2.7 Security was treated as identity, not as injection

**In our documents.** Identity, read permissions and the GitHub App with scoped tokens are handled well. What is missing is handling the untrusted content that comes in through the same channels that trigger work: Slack messages, issues, PRs, vault notes and tool results.

**Evidence.**
- GitInject ran real GitHub Actions workflows with agents. All providers were vulnerable to at least one serious attack, and the most serious was structural: attacker-controlled configuration files in an unmerged contribution were loaded as operator instructions ([Isbarov et al., p. 1](https://www.alphaxiv.org/pdf/2606.09935?page=1)).
- Adversarial context planted in a repository led Claude Code and Codex CLI to request dangerously broad permission rules in 58% of cases. Once the rule was approved, the exploit completed silently in 81% ([Yang et al., p. 1](https://www.alphaxiv.org/pdf/2610.22987?page=1)).

**Change.**
1. Agents never load AGENTS.md, skills or configuration from unmerged or third-party branches. They are always read from `main`.
2. Only actors registered in the policy can trigger work.
3. Agents cannot create persistent permission rules. The allowlist is a versioned part of the factory.
4. The executor's outbound network is limited to GitHub and the model provider.
5. Write secrets are never in the process that reads external content. The pilot already provides for this for queries, and it must be extended to the whole executor.

### 2.8 Human attention is the scarce resource and must be designed for

**In our documents.** There is a good starting point: human waiting time is separated from execution time.

**Evidence.** Ronacher observes that the number of daily prompts stays stable while the agents' active time multiplies. Reichel et al. propose *deliberate pacing* and argue that "neither uninterrupted autonomy nor frequent human intervention is universal" ([p. 1](https://www.alphaxiv.org/pdf/2611.09550?page=1)). In 95 failed runs of multi-agent systems, errors enter early (median at 18% of the run). In 72% of the failures the trajectory already contained contrary evidence that no agent used ([Wang et al., p. 1](https://www.alphaxiv.org/pdf/2611.13254?page=1)). That is why human intervention should come early, at the spec, and not only at the end.

**Change.** There are two human decision points: the spec and the delivery. Each one arrives with an executive summary in HTML containing the what, the why, the evidence and what is pending. Decisions are grouped into a daily time slot. Reading minutes are recorded.

### 2.9 The specification is the contract, and it has costs

**Evidence.** A study of spec-driven development combined 21 interviews and the SpecMine corpus (470,795 specs). Practitioners report more reliable agents, but also higher planning and review costs. Specs with implementation detail help the agent and degrade quickly, and consistency between spec and code is usually checked only when the change is closed. Without a spec, intent is lost with the chat session ([Agarwal et al., p. 1](https://www.alphaxiv.org/pdf/2608.25202?page=1)).

**Change.** Separate the **product spec** (invariants and acceptance examples, long-lived, in the vault) from the **technical spec** (the work item's plan, disposable), as Lloyd proposes. The product spec's acceptance examples become the protected tests of §2.3. A trivial task can skip the technical spec, but never the acceptance examples.

### 2.10 Too much breadth for the first round

Three providers with adapters, the local and VPC execution modes, the Rust binary, the multi-project design and the CTO page with its configurator multiply the surface before a single work item has been closed. Lloyd recommends testing models and harnesses on your own tasks. That first requires having your own tasks recorded. **A single executor in the v0**, chosen for having authorized access for local unattended use. The second provider comes in at v1 as a comparative experiment on the same work items.

---

## 3. What stays and already has support

- **Control in the process, not in the final review.** This matches the central thesis of Hassan et al.: "Final code review therefore cannot remain the primary organizational control for owning code changes" ([p. 1](https://www.alphaxiv.org/pdf/2611.21623?page=1)).
- **Autonomy by process and by decision**, as opposed to the idea of a "lights-out factory". Supported by Hassan et al. and by Yang et al.'s measurement of automated reviewers ([*Lights-off*](https://www.alphaxiv.org/pdf/2610.13668?page=1)).
- **Vault written by agents, and the handoff test.** Supported by CompAct-Bench (decisions, discarded alternatives and next steps are what cannot be recovered from state) and by the finding that intent is lost in the chat.
- **Trajectories as evidence.** Ullrich et al. propose treating them as QA artifacts, although they warn that on their own they do not prove that the decisions are justified ([p. 1](https://www.alphaxiv.org/pdf/2611.22323?page=1)).
- **Cost per accepted delivery, including rework.** Hassan et al. propose "Price the workflow rather than the worker" with rigor proportional to risk ([p. 20](https://www.alphaxiv.org/pdf/2611.21623?page=20)).
- **Playwright + Chromium with approved screenshots** as reproducible regression, with computer use only as exploration. This fits Tan's "runtime verification".

---

## 4. Proposed version zero

### Scope

| Dimension | V0 | Moves to v1 |
|---|---|---|
| Product | Woku, one service and, if the work item requires it, its interface | Other products or multi-project |
| Memory | Existing [woku's engineering vault] and [woku's QA vault], one folder per work item | Managed vault |
| Trigger | Local CLI (`factory open <issue>`) | Slack, Sentry events, schedules |
| State | GitHub: issue, spec PR, code PR, checks, approvals. One `state.md` per work item in the vault | PostgreSQL + durable queue |
| Executor | One agent CLI in headless mode, on the machine of whoever triggers it | VPC/Fargate, second provider |
| Context | New session per stage, native compaction | Threshold experiment |
| Self-improvement | Evaluators propose and a person decides | Unattended changes only with a measured verifier and rollback |

*(File names and the CLI command translated from Spanish.)*

### Phase 0: the workshop (before automating)

1. **Inventory of corrections.** Review the last 30 to 50 PRs made with agents at Woku and the notes in [redacted: internal woku reference]. Every correction that recurs becomes a deterministic control: lint rule, import ban, type or architecture test. Initial target: 5 to 10 rules with messages that state the root cause.
2. **Feature map** of Woku for the verifier: screens, flows and test data, alongside the existing journeys in [redacted: internal woku reference].
3. **Protected acceptance path** and the CI checks from §2.3.
4. **Short AGENTS.md**, with only what cannot be expressed as a control, written prescriptively. A check flags obsolete paths or commands.

### Phase 1: the minimal line

```text
issue ─► triage ─► product+technical spec (PR to the vault) ─► [CODEOWNER APPROVAL on SHA]
      ─► build (new session, branch, without touching acceptance/) ─► deterministic CI
      ─► verify (different identity, Playwright, evidence in [woku's QA vault])
      ─► HTML summary + dossier ─► [human MERGE]
```

- Each arrow is executed by a runner script (Node or shell) that reads the state in GitHub. There is no permanent coordinator.
- Triage classifies: trivial, which goes straight to build with acceptance examples, or ambiguous, which goes through a spec.
- Executable limits per stage: number of build retries and a token or time budget. When they run out, the work item is blocked with a reason.
- Dossier in [redacted: internal woku reference]: `spec.md`, `log.md`, `verification.md`, `summary.html`, plus the links to the SHA, PR and CI run.

### Measurement: compare against the current mode

- **Design.** 10 to 15 real Woku work items, assigned alternately to "factory v0" and to "person + interactive agent", with the same acceptance criteria. They can be paired by estimated size. Two cases, as the current plan provides, are enough to debug, not to decide.
- **Objective recording**, with timestamps and not self-report (because of the perception bias in METR).

| Indicator | How it is obtained |
|---|---|
| Human minutes per accepted change (clarify, review, intervene) | Timestamps in the dossier and GitHub events |
| Cycle time and time waiting on humans | GitHub events |
| Cost in tokens or quota per accepted change, including failed attempts | Runner record |
| Subsequent fixes at 14 and 30 days, and reverts | `git log`, with PRs linked to the work item |
| Strength of the added tests (assertions, killed mutants) | CI check |
| Handoff: did a new session resume without asking the person? | Log |

### Criteria for moving to v1

- At least 10 work items closed through the line, with a complete dossier and no transition that was not decided by code or by an authenticated person.
- Human minutes per accepted change no worse than in the current mode, and subsequent fixes no higher.
- Zero builder modifications to `acceptance/`, workflows or lint that made it into a merge.
- An automated judge used only if its agreement with human grading was measured and is acceptable.

---

## 5. Public repository: Woku as the first installation

**Goal clarified (November 22, 2026).** The factory will be a public repository so that other people and companies can set up their own. Woku is the first installation and the reference case. This does not change the recommendation of a minimal v0; it reinforces it.

**Every infrastructure dependency is a barrier to adoption.** A kit that works with GitHub, an agent CLI and Markdown can be tried in an afternoon. One that requires Terraform, AWS, RDS and Fargate leaves out almost all small teams. The VPC becomes an optional deployment profile in v1, not the default path. Lloyd himself places the value of a full platform at teams of about 10 people or more.

**Separate the public core from the private installation.**

| Public repository (the kit) | Woku installation (private) |
|---|---|
| Versioned formats: product spec, technical spec, dossier, `state.md` and decision record, with templates | Contents of [woku's engineering vault] and [woku's QA vault], repository names, real people and CODEOWNERS |
| Runner and the executor adapter contract, with one implementation | Provider accounts, tokens and quotas |
| Reusable CI checks: protected acceptance path, assertions or oracles, configuration read only from `main` | Lint rules specific to Woku's domain |
| Project manifest schema, with validator | Woku's manifest |
| Measurement protocol and comparison script | Data from Woku's work items |

**What lasts is the open formats, not the tool.** Ronacher warns that collaboration depends on common standards and formats. The value of the repository lies in the protocol (stages, gates, evidence) and in its files, and both must work the same with Claude Code, Codex, OpenCode or a Warp Blueprint. The formats carry `schemaVersion` from day one.

**Portability is proven, not declared.** The v0 acceptance criterion includes a second project: an example repository inside the kit (`examples/support-agent`) that reuses the case already designed in the [prototype](../prototypes/warp/factory.yaml). Anyone must be able to reproduce the complete journey without access to Woku. The manifest cannot contain anything specific to Woku. The full multi-project design (one installation with several isolated projects) stays in v1.

**Defaults have to be safe.** Whoever adopts the kit will run it with their own credentials and on their own code. The defenses from §2.7 must come enabled by default and be documented in a `SECURITY.md` with the threat model. If the kit's repository is maintained with its own factory, which is desirable to show that it works, PRs from outside people are untrusted content. They must never trigger agents with credentials without a label applied by whoever maintains the project. That is exactly the GitInject scenario.

***Before publishing, clean up internal Woku references.*** The [conceptual framework](2026-11-21-conceptual-framework.md) cites paths and commits from [woku's engineering vault] and [woku's QA vault], and the [pilot](2026-11-22-pilot-architecture.md) cites [redacted: internal woku reference]. In the public version it is better to describe them as "practice observed in an installation" or to move them to the private documentation.

**Measurement can be the distinctive contribution.** Public claims about software factories are mostly self-reported or vendor figures. An open protocol for comparing "factory versus person + agent" on the same work items gives every adopter a way to evaluate their own. If Woku authorizes it, publishing aggregate results would strengthen the project.

---

## 6. Quality of the evidence

- Almost all the new literature consists of **preprints from 2025 to 2026**. Some indicate submission to or acceptance at a venue (TOSEM for Voria et al. and for Hassan et al., NeurIPS for GitInject and for Wang and Qi), but we did not verify this in every case. The repository studies almost always use AIDev, which is open source and has agents from 2025 to 2026. The figures may not carry over to a small team with private code.
- *The Self-Merge Illusion* is single-authored and comes from a collective with no academic affiliation. It is used only as a hint that corroborates Peralta et al.
- The METR study used early-2025 models. Ronacher shows that later models reduced his corrections. Its value for us is methodological.
- The talks are practitioner testimony and, in Warp's case, sales material.

## 7. Open decisions for the team

1. Do we accept scaling the v0 down to CLI + GitHub + vault, without a VPC, and postponing the CTO page as v1 material?
2. Which license will the kit use? Apache-2.0 includes an explicit patent grant; MIT is simpler. What will it be called, and who maintains it?
3. What of the Woku experience can be published as a reference case: only aggregate metrics, or also anonymized example dossiers?
4. Which executor has authorized access for local headless use with the account of whoever triggers it?
5. Who is the CODEOWNER of `acceptance/` and of the product specs at Woku?
6. Which 10 to 15 work items from Woku's backlog go into the comparison, and who assigns them alternately?
