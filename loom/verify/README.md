# verify

**Stage 1, workshop. Trust pyramid layer 3: verification.**

Ways for an agent to prove that its change works, producing artifacts a human can judge in seconds instead of reading the diff.

## Belongs here

- Runtime verification: drivers that run the software and use it like a user would (browser automation, the DevTools protocol, CLI drivers).
- Feature maps: the user's-eye map of a target's features, so humans and agents share names for things.
- Property-based tests and formal specifications (for example TLA+ or Lean) for flows and algorithms where examples are not enough.
- The definition of a verification artifact: what a screenshot, video, state chart, trace or owner summary must contain to count as evidence.

## Does not belong here

- Static checks that do not run the software: `checks/`.
- The procedure an agent follows to verify a change: a skill in `skills/` that calls what lives here.

## Contract

- Every verification produces an artifact saved where the reviewer looks (the iteration folder, the pull request).
- Reusable drivers are CLIs, so agents call them the same way every time and they can be tested.
- A verification says what it proves and what it does not.

## Open questions

Artifact formats and storage; how a reviewer sees the artifacts of one change; which verification is worth its token cost for which kind of change.
