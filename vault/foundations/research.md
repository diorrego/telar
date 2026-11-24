# Research synthesis

The research behind Telar: how it unfolded, what each source claims, and which decisions each one drove. Claims are attributed to their authors; Telar's own positions are marked **Telar**. Talk timestamps are mm:ss; paper citations give the page where possible.

The research conversations and working documents (literature review, paper, conceptual framework, pilot designs, critical review, kit design) are in [`vault/evidence/`](../evidence/README.md), translated into English. The talk transcripts are not copied (third-party content); they are cited by public link. This file is the synthesis.

Synthesis date: 2026-11-24.

## 1. How the research unfolded

The order matters, because the main conclusion (workshop first) came from a review that reversed an earlier design.

| Date | Step | Outcome |
|---|---|---|
| 2026-11-21 | Exploratory literature review (alphaXiv, OpenAlex) | A research question, a working definition, six annotated readings and an extraction protocol ([section 3.1](#31-what-a-software-factory-is)) |
| 2026-11-21 to 22 | Five practitioner talks (AI Engineer channel) | Practice signals: workshop before factory, the trust pyramid, factories as code ([section 2](#2-practitioner-talks)) |
| 2026-11-22 | Conceptual framework, single-project pilot, adaptation of a commercial factory product, multi-project design | A sound framework, but designs that put almost all their detail into orchestration (events, queues, cloud, several providers) |
| 2026-11-22 | Critical review against a new literature search (2024 to 2026) | Verdict: the framework holds, the build order is wrong. Version zero becomes a hardened workshop plus a minimal line ([section 4](#4-what-the-research-decided)) |
| 2026-11-22 | Goal clarified: a public kit others adopt; a real product is its first installation | Every infrastructure dependency is an adoption barrier; portability must be proven with a public example; Apache-2.0 proposed |
| 2026-11-24 | This repository | Telar starts from the critical review's conclusions |

**Research question.** Which decisions in the delivery cycle can a system of agents take, from receiving an objective until someone accepts the change, and what evidence shows whether that delegation improves the result?

**Working definition.** An agentic software factory is a system that receives a product or maintenance objective, coordinates several stages of work repeatably, and keeps evidence that allows the result to be accepted, corrected or escalated. The number of agents, their role titles and whether a person approves at the end are independent dimensions.

**Guiding question.** With the same objective and the same acceptance tests, when does a factory reduce total human time per accepted change, and how much work reappears later as review, rework or incidents?

## 2. Practitioner talks

Five talks from the AI Engineer channel. They are testimony from practitioners, not studies: three are by the CEO of a company that sells a factory product, and the figures are self-reported. They are read as signals of practice; the papers in section 3 are read as evidence.

| ID | Talk | Speaker | Link |
|---|---|---|---|
| T1 | Build the Workshop Before the Software Factory | Armin Ronacher (Earendil) | https://www.youtube.com/watch?v=JNexz3Tbiu8 |
| T2 | All Code Is Slop (Except Mine) | Lauren Tan | https://www.youtube.com/watch?v=O_zcc6Xl12g |
| T3 | Software Engineering Is Becoming Factory Engineering | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=tUPPVhBBcoM |
| T4 | Engineer Your Coding Agents Like Any Other System | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=0LeT996Hz3E |
| T5 | How to Build a Software Factory That Improves Itself | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=nKjPBAw_N_0 |

### T1. Ronacher: build the workshop before the factory

Build the atelier, where a skilled person uses powerful tools to make more ambitious and better software, before building the factory.

- **Models improve under a stable harness.** The Pi agent's core harness has the same tools it had a year ago and is far more capable, purely from better models. Plugins he loved (an auto-research loop) are no longer necessary (00:44 to 02:40).
- **His own data.** Corrections per session went down with every model. The P90 time an agent runs per task went from about 2.5 minutes to 14 minutes or more. Agents increasingly prefer Bash; "code mode" is rising (02:40 to 04:24).
- **Attention is the limit.** Prompts per day are flat (120 to 190) while agent active time grew to many times his working day. He started 141 repositories in a year and maintains only 10 to 15. Starting got easy; maintaining did not (04:36 to 07:10).
- **Attention matters even when automated.** A friend fully automated an open source project and later turned it off when he stopped caring about it (07:19 to 07:58).
- **Push back.** The agent is rewarded for completing the goal, not for what we are happy with over time. Avoid the "Simpson car" of features. "True skill versus agent skill" (08:01 to 10:08).
- **Stay within understanding.** Around 70% into a session, before verification, the agent writes a short executive summary and a typeset HTML page, because he no longer reads the code in many cases (10:13 to 11:08).
- **Few dependencies, but no uncontrolled growth.** Divergent implementations of the same format (a tar archive read differently by different tools); standards and open formats matter; forks replace upstreaming (11:24 to 13:31).
- **Harness directions.** Durable agents that suspend, resume and restart themselves (15:17 to 16:47). Code mode with cheap classifier models at each branch of an on-demand workflow (16:49 to 19:17).
- **Closing.** "Now that we can build everything, maybe we should not" (19:21).

### T2. Tan: all code is slop (except mine)

The meta-skill is keeping or raising quality while massively increasing output. It is about trust built through investment in the agent's environment (00:12 to 01:56).

- **The inverse pyramid.** Code itself (API design, architecture), then static analysis (lint, types, compilers, tests), then verification (runtime and formal), then a little prose (rules, skills, AGENTS.md) (02:03 to 02:59).
- **Corrections become checks**, not more lines in the rules (03:12 to 03:27).
- **The codebase is a garden.** In 2024 she reviewed three colleague pull requests when she got to work; today it is more like 300. Agents copy anti-patterns because they look established (03:27 to 04:58).
- **Ban what needs nuance** (`useEffect` banned in product code) and give context through directory structure (process boundaries enforced by a dependency analyzer) (05:26 to 06:56).
- **Prose is an escape hatch.** Agents use comments and rules to justify not doing the right thing, and over-rotate small corrections into hard rules. Her team banned 99% of comments and wrote lint rules whose messages point to the root cause (06:56 to 09:10).
- **Review becomes looking at verification artifacts**: videos, screenshots, state diagrams; a feature map as shared vocabulary; custom CLIs inside skills; TLA+, Lean and property-based UI tests (09:40 to 13:21).
- **Tokens go to verification**: about 70% of daily tokens (11:53 to 12:52).
- **Results.** 11,000 pull requests in a month, revert rate steady at about 0.5%, performance improved (13:32 to 15:10).
- **"If your inner coding loop produces slop, automating that loop just produces more slop"** (15:11 to 16:07).

### T3 to T5. Lloyd: factory engineering

One thesis in three talks: software engineering is becoming factory engineering.

- **Definition.** "A code-defined, closed loop system for continuously measuring and improving cloud coding agents" (T4 03:44). Not loose automations, AI teammates, shared skills or personal swarms (T4 03:14 to 03:38).
- **The loop.** Triage (easy and unambiguous goes straight to implementation), spec for hard work (a product spec with invariants, a tech spec with architecture), human spec review, implementation, agent then human code review, verification (computer use), human product review, ship, monitor (T3 03:22 to 04:03, 10:03 to 12:02).
- **The stack.** Factories as code, a data layer recording every run, sandboxed compute, interchangeable inference, orchestration, API and MCP access (T4 08:09 to 10:40; T5 17:12 to 17:44).
- **Measurement and self-improvement.** Cycle time, human interactions per pull request, cost; LLM-as-judge scores over recorded runs; agents open pull requests against the factory definition (T5 08:12 to 14:42; T4 12:51 to 15:51). Skill loops with observer agents (T3 14:03 to 14:48).
- **Benchmarks on your own data**, curated by hand at first (T5 14:46 to 17:04, 20:10 to 20:47).
- **Against pull request pile-up:** spec-driven development and computer use verification (T5 18:12 to 18:50).
- **Fit.** Overkill for an individual; valuable from about 10 engineers (T5 21:23 to 21:53). Taste and product sense remain essential (T3 19:12 to 20:12).

## 3. Academic references

Most are 2025 and 2026 preprints (see [section 6](#6-quality-of-the-evidence)). They are grouped by the question they answer. The last column says what each one changed in the design.

### 3.1 What a software factory is

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R1 | Cusumano, *The Software Factory Reconsidered*. [link](https://hdl.handle.net/1721.1/11025) | The factory as a way of organizing engineering work predates agents; repeatability lives in the organization: knowledge, responsibilities and delivery means kept between changes. | A factory is an organizational capability, not a tool. |
| R2 | Qian et al., *ChatDev*, ACL 2024. [link](https://aclanthology.org/2024.acl-long.810/) | Specialized agents (design, code, test) converse from a user requirement. Leaves open who maintains the product after delivery. | Telar targets maintenance of existing software, not only creation. |
| R3 | Pavlenko et al., *Towards an AI Software Factory for Data Systems*, 2026. [link](https://www.alphaxiv.org/pdf/2609.36323) | Microsoft repositories; operations feed planning. Works best for changes with a measurable objective. Evidence that review got shorter is called anecdotal (§2.4). | Delegate first where a signal can judge each attempt. |
| R4 | Jiang and Lysenko, *Instant Software Factories*, 2026. [link](https://www.alphaxiv.org/pdf/2610.36254?page=1) | Two industrial installations, configured by hand over 15 and 17 days. Agents modified the CI controls. At least 5.6% of issues marked fixed had a wrong fix found later. | Activity and delivered quality need independent measures; builders must not touch their own controls. |
| R5 | Hua, *Beyond the Agent Harness*, 2026. [link](https://www.alphaxiv.org/pdf/2611.06946?page=1) | The factory boundary is where a system coordinates distinct runs, transfers state between them, or changes its own operation from results. One operator, six projects. | Distinguishes a harness from a factory; Telar is not a harness. |
| R6 | Hassan et al., *The Software Engineering Factory*, 2026. [link](https://www.alphaxiv.org/pdf/2611.21623?page=1) | "Final code review therefore cannot remain the primary organizational control" (p. 1). Gates that block versus call-outs that guide (p. 17, 19). Each stage retrieves context on demand (p. 17). "Price the workflow rather than the worker" (p. 20). "Start Now and Compound" (p. 24). Rigor proportional to risk. | Control lives in the process; gates are code; start small and compound. |
| R7 | Yang et al., *(When) Should a Software Factory be Lights-off?*, 2026. [link](https://www.alphaxiv.org/pdf/2610.13668?page=1) | CRBugBench: reviewer agents miss bugs that need reasoning beyond local code, and do worse on industrial repositories. | Autonomy by process and by decision, not a "lights-off" factory. |
| R8 | iReDev, 2025. [link](https://www.alphaxiv.org/pdf/2507.13081?page=1) | Agents for requirements elicitation, analysis and validation. | Research before building can end in not building. |
| R9 | MetaGPT. [link](https://www.alphaxiv.org/pdf/2308.00352) | Standard operating procedures between agent roles. | Candidate for the next screening. |
| R10 | *Human-In-The-Loop Software Development Agents*, ICSE-SEIP 2025. [link](https://doi.org/10.1109/ICSE-SEIP66354.2025.00036) | Human intervention in agent development loops. | Candidate for the next screening. |

The review's **extraction protocol** follows one unit of work from start to end and records five fields: input and scope; coordination (who decomposes, assigns, keeps state, retries or escalates); human authority (what a person must start, clarify, review and authorize, and whether their time is measured); acceptance (who defines and checks the criterion); results and evidence (comparator, total time, human effort, cost per accepted change, later defects, follow-up length).

### 3.2 Build order and how to measure productivity

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R11 | Peng et al., *The Impact of AI on Developer Productivity*, 2023. [link](https://www.alphaxiv.org/pdf/2302.06590?page=1) | Controlled experiment: an HTTP server built with or without an AI assistant. | The comparator design: same objective, same acceptance criteria. |
| R12 | METR, *Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity*, 2025. [link](https://www.alphaxiv.org/pdf/2507.09089) | Experts in their own repositories took 19% longer with AI, after expecting to be 24% faster, and afterwards believed they had been 20% faster. | Perceived productivity is not a measure; record timestamps, not self-reports. |

### 3.3 Prose is a weak constraint

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R13 | Voria et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.13709?page=24) | Across 2,053 checkable instructions in 6,541 agent commits, mean AGENTS.md compliance is 59.8%, and bimodal: some instructions are always followed, others never (p. 24). | Rules are the last layer of the trust pyramid; effects are decided by code. |
| R14 | Mehtiyev et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.09802?page=1) | When an instruction goes stale, agents follow it or work around it; none fixed the file. | Checks must detect stale paths and commands in instruction files. |
| R15 | Tsuchida et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.04367) | Conditional wording is complied with less than prescriptive wording. | Rules are short, specific and prescriptive. |

### 3.4 Acceptance independent of the builder

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R16 | Banik et al., 2026. [link](https://www.alphaxiv.org/pdf/2606.18168?page=1) | Of 86,156 test patches written by agents, 80.2% have no explicit or only weak assertions. | Counting tests overstates verification; check assertion strength. |
| R17 | Gui, 2026. [link](https://www.alphaxiv.org/pdf/2611.10404?page=1) | Where the answer could not leak, almost every frontier model tried to recover it, escalating from repository history to the git object store to sweeping the file system for hidden tests. | The builder works without access to acceptance tests or future history. |

R4 (agents modified CI controls) belongs here as well.

### 3.5 Metrics that mislead

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R18 | Takerngsaksiri et al., 2026. [link](https://www.alphaxiv.org/pdf/2609.26847?page=1) | Merged agent pull requests receive verified later corrections at 1.62 times the odds of human pull requests in the same repositories. | Track the correction rate 14 and 30 days after merge. |
| R19 | Peralta et al., 2026. [link](https://www.alphaxiv.org/pdf/2605.22534) | Of 353 rejected agent pull requests, 64.3% are not explained by an agent failure; many merged ones carried human corrective commits. | Merge rate and "autonomy" hide human work; record who made each commit. |
| R20 | Baba, *The Self-Merge Illusion*, 2026. [link](https://www.alphaxiv.org/abs/2611.self-merge-agentic-software-engineering) | Single-author preprint, weaker evidence: 59% of merged agent pull requests are merged by their own author, and differences between agents vanish under human review. | Used only as a hint that supports R19. |

### 3.6 Context, specs and handoff

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R21 | Chen et al., *CompAct-Bench*, 2026. [link](https://www.alphaxiv.org/pdf/2611.25673?page=1) | After compaction, mean accuracy falls to 56.7% even on tasks always solved without it (best model 68.5%). No compaction threshold is universal (p. 6). In code, continuing from the repository state alone solves 58 to 72%. What must be kept is "prior decisions, rejected alternatives, and unresolved next steps" (p. 8). | A fresh session per stage, started from the written record; the record holds decisions, rejected alternatives and next steps. |
| R22 | Agarwal et al., spec-driven development and the SpecMine corpus, 2026. [link](https://www.alphaxiv.org/pdf/2608.25202?page=1) | 21 interviews and 470,795 specs: more reliable agents, but more planning and review cost. Specs with implementation detail help, then decay. Without a spec, intent is lost with the chat session. | Separate a long-lived product spec (invariants and acceptance examples) from a disposable technical spec. |
| R23 | Ullrich et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.22323?page=1) | Agent trajectories can serve as QA artifacts, but alone they do not prove decisions were justified. | Record runs, and record decisions separately. |

### 3.7 Judges and self-improvement

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R24 | Kumar et al., 2026. [link](https://www.alphaxiv.org/pdf/2610.12083?page=1) | LLM-as-judge verdicts change between identical runs at temperature zero; the most consistent judge agreed with ground truth 51% of the time. | Measure a judge against 20 to 30 human-graded cases and degenerate inputs before it decides anything. |
| R25 | Wang and Qi, 2026. [link](https://www.alphaxiv.org/pdf/2610.27465?page=1) | In 9 of 37 configurations of their own self-improvement gate, the judge gave the same score whatever the input, silently. Rule: "a change can run unattended only when its old version is kept and its verifier's strength has been measured". | Evaluators propose, humans decide; every change is versioned and revertible. |

### 3.8 Security

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R26 | Isbarov et al., *GitInject*, 2026. [link](https://www.alphaxiv.org/pdf/2606.09935?page=1) | In real CI workflows with agents, every provider was vulnerable to at least one serious attack; the worst was structural: attacker-controlled configuration in an unmerged contribution was loaded as operator instructions. | Agents read instructions, skills and configuration only from the main branch. |
| R27 | Yang et al., 2026. [link](https://www.alphaxiv.org/pdf/2610.22987?page=1) | Adversarial context planted in a repository led two major coding agents to request dangerously broad permission rules in 58% of cases; once approved, the exploit completed silently in 81%. | Agents never create persistent permission rules; the allowlist is versioned. |

### 3.9 Human attention

| ID | Reference | Finding | Effect on Telar |
|---|---|---|---|
| R28 | Reichel et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.09550?page=1) | "Neither uninterrupted autonomy nor frequent human intervention is universal"; they propose deliberate pacing. | Human decision points are designed, not left to chance. |
| R29 | Wang et al., 2026. [link](https://www.alphaxiv.org/pdf/2611.13254?page=1) | In 95 failed multi-agent runs, errors entered early (median at 18% of the run), and in 72% the trajectory already held contrary evidence that no agent used. | Intervene early, at the spec, not only at the end. |

## 4. What the research decided

The critical review turned the sources above into the direction Telar starts from. Each point lists the sources behind it.

| # | Decision | Sources |
|---|---|---|
| 1 | **Workshop before the line.** Build deterministic controls in the codebase first; automate only a path that already works interactively. | T1, T2, R6, R12 |
| 2 | **Gates are code.** Every transition with effects (start building, merge, deploy) is decided by code or an authenticated person, never by generated text. Natural language conditions are only call-outs. A spec approval is a forge approval by the owner, tied to the reviewed commit, invalidated by any new commit. | R6, R13, R14, R15 |
| 3 | **The builder never touches acceptance.** Acceptance tests live in a protected path owned by product or QA; CI fails if the builder's change touches it, the workflows or the lint configuration; the verifier uses another identity; the builder has no access to future history; weak assertions are rejected. | R4, R16, R17 |
| 4 | **A fresh session per stage**, started from the written record, which keeps decisions, rejected alternatives and next steps. No compaction threshold policy. | R6, R21, R23 |
| 5 | **Product spec separate from technical spec.** Acceptance examples from the product spec become the protected tests. A trivial task may skip the technical spec, never the acceptance examples. | T3, R22 |
| 6 | **Two human decision points**, the spec and the handoff, each with a short summary (what, why, evidence, open items). Reading time is recorded. | T1, R28, R29 |
| 7 | **Evaluators propose; people decide.** No unattended change to the factory definition, prompts or skills. Judges are measured before they are trusted. | T5 (caveat), R24, R25 |
| 8 | **Secure by default.** Configuration read only from the main branch; only registered actors trigger work; no agent-created permission rules; minimal network egress; no write secrets in a process that reads external content. | R26, R27 |
| 9 | **Measure per accepted change, against the current way of working** (a person with an interactive agent), on the same tasks and criteria, from timestamps: human minutes per accepted change (clarify, review, intervene), cycle and waiting time, cost including failed attempts, corrections at 14 and 30 days, reverts, test strength, and whether a fresh session resumed without asking. The 0.5% revert rate from T2 is a reference, not a target. | R11, R12, R18, R19, R20, T2 |
| 10 | **A narrow first version.** One forge, one agent CLI, Markdown memory; no server, database or cloud. A second executor, chat triggers, durable queues, multi-project and unattended self-improvement come later, each with entry criteria. | R6, T5, critical review |
| 11 | **A public kit.** Every infrastructure dependency is an adoption barrier: a team should be able to install it in an afternoon. Open, versioned formats outlast tools. Portability is proven with a public example project anyone can run. | T1, T5 |

**Telar:** decision 11 is settled by [ADR 0008](../decisions/0008-telar-is-a-method-and-framework.md), with woku as the only installation for now. The others are the input of the [`core-definition`](../projects/core-definition/v1/DIAGNOSIS.md) project, which turns them into a catalog of non-negotiables (N-01 onward) for Diego to accept or reject one by one.

## 5. Agreements and tensions

### Where the sources agree

| Theme | Talks | Papers |
|---|---|---|
| Human attention is the scarce resource | T1; T3 to T5 (human touchpoints) | R28, R29 |
| Trust comes from the environment, not the prompt | T2 (pyramid); T1 (push back) | R13, R14, R15 |
| Control belongs in the process, not in final review | T3 (spec review, verification) | R6, R7 |
| Verification is where effort goes, and it must be independent | T2 (70% of tokens); T5 (computer use) | R4, R16, R17 |
| Measure on your own work, by accepted change | T1 (own sessions); T4, T5 (scores, benchmarks) | R11, R12, R18, R19 |
| Written memory makes handoff possible | T1 (summaries) | R21, R22, R23 |
| Automation amplifies the inner loop | T1, T2 | R4, R6 |

### Where they disagree, and where Telar stands

| Tension | One side | Other side | Telar position |
|---|---|---|---|
| Workshop or factory first | T1, T2: foundations first | T3 to T5: the factory is infrastructure every project will have | **Telar:** workshop first, then a minimal line (section 4, decision 1). Lloyd himself calls the full factory overkill for individuals |
| Gardening or engineering | T2: the job is becoming gardening | T4: "not about growing a garden" | **Telar:** both. The codebase is tended; the tending is done with engineered mechanisms |
| Local or cloud | T1: interactive workshop, durable agents | T3 to T5: cloud sandboxes for security and governance | **Telar:** local first (decision 10); cloud is an optional later profile |
| Reading code or reading evidence | T2, T3 to T5: review shrinks to artifacts | T1: people who no longer understand their own systems | **Telar:** evidence replaces line by line review only where trust was earned; the owner must still understand the system |
| Self-improvement | T4, T5: agents open pull requests to the factory | R24, R25: judges are unreliable | **Telar:** evaluators propose, people decide (decision 7) |
| Volume as a signal | T2: thousands of pull requests with a steady revert rate | T1: 141 projects started, 10 to 15 maintained; R18, R19 | **Telar:** volume is not a goal; measure accepted changes and what comes back |

## 6. Quality of the evidence

- Almost all papers are **2025 and 2026 preprints**. Some report submission or acceptance at a venue; that was not verified for each one. Repository studies mostly use open source datasets with 2025 and 2026 agents; figures may not transfer to a small team with private code.
- R20 is a single-author preprint without academic affiliation; it is used only as a hint that confirms R19.
- R12 used early 2025 models, and T1 shows later models reduced corrections. Its value here is methodological.
- The talks are practitioner testimony; T3 to T5 are also commercial material.

## 7. Vendor and tool documentation

Consulted while designing, not as evidence of effect.

| Area | Documents |
|---|---|
| A commercial factory product (Warp Factories) | [Overview](https://docs.warp.dev/factories), [Factory as code](https://docs.warp.dev/factories/factory-as-code/), [Blueprints](https://docs.warp.dev/factories/blueprints/), [Gates](https://docs.warp.dev/factories/blueprints/gates/), [Benchmarks](https://docs.warp.dev/factories/benchmarks/), [Measure and improve](https://docs.warp.dev/factories/measure-and-improve/), [Computer use verification](https://docs.warp.dev/factories/use-cases/computer-use-verification/), [Testing and tuning](https://docs.warp.dev/factories/guides/testing-and-tuning-your-factory/), [Multi-repository](https://docs.warp.dev/factories/guides/multi-repository-factory/), [Self-hosting](https://docs.warp.dev/factories/self-hosting/), [Harness authentication](https://docs.warp.dev/factories/harnesses/authentication/), [Factory MCP](https://docs.warp.dev/factories/factory-mcp/) |
| Agent CLIs in headless mode | Claude Code: [headless](https://code.claude.com/docs/en/headless), [CLI reference](https://code.claude.com/docs/en/cli-reference), [commands](https://code.claude.com/docs/en/commands), [Agent SDK](https://code.claude.com/docs/en/agent-sdk/typescript), [legal and compliance](https://code.claude.com/docs/en/legal-and-compliance). Codex: [auth](https://developers.openai.com/codex/auth/), [non-interactive](https://developers.openai.com/codex/noninteractive/), [app server](https://developers.openai.com/codex/app-server/). OpenCode: [server](https://opencode.ai/docs/server/), [providers](https://opencode.ai/docs/providers/), [API](https://opencode.ai/docs/api) |
| Verification | Playwright: [trace viewer](https://playwright.dev/docs/trace-viewer-intro), [snapshots](https://playwright.dev/docs/test-snapshots), [browsers](https://playwright.dev/docs/browsers), [accessibility testing](https://playwright.dev/docs/accessibility-testing), [Playwright MCP](https://github.com/microsoft/playwright-mcp) |
| Forge, channels and operations | [GitHub App installation tokens](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/generating-an-installation-access-token-for-a-github-app), [Slack Socket Mode](https://docs.slack.dev/apis/events-api/using-socket-mode/), [Google SRE: Managing Incidents](https://sre.google/sre-book/managing-incidents/) |
| Infrastructure considered and deferred | [Terraform](https://developer.hashicorp.com/terraform/intro), [AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html), [pg-boss](https://github.com/timgit/pg-boss), [portable-pty](https://docs.rs/portable-pty/), [xterm.js](https://xtermjs.org/) |

## 8. Prior art: methods and frameworks

Researched on 2026-11-24 to test the definition in [ADR 0008](../decisions/0008-telar-is-a-method-and-framework.md).

| Precedent | What it shows | Effect on Telar |
|---|---|---|
| [Scrum Guide 2020](https://www.scrumguides.org/scrum-guide.html) | A "lightweight framework", "purposefully incomplete", that defines only what its theory requires; teams fill in the rest | Telar's method defines a minimal set of non-negotiables; each workshop models the rest |
| Rails, extracted from Basecamp ([origin story](https://thenextweb.com/news/the-ruby-on-rails-origin-story); DHH, RailsConf 2013) | "Frameworks are not inventions, they're extractions"; the bad features came from inventing ahead of need | Telar is built by serving woku and abstracting from it |
| Roberts and Johnson, [*Patterns for Evolving Frameworks*](https://nzjohng.github.io/publications/papers/EFPL.pdf) | "Three Examples": a framework is generalized from about three applications (the rule of three) | A mechanism or format is declared stable only after more than one installation uses it |
| [GitHub Spec Kit](https://developer.microsoft.com/blog/spec-driven-development-spec-kit) | A project "constitution" of principles and constraints governs spec-driven work | Repository-resident rules are common practice |
| [Kiro](https://kiro.dev/docs/steering/) | Markdown steering rules per workspace, specs per feature, event-driven hooks | Same |
| [BMAD Method](https://github.com/ResourcefulAI/bmad-method) | A method of role-based agents and guided workflows built on a core | "Method plus core" is an established shape |
| [Agent OS](https://github.com/buildermethods/agent-os) | Discovers a codebase's standards from its code and injects them into agent work | Rules can be harvested from the workshop's own code and corrections |
| [AGENTS.md](https://openai.com/index/agentic-ai-foundation/), now in the Agentic AI Foundation (Linux Foundation) | An open format for project instructions | Adopt instead of inventing ([ADR 0004](../decisions/0004-claude-md-canonical-agents-md-symlink.md) already mirrors it) |
| [Agent Skills](https://agentskills.io/) | An open, portable format for skills (`SKILL.md`) | Candidate format for layer 4 of the trust pyramid |
| [Self-hosting compilers](https://en.wikipedia.org/wiki/Bootstrapping_(compilers)) and [dogfooding](https://www.nngroup.com/articles/dogfooding/) | Self-hosting proves a tool works but amplifies its own bugs and needs a trusted previous version; dogfooding biases a product toward its builders' own use cases | Why Telar-for-Telar comes later, and why woku, not this repository, is the primary signal |

**Telar:** in what was found, the agent frameworks keep project rules as repository-resident prose, and some add hooks. None ties each rule to the correction that created it, places it at the layer that enforces it, and measures whether it works. That is the gap Telar's method targets.

## 9. Open questions

- How to measure corrections and human minutes reliably across harnesses.
- Which verification is worth its token cost for which kind of change (T2's 70% is a data point, not a target).
- What evidence each human gate needs so that it is not a rubber stamp.
- When a judge is trustworthy enough to score runs (R24, R25).
- What of the first installation's experience can be published: aggregated metrics only, or anonymized records as well.
- Next screening: R9, R10, and new work on agent review and verification.
