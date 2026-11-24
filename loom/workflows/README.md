# workflows

**Stage 2, loop. Empty until the workshop stage meets its exit criteria ([ADR 0006](../../vault/decisions/0006-workshop-before-factory.md)).**

The development loop defined as code: input, triage, spec, human spec review, implementation, agent and human code review, verification, human product review, ship, monitor, and back to input.

## Belongs here

- Stages, transitions and the conditions between them, including cheap decision models at branch points.
- Human gates: where a person must approve, and the evidence they get to decide.
- Triggers: where work comes from (issues, chat, monitoring, recurring corrections).

## Does not belong here

- Agent definitions: `agents/`.
- Scoring of runs: `evals/`.

## Contract

- Every human gate names the evidence it requires. A gate without evidence is a rubber stamp.
- Runs are durable: they can be suspended, resumed and restarted without a human babysitting them.
- Every run is recorded (conversation, artifacts, cost), because recorded runs are the raw material of `evals/`.

## Open questions

Orchestrator (an existing tool or Telar's own); where run records are stored and for how long; how the cost of a run is measured.
