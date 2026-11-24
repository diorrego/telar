# Evidence

The research Telar comes from: the working conversations, the documents they produced, a prototype and the figures, translated into English and ordered by date ([ADR 0009](../decisions/0009-research-evidence-in-the-vault.md)). The synthesis is in [`foundations/research.md`](../foundations/research.md); the first project that works from this evidence is [`core-definition`](../projects/core-definition/v1/DIAGNOSIS.md).

## How to read it

The research happened in three conversations between Diego and AI assistants in OpenResearch, between 2026-11-21 and 2026-11-24. Each conversation produced documents. Read a conversation to see why a document says what it says: Diego's requirements are often in the conversation, not in the document (for example research before requirements, or the order rules, workshop, factory).

| # | Date | Conversation | Documents it produced |
|---|---|---|---|
| 1 | 2026-11-21 to 22 | [Agentic software factories](conversations/2026-11-21-agentic-software-factories.md): literature review, the traditional and agentic factory models, Diego's model (research stage, rules in YAML, channels, isolated environment, vaults as memory), pilot architecture, single-project scope, browser checks, compaction, Warp | [Literature review](documents/2026-11-21-literature-review.md), [paper](documents/2026-11-21-paper-agentic-software-factories.tex), [conceptual framework](documents/2026-11-21-conceptual-framework.md), [pilot architecture](documents/2026-11-22-pilot-architecture.md), [multi-project architecture](documents/2026-11-22-multi-project-architecture.md), [research guide](documents/2026-11-22-research-guide.md), [Warp Factories and the pilot](documents/2026-11-22-warp-factories-and-pilot.md), [Warp prototype](prototypes/warp/factory.yaml) |
| 2 | 2026-11-22 | [Critical review](conversations/2026-11-22-critical-review.md): the review against the talks and new literature, the public kit with woku as first installation, license, name | [Critical review and version zero](documents/2026-11-22-critical-review-and-version-zero.md), [public kit: model and architecture](documents/2026-11-22-public-kit-model-and-architecture.md) |
| 3 | 2026-11-22, 24 | [AI Engineer talks](conversations/2026-11-22-ai-engineer-talks.md): summary of the five talks, the order rules then workshop then factory, a LinkedIn post | None |

## Index

| Date | Kind | Item | Original |
|---|---|---|---|
| 2026-11-21 | Conversation | [Agentic software factories](conversations/2026-11-21-agentic-software-factories.md) | OpenResearch chat "Fábricas de Software Agénticas" (Codex), 2026-11-21 to 22 |
| 2026-11-21 | Document | [Literature review](documents/2026-11-21-literature-review.md) | "Fábricas de software con agentes" |
| 2026-11-21 | Document | [Paper (LaTeX)](documents/2026-11-21-paper-agentic-software-factories.tex) | `paper.tex`, a 10-page integrative review; Diego judged it "an advance, but poor" and asked to define the factory model first |
| 2026-11-21 | Document | [Conceptual framework](documents/2026-11-21-conceptual-framework.md) | "De la fábrica de software tradicional a la fábrica con agentes", updated 2026-11-22 |
| 2026-11-21 | Figure | [Traditional software factory](figures/2026-11-21-traditional-software-factory.svg) | `fabrica-de-software-tradicional.svg` |
| 2026-11-21 | Figure | [Agentic software factory](figures/2026-11-21-agentic-software-factory.svg) | `fabrica-de-software-con-agentes.svg` |
| 2026-11-21 | Figure | [Agentic factory, research and operation](figures/2026-11-21-agentic-factory-research-and-operation.svg) | `fabrica-con-agentes-investigacion-y-operacion.svg` (the current model diagram) |
| 2026-11-21 | Figure | [Pavlenko et al., figure 1](figures/2026-11-21-pavlenko-cycle.png) | From the cited paper, in English |
| 2026-11-21 | Figure | [Paper diagrams](figures/2026-11-21-paper-diagrams.png) | Rendered from the Spanish paper; a raster, not translated. The translated diagrams are in the `.tex` source |
| 2026-11-22 | Document | [Pilot architecture](documents/2026-11-22-pilot-architecture.md) | "Piloto monoproyecto de la fábrica de software con agentes" |
| 2026-11-22 | Document | [Multi-project architecture](documents/2026-11-22-multi-project-architecture.md) | Multi-project design, kept as reference for later |
| 2026-11-22 | Document | [Research guide](documents/2026-11-22-research-guide.md) | The entry guide (`README.md`) of the research on 2026-11-22 |
| 2026-11-22 | Document | [Warp Factories and the pilot](documents/2026-11-22-warp-factories-and-pilot.md) | "Qué tomar de Warp Factories para el piloto de Woku" |
| 2026-11-22 | Prototype | [Warp Blueprint](prototypes/warp/factory.yaml) and its workers ([foreman](prototypes/warp/agents/foreman/agent.md), [builder](prototypes/warp/agents/builder/agent.md), [verifier](prototypes/warp/agents/verifier/agent.md)) | `prototipos/warp/`; schema keys unchanged, values translated. Its gates are natural language, which the critical review rejects |
| 2026-11-22 | Conversation | [Critical review](conversations/2026-11-22-critical-review.md) | OpenResearch chat "Revisión Crítica Fábrica Software" (Claude Code) |
| 2026-11-22 | Document | [Critical review and version zero](documents/2026-11-22-critical-review-and-version-zero.md) | "Revisión crítica de la fábrica con agentes y propuesta de versión cero" |
| 2026-11-22 | Figure | [CompAct-Bench, figure 2](figures/2026-11-22-compactbench-fig2.png) | From the cited paper, in English |
| 2026-11-22 | Figure | [SE Factory, figure 6](figures/2026-11-22-se-factory-fig6.png) | From the cited paper, in English |
| 2026-11-22 | Document | [Public kit: model and architecture](documents/2026-11-22-public-kit-model-and-architecture.md) | "Modelo y arquitectura del kit público de fábrica de software con agentes"; the kit's provisional name was "obrador" |
| 2026-11-22 | Figure | [Kit components](figures/2026-11-22-kit-components.svg) | `kit-publico/componentes-del-kit.svg` |
| 2026-11-22 | Figure | [Journey of a work item](figures/2026-11-22-work-item-journey.svg) | `kit-publico/recorrido-de-un-encargo.svg` |
| 2026-11-22 | Conversation | [AI Engineer talks](conversations/2026-11-22-ai-engineer-talks.md) | OpenResearch chat "AI Engineer Talks Summary" (Claude Code), continued 2026-11-24 |

## Conventions

- **Translation.** From Spanish, on 2026-11-24, faithful and complete: no summarizing, rewording or improving. Text that was already in English is unchanged. Terms follow the [glossary](../foundations/glossary.md): *encargo* is "work item", *expediente* "dossier", *bitácora* "log", *puerta* "gate", *aviso* "call-out", *taller* "workshop". Spanish identifiers in illustrative code and file names in examples were translated and the change is noted under the block.
- **Provenance.** Each file starts with what it was translated from, when, and where the original is kept (the OpenResearch research workspace, unchanged).
- **Conversations.** Diego's messages, the assistant's answers and Diego's mid-turn messages, in order, with their timestamps. Tool calls are omitted (their results are the documents). Headings inside a message are one level below the message heading.
- **Redactions.** The repository is public. Absolute local paths, private links (two private landing pages) and woku-internal details (vault file paths, commit hashes, repository names, an internal project name) are replaced by `[redacted: reason]`. The name woku and generic phrases like "engineering vault" or "QA vault" stay ([ADR 0008](../decisions/0008-telar-is-a-method-and-framework.md)).

## Not included

| Item | Why |
|---|---|
| The five talk transcripts | Third-party content; cited by public link in [`research.md`](../foundations/research.md) |
| Two landing pages (a visual guide and a CTO edition) and their covers | Presentations generated from the documents above, hosted privately |
| `paper.pdf` | Compiled from the Spanish source; the translated `.tex` replaces it |
| `PRODUCT.md` | A design brief for the landing pages |
| Tool call outputs | Their results are the documents |

## Corrections to the evidence

None yet. Each correction of a translation or a redaction is listed here with its date and reason.
