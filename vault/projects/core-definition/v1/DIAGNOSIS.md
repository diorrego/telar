# Diagnosis: core-definition v1

## Inspection record

| Field | Value |
|---|---|
| Date | 2026-11-24 |
| Repository | `diorrego/telar`, branch `main`, commit `e5a9d66` (state before this iteration) |
| Evidence | [`vault/evidence/`](../../../evidence/README.md): three research conversations, nine research documents, one prototype, figures; the five talks in [`research.md`](../../../foundations/research.md) |
| Harness and model | Claude Code, claude-opus-5-5 |
| Method | Read the three research conversations in full (Diego's messages, the assistant's answers, and Diego's mid-turn messages) and the research documents listed below; extracted every requirement Diego stated, every decision the research settled, and every contradiction between documents; classified each candidate non-negotiable by level |

## Question

What must Telar's core contain, and only that, so that an agent-assisted workshop can model its own rules across the whole model from research to production and operation? For each element: is it Telar's (the same in every installation) or the project's (in the project's repositories, woku first)? The answer is a definition. No code ([ADR 0005](../../../decisions/0005-documentation-before-code.md)).

## Evidence inventory

Read status is stated honestly: this project exists because an earlier proposal was made without reading all of this (correction [C-0002](../../../qa/corrections/C-0002-shallow-proposal-without-evidence.md)).

| ID | Evidence | Date | Read | Contributes |
|---|---|---|---|---|
| E1 | [Conversation: agentic software factories](../../../evidence/conversations/2026-11-21-agentic-software-factories.md) | 2026-11-21 to 22 | In full | Diego's model: two processes, research before requirements, rules in YAML, channels, isolated always-on agents, vaults as memory, single-project first, browser checks, 50% compaction |
| E2 | [Conversation: critical review](../../../evidence/conversations/2026-11-22-critical-review.md) | 2026-11-22 | In full | Public kit, woku first installation, license, name |
| E3 | [Conversation: AI Engineer talks](../../../evidence/conversations/2026-11-22-ai-engineer-talks.md) | 2026-11-22, 24 | In full | Order "rules, contracts, tests, then workshop, then factory"; human review inside the flow; the factory lives isolated and works where people work |
| E4 | [Literature review](../../../evidence/documents/2026-11-21-literature-review.md) | 2026-11-21 | In full | Research question, working definition, extraction protocol |
| E5 | [Paper (LaTeX)](../../../evidence/documents/2026-11-21-paper-agentic-software-factories.tex) | 2026-11-21 | Structure and summary only | Four operation models; technologies by function. Diego judged it "an advance, but poor" (E1) |
| E6 | [Conceptual framework](../../../evidence/documents/2026-11-21-conceptual-framework.md) | 2026-11-21 to 22 | In full | Lifecycle from need to production; operation processes and their units; four observable conditions; prompt, event and authorization; vault records |
| E7 | [Pilot architecture](../../../evidence/documents/2026-11-22-pilot-architecture.md) | 2026-11-22 | In full | Coordinator, executor, browser verification, compaction policy, connector contracts, acceptance criteria |
| E8 | [Multi-project architecture](../../../evidence/documents/2026-11-22-multi-project-architecture.md) | 2026-11-22 | Partially | Manifest per project, profiles, project isolation (deferred to v1) |
| E9 | [Research guide](../../../evidence/documents/2026-11-22-research-guide.md) | 2026-11-22 | In full | State of the design on 2026-11-22 and open decisions |
| E10 | [Warp Factories and the pilot](../../../evidence/documents/2026-11-22-warp-factories-and-pilot.md), [prototype](../../../evidence/prototypes/warp/factory.yaml) | 2026-11-22 | Partially | Blueprint, gates, workers, benchmarks; natural-language gates in the prototype |
| E11 | [Critical review and version zero](../../../evidence/documents/2026-11-22-critical-review-and-version-zero.md) | 2026-11-22 | In full | The build order is wrong; version zero as hardened workshop plus minimal line; ten findings with literature |
| E12 | [Public kit: model and architecture](../../../evidence/documents/2026-11-22-public-kit-model-and-architecture.md) | 2026-11-22 | In full | Principles P1 to P9, entities, stages and gates G1 to G4, engine, policy compiler, adapters, formats, security, installations, measurement |
| E13 | Talks T1 to T5 ([research.md](../../../foundations/research.md)) | 2026-11-22 | In full | Workshop before factory; trust pyramid; factory as code |
| E14 | Telar foundations and ADRs 0001 to 0009 | 2026-11-24 | In full | Constraints on the answer |

E5, E8 and E10 are finished in phase 1 of the plan.

## What Diego has stated

These are requirements in the owner's words (translated), and they outrank any document written from them.

| ID | Statement | Source |
|---|---|---|
| R1 | A software factory has a creation process, from requirement to production, and another process that resolves failures once the software is in production. | E1, 2026-11-21 23:25 |
| R2 | Research comes before agreeing requirements; good research can change requirements preconceived from experience or domain knowledge. | E1, 23:51 |
| R3 | The person's instructions should be programmed in CI/CD or common languages (for example a YAML file) so agents take them or receive them through events: autonomy with the human present through the instructions they leave. | E1, 23:51 |
| R4 | People approve changes; usually teams of two or more, and the one-person case must count too. | E1, 23:51 |
| R5 | Prompts and events arrive where people live: Slack, Discord, email, the coding agent. | E1, 23:51 |
| R6 | Agents always available in an isolated environment (for example a VPC) running Claude Code, Codex or OpenCode under these rules; monitored for agent performance and human interaction; able to connect to local agents for specific tasks. | E1, 23:51 |
| R7 | Read-only access to logs, Sentry, PostHog, MCPs, CLIs, and scripts that query databases; versioning on GitHub; code repositories and vaults always up to date so agents can grep them. | E1, 23:51 |
| R8 | Prefer subscriptions over API billing. | E1, 23:51 |
| R9 | Vaults document how work is done (logs, plans, bugs, how they are solved and verified); agents search them for past decisions and also write in them. | E1, 2026-11-22 00:16 and mid-turn |
| R10 | The agent has access to several repositories, both code and vaults. | E1, mid-turn |
| R11 | Single-project first; multi-project once the factory is polished. | E1, mid-turn 00:24 |
| R12 | Visual frontend checks for UX and UI in a browser. | E1, 11:01 |
| R13 | Check context usage and compact above 50%. | E1, 11:05 |
| R14 | Woku uses it, but the repository is public so other people and companies build their own factories; Diego maintains it. | E2, 20:49 and 21:02 |
| R15 | The order is: rules, contracts, tests; then the workshop; then the factory. | E3, 2026-11-24 09:29 |
| R16 | The human review must be inside the flow; HTML or artifacts with diagrams speed it up. | E3, 09:55 |
| R17 | The agentic software factory lives in an environment isolated from your machine and interacts where people work. | E3, 09:55 |
| R18 | Telar is a method and framework any agent-assisted workshop uses to model its own rules. It serves woku first, keeps abstracting from woku, and Telar-for-Telar comes later. | This session, [ADR 0008](../../../decisions/0008-telar-is-a-method-and-framework.md) |
| R19 | The first project defines the structure of core: its non-negotiables, ordered, separating the repository level (the project, woku first) from the Telar level, across the model from research to production. Core is code; nothing goes there before this is defined. | This session |

## What the research already settled

From E11 and E12, each backed by the literature in [`research.md`](../../../foundations/research.md), section 4:

- Version zero is a hardened workshop plus a minimal line: one forge (GitHub), one agent CLI, Markdown memory, no server, database or cloud (E11 §4, E12 §1).
- Gates are code; agents propose, code and people decide (E12 P1).
- The builder never touches acceptance; the verifier is another identity (E12 P3, G2, G3).
- State lives in Git and the forge; the readable state file is a cache (E12 P4).
- A fresh session per stage with context from the dossier (E12 P5), which contradicts R13 (see C2).
- Rigor proportional to risk: light, standard and strict lines (E12 P6).
- Formats before tools, versioned from day one (E12 P7).
- Secure by default (E12 P8, §7).
- Measure against the current way of working (E12 P9, §10).
- Two human decision points, spec and handoff, each with a summary (E11 §2.8).
- Evaluators propose; people decide; judges are measured first (E11 §2.6).

## The process model

### Creation: one work item from need to production

E6 defines the stages; R2 added research; E1 (23:33) set the rule that every stage must state three things: what the system may decide, what a person keeps, and what evidence lets work advance. E12 implemented only part of it in version zero.

| E6 stage | Version zero line (E12) | Gap |
|---|---|---|
| Intake: a need, an observation or an imagined solution | An issue; `triage` classifies trivial or ambiguous | Other intake channels (R5) come later |
| Research | No stage of its own; the `spec` agent reads the issue, specs and code | R2 requires research with its own output before requirements (G2) |
| Agree the requirement | `spec`: product spec with invariants and acceptance examples; gate G1, approval on the exact revision | Covered |
| Design and plan | Technical spec inside `spec` | Covered in part |
| Build and integrate | `build`: fresh session, protected paths; gate G2 | Covered |
| Verify and validate | `verify`: verifier identity, acceptance tests, browser; gate G3 | Validation by a domain person (does it serve the real task?) is not modeled (G4) |
| Release and check in production | `handoff`: summary and human merge, gate G4; follow-up measures corrections at 14 and 30 days | Deploy and verification in production are outside the line; "done" means merged, not verified in production (G3, C10) |

### Operation: what happens after delivery

E6 and R1 define four processes, each with its own outcome unit. None is in version zero.

| Process | Starts when | Unit of outcome |
|---|---|---|
| Daily operation | A service is in use | Availability during the observation window |
| Incident response | A degradation blocks work | Service restored (a rollback may be enough) |
| Corrective maintenance | A defect needs a permanent change | Change verified in production |
| Evolution | Use reveals a new need | A new requirement delivered and validated |

### Maturity: how a workshop grows

Four sequences exist and must become one (G6):

| Source | Sequence |
|---|---|
| R15 (Diego) | Rules, contracts, tests; then the workshop; then the factory |
| E3 (assistant's reply to R15) | The workshop seen from two sides (technical: Tan; human: Ronacher), then the factory (Lloyd); a cycle, since what the factory learns returns to the workshop as new rules |
| [ADR 0006](../../../decisions/0006-workshop-before-factory.md) (proposed) | Workshop, loop, factory |
| E12 roadmap | v0 (workshop and minimal line), v0.x (second adapter, issue-comment channel, runner in CI), v1 (service, Slack, VPC profile, multi-project, self-improvement) |

## Contradictions between sources

| # | Topic | Position A | Position B | Status |
|---|---|---|---|---|
| C1 | Where it runs | Always-on, isolated environment, reachable from people's channels (R6, R17, E6, E7) | Version zero runs locally from a CLI; the cloud is an optional later profile (E11 §5, E12) | Open: compatible if staged, but the stage and criteria are undecided |
| C2 | Context | Compact above 50% (R13, E7) | A fresh session per stage, no threshold; no fixed threshold works for every task (E11 §2.5, CompAct-Bench) | Open: needs Diego's decision |
| C3 | Gates | Natural-language conditions evaluated by a model (E10 prototype) | Code and the forge decide (E11 §2.2, E12 P1) | Settled by E11 and E12 unless Diego reopens it |
| C4 | State | PostgreSQL and a queue (E7) | Git and the forge, no database (E12 P4) | Settled for version zero |
| C5 | First channel | Slack (E7) | CLI; issue comments in v0.x; Slack in v1 (E12) | Settled for version zero; R5 is the long-term target |
| C6 | Scope | Multi-project (E8) | Single-project (R11, E7) | Settled: single-project first |
| C7 | Executors | Three providers (E7) | One in version zero (E11 §2.10, E12) | Settled for version zero |
| C8 | Proof of portability | A public example project as second installation (E11 §5, E12 §8) | Only woku for now (R18) | Settled by Diego: only woku; Telar keeps abstracting |
| C9 | Names in formats | `obrador/v0alpha1`, `OB-<n>`, `.obrador/` (E12) | The project is named Telar | Rename needed |
| C10 | When work is done | Merged (E12, G4) | Verified in production (E6 units, R1; Telar's project stage 8) | Open |
| C11 | Research stage | Not in the version zero line (E12) | Required before requirements (R2, E6) | Open |
| C12 | Telar developed with Telar | Desirable (E11 §5) | Later (R18) | Settled: later |

## Levels: Telar or project

R19 asks to separate the repository level from the Telar level. The evidence shows that two levels are not enough, because many elements are a Telar mechanism filled with project values. Proposed taxonomy:

| Level | Meaning | Example |
|---|---|---|
| **T**: Telar invariant | Defined and enforced by Telar; identical in every installation; not configurable | The builder's change cannot touch the acceptance path |
| **M**: Telar mechanism, project values | Telar defines the mechanism and its format; each project supplies the values | Risk paths and the line each one requires |
| **B**: project baseline | Each project repository must have it for Telar to work; Telar states the minimum and checks that it exists; the project implements it | CI workflows, branch protection, CODEOWNERS, lint, tests |
| **P**: project only | The project's own rules and content; Telar provides only the method to model them | Woku's domain lint rules; woku's feature map |

## Candidate non-negotiables

Each row: the statement, its level, where it is enforced, its sources, and whether the evidence settles it. Phase 2 of the plan turns this into a catalog Diego accepts or rejects row by row.

### Authority and gates

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-01 | Every transition with effects (start building, merge, deploy) is decided by code or an authenticated person, never by generated text | T | Engine, forge | E11 §2.2, E12 P1, R6 in research.md | Settled |
| N-02 | An approval is bound to the exact revision; a new commit invalidates it | T | Forge (dismiss stale approvals) | E11 §2.2, E12 G1 | Settled |
| N-03 | Who approves what: roles (product, QA, maintainer), counts per line, and the one-person case as two separate moments | M | Manifest, CODEOWNERS | R4, E6, E12 | Settled (mechanism) |
| N-04 | Only registered actors trigger agent work; external contributions need a maintainer's label | T rule, M actors | Engine | E12 §7 | Settled |
| N-05 | Agents never create persistent permission rules; the allowlist is versioned and owned by the maintainer | T | Policy compiler, CODEOWNERS | E11 §2.7 | Settled |

### Acceptance independent of the builder

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-06 | Acceptance tests live in a protected path owned by product or QA | T rule, M paths and owners | CODEOWNERS, CI check | E11 §2.3, E12 P3 | Settled |
| N-07 | The builder's change cannot touch acceptance, CI workflows, lint configuration, the manifest or agent instructions | T | CI check, session policy | E12 G2 | Settled |
| N-08 | The verifier is a separate identity without write access to code; a verification counts only when that identity publishes it | T rule, B identity | Forge status | E12 G3, §5.4 | Settled |
| N-09 | The builder works without access to future history or hidden tests | T | Executor setup | E11 §2.3 | Settled |
| N-10 | Tests without an oracle are rejected (assertion check or light mutation testing) | T check, M thresholds | CI check | E11 §2.3 | Settled |

### The workshop's rules as code

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-11 | A project's standing instructions live in a versioned manifest, not in prompts | T format, P content | Engine | R3, E6, E12 §6.1 | Settled |
| N-12 | Agents read configuration, instructions and skills only from the default branch | T | Engine | E11 §2.7 | Settled |
| N-13 | Every correction to an agent is recorded and encoded at the lowest layer that prevents it: architecture, check, verification, skill, rule | T method, P resulting rules | Process, corrections ledger | R15, T2, principle 4 | Settled as method; format open (G1) |
| N-14 | Domain rules (lint rules, architecture boundaries, banned APIs) belong to the project | P (tooling: B) | Project CI | E11 phase 0, T2 | Settled |
| N-15 | Agent instruction files are short, prescriptive, and checked for stale paths and commands | T check, P content | CI check | E11 §2.2 | Settled |
| N-16 | Rigor proportional to risk: the line (light, standard, strict) is the stricter of the agent's proposal and what the touched risk paths require | M | Engine | E12 P6 | Settled |
| N-17 | Call-outs inject guidance under conditions and never block | M | Engine | E12 | Settled |

### Memory and handoff

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-18 | Each work item has a dossier: product spec, technical spec, log, decisions, verification, summary, run records | T format, B location | Format validation | E12 §6.2, R9 | Settled |
| N-19 | Agents read the project memory when they start and write as they go: findings, plan, decisions, discarded attempts, verification | T method | Process, handoff test | R9, E6 | Settled |
| N-20 | Handoff test: a fresh session that reads only the dossier and the repositories can state where the work item is and what comes next | T | Conformance test | E12, E6 | Settled |
| N-21 | Context policy: a fresh session per stage, or compaction above a threshold | T | Executor adapter | R13 vs E11 §2.5 | Open (C2) |
| N-22 | A work item may span several repositories and vaults of one project; the manifest lists them | M | Manifest | R10, E6, E7 | Settled |

### Verification and evidence

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-23 | Verification produces artifacts tied to a revision and an environment, and states what it proves and what it does not | T format, P flows | Format validation | E7, E12, T2 | Settled |
| N-24 | User interface changes are verified in a browser; visual baselines are approved by a person | M (adapter: B) | Verifier | R12, E7 | Settled as direction |
| N-25 | The verifier uses a feature map of the product | P content, T format | Verifier | E11 phase 0, T2 | Open (format) |
| N-26 | Every human decision point receives a short summary (what, why, evidence, open items) as HTML or an equivalent artifact; reading time is recorded | T | Engine | R16, T1, E11 §2.8 | Settled |
| N-27 | At least two human decision points: the spec and the handoff | T minimum, M more | Engine, forge | E11 §2.8, E12 | Settled |

### Coverage of the lifecycle

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-28 | Research is a stage before agreeing the requirement, with its own output (sources, assumptions confirmed or contradicted, open questions), and it may end in not building | T | Engine | R2, E6, iReDev | Open (C11) |
| N-29 | Product spec (invariants and acceptance examples, long-lived) is separate from the technical spec (disposable); acceptance examples become the protected tests; trivial work may skip the technical spec, never the acceptance examples | T | Engine, CI | E11 §2.9, T3 | Settled |
| N-30 | Triage classifies trivial or ambiguous work | T | Engine | E12, T3 | Settled |
| N-31 | "Done" means verified where the software runs | T vocabulary, B deploy path | Engine, process | E6, R1 | Open (C10) |
| N-32 | Incident response, corrective maintenance and evolution are distinct processes with their own units and closing criteria | T model | Engine (later) | R1, E6 | Open (not in version zero) |
| N-33 | Operational sources (logs, error tracking, analytics, databases) are read-only, including agent-written scripts; write credentials never live in a process that reads external content | T policy, P connections | Executor identity | R7, E6, E11 §2.7 | Settled as policy; later stage |

### Measurement

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-34 | Measure per accepted change against the current way of working (a person with an interactive agent), on the same tasks and criteria, from timestamps rather than self-reports | T protocol, P data | Report | E11 §4, E12 §10 | Settled |
| N-35 | The metrics: human minutes (clarify, review, intervene), cycle and waiting time, cost including failed attempts, corrections at 14 and 30 days, reverts, human commits inside agent changes, test strength, handoff success | T definitions | Report | E11 §2.4, E12 §10 | Settled |
| N-36 | The factory observes its own work: triggering event, policy version, executor, sources consulted, decisions requested, queue, execution and human-wait time | T | Run records | E6, R6 | Settled |

### Security, execution and state

| ID | Statement | Level | Enforced by | Sources | Status |
|---|---|---|---|---|---|
| N-37 | Secure defaults are on: configuration from the default branch, registered actors, no agent-created permission rules, minimal network egress, no write secrets near external content, a `SECURITY.md` with a threat model | T | Engine, docs | E12 §7 | Settled |
| N-38 | Executors sit behind an adapter contract (start, stream events, cancel, capabilities, policy, budget) with a conformance suite; one executor in version zero | T contract, P choice | Conformance suite | E12 §5.3 | Settled |
| N-39 | Each stage has a budget (attempts, minutes, tokens); when exhausted, the work item is blocked with a reason | T mechanism, M values | Engine | E11 §4 | Settled |
| N-40 | Subscriptions are preferred where the provider allows the execution mode; moving to usage billing is an explicit budget decision | P policy | Process | R8, E6, E7 | Settled as preference |
| N-41 | Work runs in an isolated environment, always available and reachable from people's channels | T target | Deployment profile | R6, R17 vs E11 | Open (C1) |
| N-42 | State lives in Git and the forge; the readable state is a cache recomputed from facts; the forge wins on conflict | T | Engine | E12 P4 | Settled for version zero |
| N-43 | Open formats with a schema version from day one and English field names | T | Format validation | E12 P7, §6 | Settled; names to change (C9) |
| N-44 | Re-running never duplicates effects: deterministic branch names, change markers, commit trailers | T | Engine | E12 §5.1 | Settled |

## The project baseline: "YAML, lint, tests"

What any project repository (woku's first) must provide for Telar to work. Telar states the minimum and checks that it exists; the project implements it.

| ID | The repository provides | Supports |
|---|---|---|
| B-1 | CI workflows (YAML) that run the required checks on every change | N-07, N-10, N-15 |
| B-2 | Branch protection on the default branch: required checks, required review, stale approvals dismissed | N-01, N-02 |
| B-3 | CODEOWNERS covering acceptance paths, CI configuration, lint configuration, the manifest and agent instructions | N-03, N-05, N-06 |
| B-4 | Lint and type configuration, where the project's domain rules live | N-13, N-14 |
| B-5 | A test suite that runs in CI, and a protected acceptance path | N-06, N-10, N-29 |
| B-6 | Short, prescriptive agent instruction files | N-15 |
| B-7 | A memory location (a vault repository or a path) for dossiers and logs | N-18, N-19 |
| B-8 | A verifier identity separate from the builder | N-08 |
| B-9 | For products with a user interface: browser verification and a feature map | N-24, N-25 |
| B-10 | A release path observable enough to verify work in production | N-31 |
| B-11 | The manifest, declaring repositories, memory, actors, acceptance, risk paths, lines, stages and call-outs | N-03, N-11, N-16, N-22 |

Woku's practice already includes CI in its repositories, iteration plans with a diagnosis and a phased checklist, bug notes with expected and actual behavior and reproduction steps, and browser QA runs. Its gap analysis against this baseline is done in woku's private vault, not here: this repository is public and keeps only the abstraction (R18).

## What no evidence defines yet

| ID | Gap |
|---|---|
| G1 | How a project models its own rules: what a rule record contains (origin, layer, enforcement point, owner, evidence of effect) and its lifecycle from correction to retirement. This is the center of R18 and nothing in the research defines it |
| G2 | The research stage: inputs, outputs and gate (N-28) |
| G3 | Release, verification in production and the operation processes inside the line (N-31, N-32) |
| G4 | Validation by a domain person, as distinct from verification |
| G5 | The project baseline as a checkable specification |
| G6 | One maturity sequence |
| G7 | Approval rules for teams of two or more versus one person |
| G8 | Telar names for formats and identifiers (C9) |

## Withdrawn hypothesis

The first commit created seven subfolders in `core/` (`checks`, `verify`, `skills`, `rules`, `agents`, `workflows`, `evals`) with contracts, derived from the talks alone and without this evidence. They are withdrawn by [ADR 0008](../../../decisions/0008-telar-is-a-method-and-framework.md) and remain in git history (commit `e5a9d66`). What survives as input: the trust pyramid ordering (now N-13) and the separation between workshop elements and loop elements.

## Constraints

- [ADR 0002](../../../decisions/0002-english-everywhere.md): English. [ADR 0003](../../../decisions/0003-vault-and-core.md): vault and core. [ADR 0005](../../../decisions/0005-documentation-before-code.md): no code. [ADR 0007](../../../decisions/0007-license-apache-2.md): Apache-2.0. [ADR 0008](../../../decisions/0008-telar-is-a-method-and-framework.md): method and framework; woku first; keep abstracting.
- Principles 3, 4, 9, 11, 12 and 14 in [`principles.md`](../../../foundations/principles.md).
- Public repository: woku specifics stay in woku's private vault.

## Unknowns

| ID | Unknown | How it will be resolved |
|---|---|---|
| U1 | Which executor woku may run headless under its subscription terms | Diego (E11 §7, question 4) |
| U2 | Who owns acceptance paths and product specs in woku | Diego (E11 §7, question 5) |
| U3 | Which woku work items enter the comparison | Diego, when measurement is planned |
| U4 | What woku authorizes to publish as a reference case | Diego (E12 §13) |
| U5 | Details in E5, E8 and E10 not yet read in full | Phase 1 of the plan |
