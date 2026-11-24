# Agentic software factory

> **Evidence.** Translated from Spanish on 2026-11-24. Original: "Fábrica de software con agentes", entry guide, 2026-11-22, kept in the research workspace. Redactions are marked `[redacted: reason]`.

**Status as of November 22, 2026.** The active stage is designing and validating a **single-project, multi-repository** factory. A single work item can span the code of a service, an interface and the engineering and QA vaults. Woku is the first proposed case. The architecture and the acceptance tests are documented. Their execution and costs remain to be validated.

## What model we are building

A person or a team delegates a goal. The factory starts by researching the need with documents, domain knowledge, code, authorized data and relevant public sources. The research may change the requirement or justify archiving it. Once what to build has been agreed, the factory coordinates design, implementation, verification and delivery. When the software goes into use, it distinguishes three results with different evidence: restoring service, verifying a permanent fix and delivering an improvement. [Conceptual framework and the daily cash closing example](2026-11-21-conceptual-framework.md)

The difference from a coding assistant appears between stages. An event covered by a versioned policy can start or resume the work item. The system keeps the version of the proposal, the evidence and who has the authority to decide. A person may reserve the approval of a requirement, an architecture decision or the expansion of a deployment. [Current diagram of research, delivery and operation](../figures/2026-11-21-agentic-factory-research-and-operation.svg) · [Traditional reference model](../figures/2026-11-21-traditional-software-factory.svg)

## How the pilot would operate

| Decision | Proposed scope |
|---|---|
| Input and rules | A first channel in Slack and one identifier per work item. Rules in YAML or in code determine which event allows researching, writing a diagnosis or requesting an approval. Discord, email and the local CLI are planned channels. |
| Execution | A coordinator available in the cloud receives the work. A bounded executor acts on the work item. The local agent can be an input channel or execute a task that requires resources on the person's computer. |
| Repositories and vaults | The agent syncs the authorized sources and records the inspected revision. It writes the findings, the plan, the decisions and the log to the vault. When it fixes a bug, it links the change and notes which test it ran, in which environment and with what result. |
| Access and approval | Queries to logs, Sentry, PostHog or databases are set up as read-only, including from scripts. Publishing changes uses separate permissions. A human approval identifies the authorized version and action. |
| Candidate technologies | TypeScript, Node.js and Fastify for the coordinator; PostgreSQL and pg-boss for state and queue. Docker Compose for the first local run. Terraform and ECS Fargate as the reference for the VPC. Rust remains an option if the local client needs to handle an interactive terminal. |
| Visual QA of the frontend | Playwright and Chromium walk through flows in staging and compare screenshots by screen size. The vault keeps the tested revision, the result and the UX decision when applicable. [Visual and UX/UI verification](2026-11-22-pilot-architecture.md#visual-and-uxui-verification-with-a-browser) |
| Agent context | When a session exceeds 50% of its effective window, the executor saves its progress and compacts before the next step. [Policy and test per provider](2026-11-22-pilot-architecture.md#context-control-and-automatic-compaction) |
| Tracking and cost | Distinguish execution time, queue time and human waiting time. Record cost and rework per accepted delivery. The preference is a subscription that the provider allows for the planned execution mode. |

The connector contracts, the invocation of Claude Code, Codex or OpenCode, event deduplication and recovery after an interruption are developed in the [pilot architecture](2026-11-22-pilot-architecture.md). The conceptual framework documents the practices observed in Woku's vaults and how to carry them over to agent work in the VPC. [Engineering and QA practices](2026-11-21-conceptual-framework.md#the-vault-as-memory-that-agents-also-write)

The [comparison with Warp Factories](2026-11-22-warp-factories-and-pilot.md) proposes trying out a [support agent Blueprint](../prototypes/warp/factory.yaml) before choosing the pilot's control plane.

## How we will know it works

The first proposed milestone is to research a functional issue in Woku. The evidence must be traceable from the initial message to the result. The QA record distinguishes a fix located in a branch from a fix that has actually been tested.

| Milestone | Expected evidence |
|---|---|
| Research and decision | A request produces a diagnosis with sources, revisions and open questions. The agent writes it to the vault. The human decision on that version is recorded in the thread. |
| Verifiable delivery | The approved plan links the changes in the repositories involved, the regression test and the result in the authorized version and environment. Pending checks are made explicit. |
| Recovery and handoff | A duplicate event or a restart during the wait keeps a single effective decision. A new session can continue from the dossier and the vault without reconstructing the chat. |
| Repeatability | The team repeats the cycle with another work item for the same product. That experience makes it possible to decide what to polish before resuming the multi-project design. |

**Open decisions for implementation:** select the initial issue, identify the specific repositories and permissions, agree on who approves each transition, choose the first agent provider and check the authentication mode, quota and cloud budget. The environment in which the delivery is verified must be recorded in the work item record.

## Research and history

- [Initial literature review](2026-11-21-literature-review.md). Six annotated readings and an [original figure from the literature](../figures/2026-11-21-pavlenko-cycle.png).
- [Paper in PDF](2026-11-21-paper-agentic-software-factories.tex) and [LaTeX source](2026-11-21-paper-agentic-software-factories.tex). An integrative review of models, technologies and evidence. The paper predates the detailed formulation of the pilot. [Paper diagrams](../figures/2026-11-21-paper-diagrams.png)
- [First version of the agentic model](../figures/2026-11-21-agentic-software-factory.svg). Precedent of the current diagram, which added research before the requirements agreement.
- [Multi-project exploration](2026-11-22-multi-project-architecture.md). It will be resumed after polishing and validating the factory for one project.
