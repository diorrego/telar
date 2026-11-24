# skills

**Stage 1, workshop. Trust pyramid layer 4: skills.**

Reusable procedures that tell an agent how to do a recurring task well, and the small CLIs they call.

## Belongs here

- Procedures with a clear trigger and outcome, for example: verify a UI change, write a diagnosis, log and encode a correction, write the owner summary before final verification.
- The scripts and CLIs a skill calls (once code is allowed), so the work is repeatable and costs fewer tokens.

## Does not belong here

- Always-on guidance: `rules/`.
- Anything a deterministic check could enforce: `checks/`.

## Contract

- One folder per skill, named by what it does.
- Each skill states its trigger, inputs, steps, output, and how its success is verified.
- Content is harness-agnostic. Packaging a skill for a specific harness is a build concern, decided by a project.

## Open questions

The format (an open skills format or Telar's own); how skills reach each harness; how a skill's effectiveness is scored.
