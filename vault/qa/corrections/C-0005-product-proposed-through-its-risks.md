---
id: C-0005
status: logged
date: 2026-11-26
by: diego
harness: claude-code
model: claude-opus-5-5
occurrences: 1
encoded_as:
encoded_in:
updated: 2026-11-26
---

# C-0005: A product proposed through its risks instead of its users

## What the agent did

The owner described the first installation by pointing at a reference product (OpenResearch) and asked for something anyone could use with little configuration. In the diagnosis and plan, the agent:

- proposed that users assemble the setup themselves, and postponed the product's app to a project after a pilot;
- recommended that a person approve every external action by default, and that one external platform never be automated, citing that platform's user agreement and a rule from an early version of the source user's instructions;
- applied a Telar candidate non-negotiable about the workshop (N-01: transitions with effects are decided by code or an authenticated person) to the product's behavior for its users;
- chose the older of two contradicting rules in the source user's repository without saying so: her later instructions gave the agent more autonomy, including on that platform.

The agent researched the constraints in depth (vendor terms, the platform's agreement) and did not research the product category or its trend.

## The correction

Diego: "I think from your questions that you don't understand the product and the trend. This is like an OpenClaw specialized in [redacted: product domain], and it must be automatic. It can be configured to give permissions, but by default it must be automatic, since that is what a person looks for when using an agent. And it must be easy; that's why we need the app [redacted: product detail]. The idea is to make it easy for the customer." (Translated from Spanish.) He also answered the open decisions against the recommendations on the product's form, the default autonomy and that platform.

## Why the workshop allowed it

- The diagnosis template has no place for the product thesis in the owner's words, confirmed before options are written. The agent built fifteen decisions on its own reading of the request.
- Nothing asks a diagnosis of a new product to research its category and reference products; risks were researched and the trend was not.
- Evidence from one early user was treated as product invariants, and a contradiction inside that evidence was resolved silently toward the conservative side.
- Nothing says that Telar's non-negotiables govern how software is built in the workshop, not what the product does for its users.
- Related to [C-0002](C-0002-shallow-proposal-without-evidence.md) (a complete-looking answer over a grounded one), but the failure differs: here the evidence was read and the framing was wrong. Logged separately; reviewed together if either recurs.

## Encoding

Not encoded yet. Proposed, for Diego to decide:

- **Template (structure):** the diagnosis template opens with "The request": the thesis restated in the owner's words, with the reference products the owner named, confirmed by the owner in one question before options are written.
- **Template (structure):** in "Options", an option that goes against what the owner asked says so in its first line, and so does a recommendation.
- **Rule, in the `core-definition` catalog:** non-negotiables govern the workshop (how software is built and released); the product's behavior toward its users is the product's decision, recorded in the product's ADRs.
- **Skill candidate:** a research checklist for a new product: category, reference products and trend before constraints.

## Log

- 2026-11-26: Logged (occurrence 1). The installation's plan moves to a new iteration with a new diagnosis.
