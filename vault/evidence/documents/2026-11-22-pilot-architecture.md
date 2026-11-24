# Single-project pilot of the agentic software factory

> **Evidence.** Translated from Spanish on 2026-11-24. Original: "Piloto monoproyecto de la fábrica de software con agentes", single-project pilot architecture, 2026-11-22, kept in the research workspace. Redactions are marked `[redacted: reason]`.

**Current scope.** An installation serves a single software project and the people responsible for it. That project can bring together several code repositories and several vaults. Every event belongs to the installation's project. A versioned configuration lists its resources, permissions, executor and approvers. The [multi-project design](2026-11-22-multi-project-architecture.md) is reserved for a stage after the full cycle has been validated.

**Design proposal · November 22, 2026.** The first run starts from a request in Slack, investigates several repositories, writes its findings to the vault and requests a decision on a specific version. A person can also start the same work item from their local agent. AWS is a reference choice for describing the VPC. The pilot and its costs remain to be tested.

## Proposed adaptation after reviewing Warp Factories

To validate the pilot with less upfront infrastructure, we propose starting with a versioned Blueprint and two small work items from the same product. The first demonstration follows the research, the approval of a specific specification, the implementation and an independent verification. The team can rehearse it with a local executor and test vaults. Managed Warp and our own coordinator are alternatives to compare afterwards against the same case, cost and criteria. [Analysis, prototype and adoption conditions](2026-11-22-warp-factories-and-pilot.md)

## One permanent coordinator and one executor per work item

| Component | Choice for the pilot | Responsibility |
|---|---|---|
| Coordinator | TypeScript, Node.js and Fastify | Receives events, validates the actor's identity, interprets rules, records transitions, requests approvals and returns results to the channel. |
| State and pending jobs | PostgreSQL on RDS and pg-boss | Stores work items, events, attempts and decisions. A transactional outbox records the publication of pending work together with the state change. A dispatcher can retry its delivery by identifier. |
| Executor | Linux container on ECS Fargate, with Git, ripgrep and an agent CLI whose version is pinned in the image | Receives a single work item and a bounded policy. Prepares the multi-repository workspace and returns events, changes and evidence. The executor's role is distinct from the role that administers the infrastructure. |
| Frontend verification | Playwright Test and dedicated Chromium in a QA task | Opens the candidate revision in staging, walks through the user task, compares screenshots and returns the result to the dossier. |
| Infrastructure | Terraform for VPC, subnets, network rules, ECS, ECR, RDS, S3, Secrets Manager, IAM and logs | Reproduces the environment. Secret values are provisioned through a secrets channel; the infrastructure code references their identifiers. |
| Evidence | Markdown and Git for project memory, S3 for attachments, PostgreSQL for process state | A decision links the vault commit that was approved. If a run ends, another one can reconstruct what is known and what is missing. |
| Tracking | Structured events, CloudWatch and traces with OpenTelemetry | The work item identifier ties together queue wait, execution, tools, cost when available, human wait and result. |

In development, the same components can be tested with Docker Compose, PostgreSQL and a local executor process. In the VPC, the coordinator lives as an ECS service and launches an isolated Fargate task per run. The containers need egress to the enabled providers and to GitHub. For a low-volume installation it is also worth estimating the components that are billed while idle, such as the managed database and network egress. [Terraform](https://developer.hashicorp.com/terraform/intro) · [ECS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html) · [pg-boss](https://github.com/timgit/pg-boss)

## From a message to a decision

1. In a thread, the person asks "investigate why the night shift closing differs from the report". The connector identifies the person, the external event and the thread in the configured channel. A unique identifier per provider and event prevents two work items from being created when a retry arrives.
2. The coordinator loads the approved version of the project policy. The rule identifies the allowed sources, the vault repository, the executor type, the deliverable and the decision that product will have to make. The message text supplies the goal. Permissions come from the policy applied by the system.
3. The executor receives the work item identifier and a repository manifest. It syncs the refs and prepares one directory per repository, with the starting revision recorded. It investigates the service, the interface and the earlier decisions in the vault. It can query a read tool when its policy authorizes it.
4. The agent writes the diagnosis and the log to the vault. A publishing component can receive the change, check its paths and create a branch and an integration proposal with a GitHub App. On retry it uses a stable branch per work item and recovers the existing proposal. The report states sources, discrepancy, conclusion and next decision.
5. The coordinator posts the summary in the thread with "approve", "request changes" or "discard". It checks the approver's identity and links the decision to the reviewed commit. A later edit that changes the proposal requires a decision again. A repeated approval produces a single transition. While waiting, the Fargate task can end.
6. After approval, the policy can enable a planning or implementation phase. For each affected repository, the branch, base revision, PR and tested revision are recorded. A combination of changes that has not yet been tested together remains pending in the QA record.

## Visual and UX/UI verification with a browser

For the pilot I would use **Playwright Test with dedicated Chromium**. Woku's QA vault already defines that browser, a staging target, HTML report, screenshots, video and traces in `[redacted: internal woku reference]`. The factory can reuse those walkthroughs from a versioned container. For an issue specific to Google Chrome, the same case can be run with the `chrome` channel; Firefox or WebKit would be added when the product's coverage requires it. [Playwright browsers](https://playwright.dev/docs/browsers)

**When it is triggered.** A change that affects a screen, or a visual issue, enables the QA task when the candidate version is available in staging. The coordinator hands it the work item, the deployed revision, the user scenario, the agreed screen sizes and the approved design reference or screenshot. If the deployment changes during the test, the result remains pending, to be repeated on the corresponding revision.

| Question | How it is checked | What goes back to the dossier |
|---|---|---|
| Can the task be completed? | The agent walks through the flow with Playwright and checks the observable effect. A one-off exploration can use Playwright MCP to navigate, inspect the page and take screenshots; a repeatable finding becomes a versioned test. | Steps, expected and observed state, tested revision and trace of the run. [Playwright MCP](https://github.com/microsoft/playwright-mcp) · [Trace Viewer](https://playwright.dev/docs/trace-viewer-intro) |
| Did the appearance of a relevant screen change? | The same state is prepared with known data and with browser, fonts and viewport pinned. The component or the page is compared against its approved reference using `toHaveScreenshot()`. For a new design, UX/QA reviews the first reference. | Approved screenshot, current screenshot and visual diff. An intentional design change requires approving the new reference before adopting it. [Visual comparisons](https://playwright.dev/docs/test-snapshots) |
| Is the flow understandable and accessible? | It is walked through by keyboard, checking focus, control names and the response to empty states or errors. axe can help detect automatable violations. Design, QA or the responsible person judges whether the user understands the action and its result. | Finding linked to a specific task, severity, evidence and human decision when UX judgment is required. [Accessibility with Playwright](https://playwright.dev/docs/accessibility-testing) |

**Acceptance example.** For an export, prepare test data and walk through the screen on desktop and on an agreed mobile viewport. On both, the person must be able to choose the period, reach the button and get the expected file. If on mobile a fixed bar covers the button, QA attaches the screenshot and the trace, logs the bug and repeats the same case after the fix. The attachments are kept in restricted-access storage and the vault record links the work item, the revision, the environment and the result. Slack receives the summary and the link. Having verified staging and having checked production are different states.

## How to talk to the agent

Each executor adapter translates three common operations: start, add an authorized instruction and cancel. If the CLI only accepts messages at startup, the instruction is saved for a new turn at the next safe boundary. The coordinator keeps the session ID that the provider allows, the last event and the persisted results. When a session lives in ephemeral storage, resuming requires restoring that authorized state or starting a new session with the dossier. [Codex, non-interactive execution](https://developers.openai.com/codex/noninteractive/) · [Claude Code, programmatic execution](https://code.claude.com/docs/en/headless) · [OpenCode, server](https://opencode.ai/docs/server/)

I would start with Node child processes and structured interfaces. The local agent can also call tools on a small factory MCP server: create a work item, check its status, add context and record a decision with an authenticated human identity. A second mode lets a local client request a specific job over an outbound connection, advertise capabilities and deliver its result. Losing the connection expires the job's reservation. The coordinator reconciles the effects already published before retrying and only reassigns if the target has the resources and permissions that the work item needs.

**Where Rust adds value.** A desktop binary that has to be installed on heterogeneous machines, supervise processes and offer an interactive terminal is a good candidate. For that role I would evaluate Tokio and portable-pty, and xterm.js if the session needs to be displayed in the browser. To send work to the pilot, an executor that receives structured data is enough. Input is delivered through stdin, SDK or the provider's API, without interpolating user messages into shell commands. A remote interactive session would be an additional channel, with its own authentication and authorization. [portable-pty](https://docs.rs/portable-pty/) · [xterm.js](https://xtermjs.org/)

### Context control and automatic compaction

Every executor, local or in the VPC, applies the same rule per session: **when the context currently in use exceeds 50% of the model's effective window, it requests compaction before the next work step**. At exactly 50% it continues. If the provider supplies counters, the comparison is `2 × tokens_in_use > effective_window` *(identifiers translated from Spanish)*, with no rounding. The session's accumulated spend and the subscription quota are measured separately.

The adapter checks usage when starting or resuming the session and with every available update, especially after large tool results. On crossing the threshold, the coordinator finishes recording the action in progress, saves a continuity point in the dossier and requests a single compaction at the next safe boundary. The continuity point includes goal, phase, current decisions and approvals, repository revisions, evidence and next pending action. Large attachments are kept by reference.

| Executor | Proposed integration |
|---|---|
| Codex | With App Server, listen for `thread/tokenUsage/updated`, get the current usage and the model's window, call `thread/compact/start` and wait for `contextCompaction` to finish. The initial response only confirms that the request was received. [Codex protocol](https://developers.openai.com/codex/app-server/) |
| Claude Code | The TypeScript SDK exposes `getContextUsage()`; the interactive interface offers `/compact`. For unattended runs, the interface available in the pinned version must be checked. The `--autocompact` option expresses the threshold in tokens and only works for this policy if its limits and its behavior reproduce the agreed rule. [Agent SDK](https://code.claude.com/docs/en/agent-sdk/typescript) · [Commands](https://code.claude.com/docs/en/commands) · [CLI options](https://code.claude.com/docs/en/cli-reference) |
| OpenCode | The API documents `POST /api/session/{sessionID}/compact`. The adapter must check the route and the usage signal in the installed version, and distinguish the acceptance of the request from its completion. [Sessions API](https://opencode.ai/docs/api) |

The coordinator records session, model, previous reading, result and first available subsequent measurement. Duplicate events or a native compaction already in progress are reconciled with the same operation. If the operation fails or the new reading is still above the threshold, a compaction loop is avoided: a new session is prepared with the reduced continuity point, usage is measured again and the same work item is kept. If no reliable measurement is available either, the adapter reports "unknown usage" and leaves the run pending under this policy. A restart preserves both the changes already published and the human decisions that are still pending.

**Proposed acceptance test.** With a window of 100,000 tokens, 50,000 allow the run to continue and 50,001 request a compaction. When that last event is delivered twice, a single operation must be recorded. After confirming a reading below the threshold, the agent must recover the next step from the dossier without repeating the previous action. The test will be run per adapter in the same local or unattended mode that the pilot will use.

## Connector contracts

| Family | Input and output | First implementation |
|---|---|---|
| Channels | Verified message or interaction → internal event with external ID, actor, thread and content. Resolution → reply to the thread. | Slack Bolt with Socket Mode opens an outbound connection. Discord and email can implement the same contract. For email, a reply can provide context; to approve, a single-use link can be opened that also requires a project identity. [Slack Socket Mode](https://docs.slack.dev/apis/events-api/using-socket-mode/) |
| Git and vaults | Repository manifest → local revisions. Authorized change → branch, PR and commit. | GitHub App installed on selected repositories. Separate code reading from publishing; issue installation tokens limited to the repositories and operations of the phase. [GitHub Apps](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/generating-an-installation-access-token-for-a-github-app) |
| Queries | Typed operation with parameters → bounded result and reference to evidence. | Start with a real query to Sentry, PostHog or logs, through SDK/HTTP or an MCP server. Diagnostic scripts use a database identity with read permissions and limits on time and results. Write credentials stay outside the process that runs the query. |
| Agent providers | Work item and context → event stream, result, files and termination reason. | Implement first the provider with authorized access for the chosen mode; add the second against the same acceptance tests. |

The dossier persists stable identifiers. The database records the decision and the transition together. When an external action is repeated, the connector reconciles against GitHub or the channel to avoid duplicating PRs or launching two runs. The process that generates text has no authority to attribute a human approval to itself.

## Pilot and acceptance criterion

First local delivery: a test event, two sample code repositories, one vault, one provider and a versioned diagnosis. Second delivery: real Slack, GitHub App, single-person approval and deliberate repetition of the same event. Third: deploy the same flow in the VPC and add a read query. After that, add a local executor and a second agent provider.

The first proposed test case is a functional issue in Woku. The initial configuration can point to the service, the interface, the engineering vault and the QA vault. Research, diagnosis and approval are demonstrated first. To validate the full cycle, the same work item records the approved plan, the implemented change, the regression test and the result on the version delivered to the authorized environment. The agent writes in the vault what it verified and what remains pending. Before widening the scope, it is worth repeating the flow with another work item from the same product and checking whether a new session can continue from the log.

The pilot is demonstrable if, from a single thread, one can recover the original question, the revisions consulted, the document written by the agent, the person who approved that version and the task that was enabled. Repeating the input event or restarting the coordinator during the wait must preserve a single effective decision. These are proposed acceptance tests.

**Access and cost.** Determine, for each provider, whether the plan allows unattended work in the VPC. Codex documents a subscription for personal access, keys for programmatic flows and Enterprise tokens for authorized automations. Record the pilot's mode and budget, and put the work item on hold if the quota runs out without an authorized alternative mechanism. [Codex authentication](https://developers.openai.com/codex/auth/) · [Hosted Claude Code terms](https://code.claude.com/docs/en/legal-and-compliance)
