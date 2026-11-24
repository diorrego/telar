# An agent factory for different software projects

> **Evidence.** Translated from Spanish on 2026-11-24. Original: "Una fábrica de agentes para distintos proyectos de software", multi-project design, 2026-11-22, kept in the research workspace. Redactions are marked `[redacted: reason]`.

**Future exploration · November 22, 2026.** The active stage is the [single-project pilot](2026-11-22-pilot-architecture.md). This proposal will be resumed after polishing how the factory works in that first project.

The unit of configuration is the project. The unit of execution is the work item. A project may start with a question and one person, span several repositories, or deliver a library, an installed application or a service in production. Each work item keeps the project's identity from the event that starts it to the evidence that allows it to be closed.

## Three decisions with different owners

| Level | Who configures it | What it decides |
|---|---|---|
| Factory installation | Whoever operates the platform | Where the coordinator runs, which providers and connectors are installed, how people and executors authenticate and which global limits apply. Terraform, AWS and PostgreSQL are possible choices for an installation. |
| Project | Its owner or team | What is built, who can decide, which sources, repositories and vaults are shared, which channels and executors are enabled, what cost is authorized and what delivering means. |
| Work item | Triggered by a person, an event or a schedule covered by the policy | What result is sought now, from which channel, with which policy version and sources, what evidence was produced and what the next decision is. |

The coordinator resolves identity and project, retrieves state, dispatches work according to capabilities, persists results and verifies the authority behind each transition. Research, implementation and operation can use different recipes on that same core. The dossier distinguishes "diagnosis approved", "change integrated", "package published" and "service verified in production". Only the output for which evidence exists is declared.

## What the project declares

We propose a versioned manifest. To start, it is enough to identify the project and its owner, and to indicate where work comes in, where to keep memory and what result can be accepted. A reusable profile, for example research, corrective maintenance or library delivery, provides initial values. The manifest can live in a factory configuration repository when the project still has no code. References to identities, resources and connectors point to a catalog of the installation. Whoever administers the project can only enable connections that have been granted to them.

This illustrative example shows two projects in the same installation. The identifiers are project-scoped. The rules express maximum permissions per phase and the outputs that an approval enables. The catalog resolves the provider and the authentication details of each resource.

```yaml
version: 1
projects:
  - id: existing-product
    owner: product-team
    input: slack-product
    executor: vpc
    resources:
      - {id: service, type: code, connection: git-service}
      - {id: interface, type: code, connection: git-interface}
      - {id: engineering, type: vault, connection: git-engineering}
      - {id: qa, type: vault, connection: git-qa}
      - {id: errors, type: telemetry, connection: errors-read}
    flow: research-issue
    research:
      read: [service, interface, engineering, qa, errors]
      annotate: [engineering, qa]
    output: diagnosis-with-evidence
    approval: {role: product-team, enables: plan-fix}

  - id: new-library
    owner: maintainer
    input: local-cli
    executor: local
    resources:
      - {id: brief, type: document, connection: project-folder}
      - {id: memory, type: vault, connection: managed-memory}
    flow: research-need
    research:
      read: [brief, memory]
      annotate: [memory]
    output: interface-proposal-with-examples
    approval: {role: maintainer, enables: plan-prototype}
```
*(Identifiers translated from Spanish.)*

The second project can register its first repository later. To distribute a version of the library, it can enable a package registry, a publishing identity and an installation test in a sample consumer. It does not need to invent a production environment or an on-call shift to join the factory.

## How a project is onboarded

1. **Register the identity, the owner and the memory destination.** It can be an existing vault, a versioned folder in the project's own monorepo or a space managed by the factory. A single person can request and approve if the project policy allows it.
2. **Link resources and the input channel.** The owner chooses among connectors that are already installed. A dedicated channel can have a default project. In a shared channel or in the CLI, the project is selected explicitly. An ambiguous request stays pending until it is clarified.
3. **Validate the manifest and simulate a work item.** The system checks references, permissions, the availability of a compatible executor and the evidence destination. The simulation shows what it would read, where it would write, whom it would ask and what that answer would enable. If a capability is missing, it identifies the resource needed.
4. **Run a first bounded research pass.** The agent records what it consulted, writes the result to the project's memory and requests the corresponding decision. The result stays associated with the versions actually used. New resources, permissions or delivery types are added when the scope expands.

## How independence between projects is implemented

- **Events and conversations.** The connector turns a delivery from Slack, email, Git or the CLI into an event with installation, project, actor, external identifier and reply reference. Before dispatching, the link between identity, channel and project is validated. Retries retrieve the same work item.
- **State and memory.** The identities of work items, queries, approvals, budgets and evidence are resolved within the project. The database and the storage apply that scope on reads as well. Each run gets an isolated directory. A shared resource, such as an internal library or a common vault, is granted explicitly to each project with its permissions.
- **Capabilities and adapters.** The flow requests operations such as reading a revision, querying signals, writing a note, running a test or publishing a package. Each adapter announces which operations it supports and returns the result, the version and the evidence. A new tool of the same type requires an adapter and contract tests. A new domain activity, such as validating an application on a physical device, may also require a new capability and a compatible executor.
- **Policy and approvals.** The input message expresses intent. Effective authority comes from the current permissions of the installation, the project, the actor and the phase. The approval record links project, work item, action and artifact version. An earlier approval does not enable another version or destination. If a permission is revoked during a wait, it is checked again on resumption.
- **Capacity and costs.** The policy assigns concurrency, budget and the allowed provider modes. A queue with per-project quotas lets a large batch leave capacity for the others. When its quota runs out, the project keeps its pending work. The installation can share the coordinator and dedicate executors or a separate network to projects that require it.

## What to test before calling the design reusable

| Scenario | Acceptance signal |
|---|---|
| Existing product with several repositories and one team | From Slack, a diagnosis is retrieved that cites the revisions of the service and the interface, the log is written and the owner enables planning of the fix. |
| New library, one maintainer and no initial code | From the CLI, the brief is researched, examples are saved in the managed vault and the maintainer can approve the prototype. Onboarding only uses configuration and capabilities that are already installed. |
| Two simultaneous projects | A search, a token, a reply to the thread or an approval from the first project does not allow reading or modifying the second. Shared resources only appear with the declared grant. |
| Retry or interruption | Repeating an event or restarting the executor keeps a single effective transition and makes it possible to retrieve the correct dossier. |

These are proposed acceptance tests. The [technical pilot](2026-11-22-pilot-architecture.md) specifies an initial installation, and the [conceptual framework](2026-11-21-conceptual-framework.md) describes the factory's responsibilities.
