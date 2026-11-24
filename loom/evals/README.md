# evals

**Stage 2, loop. Empty until the workshop stage meets its exit criteria ([ADR 0006](../../vault/decisions/0006-workshop-before-factory.md)).**

Measurement of the workshop on its own work, and the self-improvement loop that feeds on it.

## Belongs here

- Scores (online evals): judges, model or human, that grade recorded runs on one failure mode each (for example, redundant tests written).
- Benchmarks: suites built from real past tasks, replayed against other models, harnesses or loom versions to compare cost and quality.
- Self-improvement: aggregation of failed scores and logged corrections into proposals, delivered as pull requests to the loom.
- Definitions of the workshop metrics in [`vision.md`](../../vault/foundations/vision.md): corrections per session, recurrence, revert rate, attention per change, cost per change, cycle time.

## Does not belong here

- Public benchmark results. Telar measures on its own data.

## Contract

- Each score defines one failure mode, its judge, and the evidence it cites.
- Judges are calibrated against human grading before their scores drive changes.
- Proposals from the self-improvement loop are born as `proposed` plans or pull requests; they never merge themselves.

## Open questions

Judge models and calibration; benchmark curation (by hand first); where results are stored.
