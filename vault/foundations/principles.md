# Principles

Every design in Telar must respect these. Each one names its source ([research](research.md)); **Telar** marks a position of our own. To change a principle, propose it to Diego and record an ADR.

## 1. Human attention is the budget

The scarce resource is not tokens or code but the attention of the people directing agents. Spend it at decisions (spec, product review, pushback), not on babysitting runs or reading code an agent could have proven correct.

*Source:* Ronacher. *In Telar:* every human gate names the evidence it needs, and owner summaries fit in a minute.

## 2. Workshop before factory

A factory amplifies its inner loop. If the inner loop produces slop, automation produces more slop at a higher cost. Build trust in the inner loop first.

*Source:* Ronacher, Tan. *In Telar:* the stages in [ADR 0006](../decisions/0006-workshop-before-factory.md).

## 3. Trust is built in the environment, bottom up

Order of preference: architecture and API design; deterministic checks (lint, types, boundaries, tests); verification (runtime, property-based, formal); prose last.

*Source:* Tan (the inverse pyramid). *In Telar:* five layers, splitting prose into skills and rules: 1 architecture, 2 check, 3 verification, 4 skill, 5 rule. The corrections ledger encodes in this order.

## 4. Every correction is a defect of the workshop

When a human has to correct an agent, the environment allowed the mistake. Log it, then encode it at the lowest layer of the pyramid that can prevent it. Prose is the last resort: it drifts, agents over-apply it as a hard rule, and it gives them a place to justify not doing the right thing.

*Source:* Tan; Lloyd (self-improvement loops). *In Telar:* the corrections ledger in [`qa/corrections/`](../qa/CLAUDE.md).

## 5. Review evidence, not diffs

Agents produce verification artifacts a human can judge quickly: screenshots, videos, state charts, check and test output, a one-minute summary. Line by line review is reserved for where checks and verification have not yet earned trust.

*Source:* Tan, Lloyd; Ronacher (summaries before verification). *In Telar:* verification artifacts, the owner review stage, and review pages: every decision and design reaches Diego as a visual page before he approves it ([ADR 0011](../decisions/0011-review-pages-before-decisions.md)).

## 6. Push back

The agent is rewarded for completing the goal; whether the result fits the system is the human's responsibility. Knowing when to say "this is the wrong way" is the core skill, and it rests on real engineering skill, not on agent skill.

*Source:* Ronacher.

## 7. Keep the codebase pristine; agents copy what they see

Code is the largest input to an agent. Workarounds, deprecated patterns and tech debt get copied as the established way. Ban new occurrences with a check, then clean up the old ones.

*Source:* Tan.

## 8. Move at the speed of understanding

Do not ship what nobody understands. Volume is not the goal; ambitious, high-quality software whose parts fit together is. Avoid uncontrolled growth.

*Source:* Ronacher.

## 9. Define the workshop as code

Versioned, declarative and diffable, so it can be branched, compared, rolled back, and improved by agents through pull requests.

*Source:* Lloyd. *In Telar:* `core/`.

## 10. Measure on your own work

Public benchmarks do not say what works on your codebase. Record runs, score them, and build benchmarks from your own past tasks.

*Source:* Lloyd; Ronacher (analysis of his own sessions).

## 11. Thin harness, replaceable models

Models improve under a stable harness, and yesterday's tricks become unnecessary. Keep model and harness as parameters. Do not build what the next model will make obsolete, and remove what it already has.

*Source:* Ronacher, Lloyd.

## 12. Few dependencies, open formats, shared standards

Agents make it cheap to write your own code, which is good for dependencies and bad for interoperability. Prefer standards and open formats. When a problem is really about agreement between people, work with people.

*Source:* Ronacher.

## 13. Decide what not to build

Now that almost anything can be built, choosing what not to build is part of the job. Every plan says what is out of scope.

*Source:* Ronacher.

## 14. A human says go

Plans are proposals until Diego says go. Agents propose, including changes to the core itself; they never approve their own proposals.

*Source:* **Telar**, consistent with Lloyd's human gates.

## 15. Document as you go

The plan, its log and the indexes are updated in the same commit as the work, not after. The vault is the memory of the workshop.

*Source:* **Telar**.
