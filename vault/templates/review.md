# Review page: {topic}

Template for the content of a review page ([ADR 0011](../decisions/0011-review-pages-before-decisions.md)). The page itself is HTML; this file says what it must contain and how it is delivered. Copy the structure, not this text.

## Where it goes and how it is delivered

- **File.** `vault/reviews/YYYY-MM-DD-{topic}.html`: a standalone HTML document (doctype, inline CSS, inline SVG, no build step). Web fonts are optional; the page must read well without them.
- **Claude Code.** Publish the same page as a private Artifact (the Artifact receives the page without the document wrapper) and give Diego the link.
- **Codex, OpenCode or another harness.** Give Diego the path of the file to open in a browser.
- **Record.** The plan log or the ADR records the page's path, and the Artifact link if there is one.

## Language and tone

- The language the user indicates (Diego: Spanish). Plain sentences. The user's own words, when quoted, in the language they used.
- The page is a view of English sources: link every item to its source file. When a page and its source disagree, the source wins and the page is rebuilt.

## Sections, in this order

1. **What I need from you.** The decisions asked, by ID, each answerable in one line (accept, choose an option, say go), and how to answer.
2. **In one line each.** A table: ID, what it fixes, the recommendation.
3. **Context.** The request or the problem, in the owner's words, and the evidence it rests on.
4. **Diagrams.** Every design, model, flow, stage sequence, architecture or state machine is drawn: inline SVG (Mermaid only inside a Claude Artifact, which renders it natively). One idea per diagram, labeled with the same terms as the sources.
5. **Each decision.** What it fixes; the options, recommendation first, and why; what changes and for whom; consequences and risks; the alternatives discarded and why. Anything the agent added beyond the owner's words is marked as such.
6. **What is open and what comes next.** What is still undecided, and what the agent does after each possible answer.

## Before sending

- Readable in about five minutes; the one-line table alone gives the gist.
- Works at phone width, and in light and dark themes.
- Every ID, number and date matches the source files.
- Nothing private on a page saved in a public repository.
