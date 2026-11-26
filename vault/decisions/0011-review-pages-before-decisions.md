---
id: ADR-0011
status: accepted
date: 2026-11-26
decided_by: diego (2026-11-26; parts 4 and 5 and the template proposed by claude, accepted with part 5 changed)
superseded_by:
---

# ADR-0011: Every decision is shown on a visual review page before it is approved

## Context

Diego, 2026-11-26 (translated from Spanish): "I see a problem in Telar here: create an artifact when Claude Code is used, or, if another agent such as Codex or OpenCode is used, create an HTML file that diagrams and shows visually the designs, decisions and models it generates, to approve decisions before implementing. This will speed up decision-making and the understanding of the research and the later design."

He had asked for the same thing during the research: the person's review belongs inside the flow, and HTML pages or Claude artifacts with diagrams speed up explanations (R16 in the [core-definition diagnosis](../projects/core-definition/v1/DIAGNOSIS.md); [evidence](../evidence/conversations/2026-11-22-ai-engineer-talks.md), 2026-11-24 09:55). The kit design already put a `summary.html` in every dossier for the human decision ([evidence](../evidence/documents/2026-11-22-public-kit-model-and-architecture.md), §6.2), and N-26 lists it as a candidate non-negotiable. Even so, until 2026-11-26 every decision was asked of Diego in Markdown files and chat tables: core-definition v1 and v2, the first installation's plans and its eight ADRs. The first visual page was made only when he asked for it (correction [C-0006](../qa/corrections/C-0006-decisions-asked-without-a-visual-page.md)).

## Decision

1. **When.** Before an agent asks Diego to decide (accept ADRs, say go to a plan, answer open decisions) or to review research, a diagnosis, a design or a model, it builds a review page and gives it to him with the request. A request without its page is incomplete.
2. **What.** A self-contained HTML page that shows what is being decided: for each decision, what it fixes in one line, the options with the recommendation, the evidence and the consequences. Designs, models, flows, stage sequences and architectures are drawn as diagrams, not only described. The page ends with what Diego has to answer. Its contents follow [`templates/review.md`](../templates/review.md).
3. **Per harness.** Claude Code publishes the page as a private Artifact and gives the link. Codex, OpenCode or any other harness gives the path of the HTML file to open in a browser.
4. **Kept with the work.** In every harness, the page is also saved in the repository as a standalone HTML document, `vault/reviews/YYYY-MM-DD-topic.html`, and the plan log or the ADR records its path (and the artifact link, if any). It is the record of what Diego saw when he decided.
5. **Language.** The page is written in the language the user indicates (Diego asked for Spanish). It is a view of English sources ([ADR 0002](0002-english-everywhere.md) still governs everything else) and links to them; when a page and its source disagree, the source wins and the page is rebuilt.

Parts 1 to 3 are Diego's rule. Parts 4 and 5 and the template were the agent's proposal; Diego accepted them on 2026-11-26 ("está bien"), changing part 5 from "the owner's language" to "the language the user indicates".

## Consequences

- The rule applies now in this repository and in the first installation, which applies Telar's method by hand and copies its rules and templates.
- `core-definition`: N-26 becomes settled as a direction: every human gate comes with a visual review page, and how it is delivered depends on the harness (a mechanism, level M). Phase 2 catalogs it; phase 5 lists the review page among the formats.
- Candidate check, once code is allowed: a plan or an ADR in `proposed` without a linked review page fails.
- Pages for Telar's own decisions are public, like the rest of this repository. An installation's pages stay in its own repository.

## Review page

[`reviews/2026-11-26-review-pages.html`](../reviews/2026-11-26-review-pages.html) (Spanish), also published as a private Artifact: https://claude.ai/artifact/T5ux1fuZm3f1QLYbih8zjx

## Alternatives considered

- **Summaries in chat only.** What happened until now, and what Diego corrected.
- **Markdown with Mermaid diagrams.** GitHub renders them, but not every harness shows them, and a document is slower to read than a page built for the decision.
- **Artifacts only.** Works only with Claude Code and leaves no record in the repository.
