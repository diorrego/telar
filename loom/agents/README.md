# agents

**Stage 2, loop. Empty until the workshop stage meets its exit criteria ([ADR 0006](../../vault/decisions/0006-workshop-before-factory.md)).**

Declarative definitions of the agents that run the steps of the development loop.

## Belongs here

- One definition per agent: role (triage, spec, implement, review, verify, monitor, observer), model, harness, tools and MCP servers, permissions, prompt, and where it runs.

## Does not belong here

- The order in which agents run: `workflows/`.
- How agents are judged: `evals/`.

## Contract

- Model and harness are parameters, not assumptions: any agent can be re-run with another model or harness to compare.
- Permissions are explicit and minimal.
- No secrets in definitions; secrets are referenced by name.

## Open questions

The definition format; which harnesses are supported first; local, cloud or both.
