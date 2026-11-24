# checks

**Stage 1, workshop. Trust pyramid layer 2: deterministic checks.**

Guardrails a machine enforces every time, so neither the agent nor the reviewer has to remember them. This is where most corrections should end up.

## Belongs here

- Lint rules that ban constructs agents misuse, especially those that need nuance to use well.
- Dependency and boundary rules: which directory may import which.
- Type, compile and test gates, and the policy for what a test must prove.
- Checks on the workshop itself, for example: every `AGENTS.md` is a symlink to its sibling `CLAUDE.md`; every plan has valid frontmatter.

## Does not belong here

- Anything that needs judgment: `rules/`.
- Checks that need the software running: `verify/`.

## Contract

- Each check traces to the correction (`C-NNNN`) or finding (`F-NNNN`) it encodes, or to the plan that introduced it.
- A failing check names the root cause and the fix, not just the violation.
- Exceptions are explicit allowlists inside the check, never comments in the checked code.

## Open questions

For the first core project: the language and runner for custom checks; how checks are installed into a target repository; how to measure that a check worked (the correction it encodes stops recurring).
