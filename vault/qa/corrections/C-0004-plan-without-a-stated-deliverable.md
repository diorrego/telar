---
id: C-0004
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

# C-0004: A product plan that did not say what its first users get

## What the agent did

It wrote the first plan of a new product installation following Telar's plan template: a goal made of observable scenarios, open decisions, phases, out of scope. It then made a visual explainer of the same plan. What the first users would receive was spread across three scenarios, two phases and the out of scope list; neither document said it in one place.

## The correction

Diego: "it's not clear to me what the deliverable or the MVP is that the first users will use." (Translated from Spanish.)

## Why the workshop allowed it

- The plan template asks for observable scenarios ("who does what, and what they see when it works"), not for a deliverable. Scenarios are how the plan is tested; they mix the workshop's own setup, research, checks and the pilot with what a user receives.
- For a definition project, such as Telar's own `core-definition`, scenarios are enough: the deliverable is the documents. For a plan that ships a product to people, the reader has to assemble the deliverable from the scenarios, and the agent did not notice the gap because the template was followed.

## Encoding

Not encoded yet. Proposed, for Diego to decide:

- **Template (structure):** `templates/plan.md` gains an optional section, required when the plan ships something to users: "Deliverable: what the users get". It states what the users have, what they do with it, what it does not include, what it asks of them, and at which scenario it exists.
- **Check, once Telar has code:** a plan with a scenario whose actors are users and no "Deliverable" section fails the plan lint, with a message that says which section to add.

## Log

- 2026-11-26: Logged (occurrence 1). The installation's plan gained the section in the same session.
