# Research synthesis

The sources that shaped Telar, what each one claims, and where they agree and disagree. Claims are attributed to their speakers, with timestamps (mm:ss) into the talk. Telar's own positions are marked **Telar**. The transcripts live in the separate research repository, not here.

Synthesis date: 2026-11-24.

## Sources

| ID | Talk | Speaker | Link |
|---|---|---|---|
| S1 | Build the Workshop Before the Software Factory | Armin Ronacher (Earendil) | https://www.youtube.com/watch?v=JNexz3Tbiu8 |
| S2 | All Code Is Slop (Except Mine) | Lauren Tan | https://www.youtube.com/watch?v=O_zcc6Xl12g |
| S3 | Software Engineering Is Becoming Factory Engineering | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=tUPPVhBBcoM |
| S4 | Engineer Your Coding Agents Like Any Other System | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=0LeT996Hz3E |
| S5 | How to Build a Software Factory That Improves Itself | Zach Lloyd (Warp) | https://www.youtube.com/watch?v=nKjPBAw_N_0 |

## S1. Ronacher: build the workshop before the factory

The argument: build the atelier, where a skilled person uses powerful tools to make more ambitious and better software, before building the factory.

- **Models improve under a stable harness.** The Pi agent's core harness has the same tools it had a year ago and is far more capable, purely from better models. Plugins he loved (an auto-research loop) are no longer necessary (00:44 to 02:40).
- **His own data.** Corrections he makes per session went down with every model. The P90 time an agent runs per task went from about 2.5 minutes to 14 minutes or more. Agents increasingly prefer Bash; "code mode" is rising (02:40 to 04:24).
- **Humans did not change; attention is the limit.** Prompts per day are flat (120 to 190) while agent active time grew to many times his working day. He started 141 repositories in a year but maintains only 10 to 15 regularly. Starting got easy; maintaining did not (04:36 to 07:10).
- **Attention matters even when automated.** A friend fully automated an open source project (issues in, agent reviews and commits) and later turned it off when he stopped caring about it (07:19 to 07:58).
- **What matters in a workshop.** Knowing when to push back, because the agent is rewarded for completing the goal, not for what we are happy with over time. Avoid the "Simpson car" of features. "True skill versus agent skill": the same tools give very different quality depending on engineering experience (08:01 to 10:08).
- **Stay within understanding.** Moderate speed to stay within what you understand. His technique: around 70% into a session, before verification, the agent writes a short executive summary and a typeset HTML page; this balances that he no longer reads the code in many cases (10:13 to 11:08).
- **Few dependencies, but no uncontrolled growth.** He likes writing more code yourself, but warns of *Wildwuchs*: divergent implementations of the same format (a tar archive read differently by different implementations). Standards, specifications and open formats matter; human collaboration is as hard as ever, and forks replace upstreaming (11:24 to 13:31).
- **Strive for excellence.** Verified software, faster and memory-efficient software, memory-safe languages (13:31 to 14:59).
- **Harness directions.** Durable agents that can suspend, resume and restart themselves, including suspending sandboxes while waiting on cheaper flex-scheduled inference (15:17 to 16:47). Code mode: let the agent write JavaScript that orchestrates tool calls outside the context window, with cheap classifier or decision models at each branch (for example, triaging 3,000 support requests) (16:49 to 19:17).
- **Closing.** "Now that we can build everything, maybe we should not." Push for more enjoyable and more ambitious software (19:21).

## S2. Tan: all code is slop (except mine)

The argument: the meta-skill of engineering is keeping or raising quality while massively increasing output. It is about trust, not blind trust but investment in the agent's environment. She shipped about 3,000 pull requests in a month after six months of that investment (00:12 to 01:56).

- **The inverse pyramid.** Deterministic layers first: the code itself (API design, architecture, refactoring) and static analysis (lint, types, compilers, tests). Then verification (runtime and formal). Then a little prose (rules, skills, AGENTS.md), for what requires judgment (02:03 to 02:59).
- **Corrections become checks.** Whenever you correct the agent, make it a deterministic check rather than another line in the rules; it is reproducible and can be trusted (03:12 to 03:27).
- **The codebase is a garden.** Code now arrives as a continuous stream (in 2024 she reviewed three colleague pull requests when she got to work; today it is more like 300). Constraints are the concrete foundation new code grows around. Workarounds and anti-patterns get copied because they look like the established pattern (03:27 to 04:58).
- **Ban what needs nuance.** Anything that requires nuance to use well leads to slop (example: `useEffect` banned in product code, allowed only inside framework APIs). The problem is categorically eliminated and never needs review again (05:26 to 06:10).
- **Context through directory structure.** Main and renderer process code in two top-level directories, with imports between them banned by a dependency graph analyzer and lint rules (06:10 to 06:56).
- **Prose is an escape hatch.** Agents use Markdown, comments, rules and skills to justify not doing the right thing, and over-rotate small corrections into hard rules. Example: timers used as quick fixes, each justified in a comment, spread until performance suffered. Her team banned 99% of comments and wrote lint rules whose messages point to the root cause (06:56 to 09:10).
- **Nothing left to review.** Do this enough and there is nothing left to look for in code review; agents merge most of their own pull requests (09:10 to 09:40).
- **Review becomes looking at verification artifacts.** Videos, screenshots, diagrams, formal verification (09:40 to 10:02). Runtime verification with the DevTools protocol; a feature map gives agents and humans shared vocabulary; custom CLIs inside skills cut tokens and are testable (10:02 to 10:50). Formal verification with TLA+ for multi-device flows and Lean for algorithms; property-based UI testing (10:50 to 11:51).
- **Tokens go to verification.** About 70% of daily tokens go to verification, for a peer she cites and for her. These are old techniques made economical by agents: "a golden age of software testing and verification" (11:53 to 12:52). A state chart skill makes state machines reviewable from the user's point of view (13:02 to 13:21).
- **Results.** Her team shipped 11,000 pull requests in a month, a stable release about once a day, 227 contributors in a month; the revert rate stayed steady at about 0.5%; performance improved on several dimensions (13:32 to 15:10).
- **Before building a factory.** Correct agents by improving the codebase first; lint to stop new occurrences, then clean up old ones; make verification strong. "If your inner coding loop produces slop, automating that loop just produces more slop" (15:11 to 16:07). Once that is in place, releases trigger an app-wide fuzzing run that opens and auto-merges fix pull requests (16:21 to 16:56).

## S3 to S5. Lloyd: factory engineering

Three talks with one thesis: software engineering is becoming factory engineering. They are combined here.

- **Where we are.** From autocomplete and chat, to interactive agents (today), to automated development. Interactive prompting is bounded by human throughput, hard to cost-control and hard to govern; local agents are a security risk (S4 01:09 to 02:39; S5 01:47 to 03:00).
- **Definition.** "A code-defined, closed loop system for continuously measuring and improving cloud coding agents" (S4 03:44). Not a loose set of automations, not AI teammates, not a shared set of skills and MCPs, not personal agent swarms: those are primitives (S4 03:14 to 03:38).
- **The loop.** Ideas in; triage (if easy and unambiguous, just implement); spec for hard work (a product spec with the invariants and a tech spec with the architecture); human spec review; implementation; agent then human code review, as risk management; verification (computer use, videos, screenshots); human product review; ship; monitor; and back to the top (S3 03:22 to 04:03, 10:03 to 12:02).
- **Components.** Automations, context and skills, humans brought in at the right time (when work gets stuck), and self-improvement loops (S3 07:58 to 08:24).
- **The stack.** Factories as code (Terraform-style: agents, triggers, workflows, MCPs, where agents run; branch, test configurations, roll back, let agents propose changes); a data and context layer that records every conversation and artifact as raw material; compute (sandboxes); inference (models and harnesses as a degree of freedom to test); orchestration; API and MCP first, integrated where work happens (chat, issue trackers, code hosting) (S4 08:09 to 10:40; S5 17:12 to 17:44).
- **Measurement.** Cycle time, level of automation (human interactions per pull request), throughput, cost (S4 12:51 to 13:23). Online evals: LLM-as-judge scores over recorded runs, for example one that flags redundant tests (S5 12:01 to 13:25).
- **Self-improvement.** Agents aggregate failures, look for patterns, and open a pull request against the factory definition ("I saw this fail 37 times") (S5 13:25 to 14:42; S4 15:00 to 15:51). Skill loops: observer agents watch how skills are applied and improve them, for example when senior engineers keep correcting a review agent's comments (S3 14:03 to 14:48).
- **Benchmarks on your own data.** Replay real past tasks against other models and configurations, plot cost against quality, derive a routing strategy; also test removing skills (S5 14:46 to 17:04; S4 15:51 to 17:10). Curate by hand to start (small, medium and hard tasks), or let the factory pick from past sessions (S5 20:10 to 20:47).
- **Two kinds of engineering.** Product engineering (putting work into the factory, owning whether it solves a real problem) and factory engineering (improving skills, context and model mix). The new tools of the trade: evals, loops, benchmarks, A/B tests of the factory (S5 06:55 to 07:51; S4 07:10 to 08:07).
- **Ownership.** Open (any model, any harness), adaptable (works with existing infrastructure), sovereign (own the data, compute and inference) (S5 04:15 to 06:00).
- **Against pull request pile-up.** Spec-driven development plus computer use verification lessen the review burden (S5 18:12 to 18:50).
- **Fit.** Overkill for an individual; valuable from about 10 engineers (S5 21:23 to 21:53). Most organizations should not build scalable factory infrastructure themselves; tuning it to the product is the interesting work (S3 12:04 to 12:51, 17:04 to 17:51).
- **Taste.** Human taste and product sense remain essential; a factory churning out what nobody cares about is pointless (S3 19:12 to 20:12).

## Where the sources agree

| Theme | S1 | S2 | S3 to S5 |
|---|---|---|---|
| Human attention is the scarce resource | Central thesis | Review shrinks to artifacts | Humans at the right touchpoints |
| Trust comes from the environment, not the prompt | Push back; understanding | The inverse pyramid | Specs, verification, scores |
| Corrections are raw material | Corrections per session as a metric | Every correction becomes a check | Failed scores become factory pull requests |
| Verification is where effort goes | Summary before verification | About 70% of tokens | Computer use verification |
| Define it, version it | Standards and open formats | Lint rules as code | Factories as code |
| Measure on your own data | Analysis of his own sessions | Revert rate, performance | Scores and benchmarks |
| Models move; keep the harness thin | Pi unchanged for a year | | Any model, any harness |
| Automation amplifies the inner loop | Maintenance does not scale with starts | Slop in, more slop out | Pull request pile-up |

## Where they disagree, and where Telar stands

| Tension | One side | Other side | Telar position |
|---|---|---|---|
| Workshop or factory first | S1, S2: foundations first | S3 to S5: the factory is infrastructure every project will have | **Telar:** workshop first, factory as stage 3 ([ADR 0006](../decisions/0006-workshop-before-factory.md), proposed). Lloyd himself calls the factory overkill for individuals |
| Gardening or engineering | S2: the job is becoming gardening | S4: "not about growing a garden"; engineer your agents | **Telar:** both. The codebase is tended like a garden; the tending is done with engineered mechanisms (checks, scores) |
| Local or cloud | S1: interactive workshop, durable agents, suspended sandboxes | S3 to S5: move agents to cloud sandboxes for security, governance and cost | Open question |
| Reading code or reading evidence | S2, S3 to S5: review shrinks to artifacts; S1 reads summaries instead of code | S1: people who no longer understand their own systems | **Telar:** evidence replaces line by line review only where trust was earned; the owner must still understand the system (principle 8) |
| Build or borrow | S3: most should not build factory infrastructure | S1: write more yourself, few dependencies | **Telar (proposed):** own the thin workshop (the loom), borrow heavy infrastructure (harnesses, inference, sandboxes). Open until stage 2 |
| Volume as a signal | S2: thousands of pull requests a month with a steady revert rate | S1: 141 projects started, 10 to 15 maintained | **Telar:** volume is not a goal; measure corrections, reverts and attention per change |

## What Telar takes

Each source maps to [principles](principles.md): S1 to 1, 2, 6, 8, 11, 12 and 13; S2 to 2, 3, 4, 5 and 7; S3 to S5 to 9, 10 and 11, and the shape of stages 2 and 3. Principles 14 and 15 are Telar's own working rules.

## Open questions raised by the research

- How to measure corrections reliably across harnesses (S1 used session analysis tooling).
- Which verification is worth its token cost for which kind of change (S2's 70% is a data point, not a target).
- What evidence each human gate needs so that it is not a rubber stamp (S3 to S5).
- When a judge is trustworthy enough to score runs without human calibration (S5 relies on LLM-as-judge and suggests adding human grading).
