# Conversation: AI Engineer talks, the order workshop then factory, and a LinkedIn post

> **Evidence.** Translated from Spanish on 2026-11-24. Original: OpenResearch chat "AI Engineer Talks Summary" (Claude Code), 2026-11-22 and 2026-11-24, kept in the research workspace. Tool calls are omitted. Redactions are marked `[redacted: reason]`.

## 2026-11-22 22:28 · Diego

summarize the main ideas of the talks ai-engineer-youtube/

*(tool calls omitted)*

## 2026-11-22 22:28 · Assistant

There are 5 transcripts (~136 KB). I'm reading them in full.

*(tool calls omitted)*

## 2026-11-22 22:28 · Assistant

There are 5 talks: one by Lauren Tan, one by Armin Ronacher and three by Zach Lloyd (Warp). Lloyd's three repeat almost everything, so I'm summarizing them together.

### 1. "All Code Is Slop (Except Mine)": Lauren Tan, SpaceXSI
`ai-engineer-youtube/All Code Is Slop Except.md` ([video](https://www.youtube.com/watch?v=O_zcc6Xl12g))

**Central idea:** the factory is based on trust, but not blind trust. It is earned by investing in the agent's environment.

- **Inverted pyramid of where to invest:** first the code itself (API design, architecture), then lint, types and tests. After that, runtime verification and formal verification. Last, and in small amounts, free text: rules, skills, AGENTS.md.
- **Every correction to the agent becomes an automated check**, not another line in AGENTS.md. For example, they ban `useEffect` in product code and they ban importing code from the main process (main) in the renderer. That way the problem disappears completely and doesn't have to be watched for in every review.
- **The codebase is a garden.** Agents copy any pattern they find, so technical debt spreads like a pest. It's worth keeping it spotless.
- **They ban 99% of comments:** agents use them to justify patches (timers like `setTimeout`) instead of fixing the root cause.
- **Review becomes review of evidence:** videos, screenshots, a "feature map" of the app, TLA+ and Lean for formal verification, and property-based UI testing. A large share of the tokens goes to verification (she cites a case of ~70%).
- **Results:** 11,000 PRs a month across the team, ~0.5% reverts and better app performance.
- **Warning:** if the inner loop produces slop, automating it only produces more slop.

### 2. "Build the Workshop Before the Software Factory": Armin Ronacher, Earendil
`ai-engineer-youtube/Build the Workshop Before.md` ([video](https://www.youtube.com/watch?v=JNexz3Tbiu8))

**Central idea:** before the factory you have to build the craft workshop. The goal is not to make more software, but more ambitious, higher quality software.

- **Models improve on their own.** His harness (Pi) hasn't changed in a year, and even so:
  - he corrects the agent much less;
  - the p90 duration of a task went from ~2.5 min to more than 14 min.
  - Many prompting or plugin tricks are no longer needed.
- **The bottleneck is human attention.**
  - His daily prompts stay stable, but the agent's active time grows exponentially.
  - He has created 141 repos, but only really maintains 10 to 15.
  - Creating projects is easy; maintaining them is not.
- **Real skill versus the agent's skill:**
  - You have to know when to stop the agent: it's optimized to "complete the goal", not for long-term coherence, and it ends up producing a system with features piled up without coherence.
  - He asks for an executive summary in HTML before the verification phase, since he often doesn't read the code.
- **Against uncontrolled growth:** if everyone builds their own implementation of everything, shared formats and standards break. As with human collaboration, that remains hard and important.
- **Where harnesses are heading:**
  - durable agents, which can be suspended and resumed (useful for flex pricing and long tasks);
  - "code mode", where the agent orchestrates tools with JavaScript;
  - cheap classifier models for decisions inside workflows.
- **Closing:** "now that we can build everything, maybe we shouldn't".

### 3 to 5. Software Factories: Zach Lloyd, Warp
`ai-engineer-youtube/Software Engineering Is.md` ([video](https://www.youtube.com/watch?v=tUPPVhBBcoM)) · `ai-engineer-youtube/Engineer Your Coding Agents.md` ([video](https://www.youtube.com/watch?v=0LeT996Hz3E)) · `ai-engineer-youtube/How to Build a Software.md` ([video](https://www.youtube.com/watch?v=nKjPBAw_N_0))

**Thesis:** software engineering becomes factory engineering. You build *what builds the product*.

- **His definition of a factory:** a closed-loop system, defined in code, that continuously measures and improves coding agents running in the cloud. It is not a set of loose automations, nor "AI teammates", nor a personal swarm of agents.
- **Why move from local agents to the cloud:** human pace limits the work, cost is hard to control, and security and governance are hard to guarantee.
- **The development lifecycle loop:** idea intake → triage (if it's easy and unambiguous, it's implemented directly) → product spec + technical spec → implementation → code review (an agent first; when a human comes in is a matter of risk management) → verification with computer use (videos, screenshots) → CI/CD → monitoring, which feeds back into intake. Humans step in at specific points.
- **The layers, from bottom to top:**
  1. Factory as code, Terraform style. It allows branches, rollback, and agents proposing PRs to the factory itself.
  2. Data: store all conversations and artifacts.
  3. Sandboxes.
  4. Inference with any model and any harness.
  5. Orchestration.
  6. An API/MCP that integrates with Slack, Linear, GitHub, etc.
- **Measure first:**
  - DORA metrics, cost per PR, human interactions per PR;
  - online evals with an LLM as judge (example: detecting redundant tests);
  - in-house benchmarks: rerun real tasks with different models to get a cost/quality curve and decide which model to send each type of task to.
- **Self-improvement:**
  - Observer agents cluster failures and open a PR against the factory definition (example: "seen 37 times").
  - Skill loops: if a human corrects the review agent, that agent gets improved.
- **Open source:** cloning software now costs almost nothing, so the product alone isn't enough. Warp opened its code because it had a factory able to handle the noise of issues and PRs (build.warp.dev).
- **About people:** less code will be written and more things will be shipped. Human product judgment remains essential.

### Common themes and tensions

| Theme | Consensus / tension |
|---|---|
| Foundation before automation | Tan and Ronacher: without quality code and without verification, automating only amplifies the slop. Lloyd starts with the infrastructure. |
| Verification | Everyone sees it as what makes trust possible: evidence (video, screenshots, specs) instead of reading diffs. |
| Corrections → lasting improvements | Tan: deterministic lint and architecture. Lloyd: PRs to the factory generated by evals. It's the same idea at a different level. |
| Metaphor | Tan talks about a "garden"; Lloyd rejects that image and wants "measurable engineering". Ronacher talks about a "craft workshop" and puts excellence above volume. |
| Human limit | Ronacher says it's attention. Lloyd reserves it for spec, review and product checkpoints. |

### What it implies for this kit (my interpretation, the talks don't say this)
If the goal of `agentic-software-factory` is to be a reusable kit, the talks suggest this order:
1. A minimal "workshop": lint and automated checks, and verification with evidence.
2. The factory defined as code (triage → spec → implementation → review → verification).
3. Recording of all sessions, plus evals and benchmarks with each installation's data (Woku as the first case).

Do you want me to turn it into a document or a page to share with the team?

## 2026-11-24 09:29 · Diego

so in the end the order of the videos would be the one by the spacex employee -> then the pi one -> to finally end with the warp ones?

that is, first rules, contracts, tests, etc -> workshop -> factory?

## 2026-11-24 09:29 · Assistant

Yes, the order is good. But what comes before the factory is not two steps (rules → workshop) but a single one: **the workshop**, seen from two sides.

### How they fit together

**1. Tan (SpaceXSI): the workshop, technical side.** Set up an environment in which the agent gets it right by default:
- Architecture and APIs that make it hard to get things wrong.
- Lint, types and tests. Every correction to the agent becomes an automated check.
- Verification with evidence: videos, screenshots, formal verification.
- Very little text (AGENTS.md, skills), and only at the end.

**2. Ronacher (Pi): the workshop, human side.** What can't be automated:
- Knowing when to stop the agent and keeping the system coherent.
- Not moving faster than you are able to understand.
- Managing attention: you can create 141 repos, but you only really maintain 10 to 15.
- At the end of his talk he takes the step toward the factory: durable agents, "code mode" and cheap classifiers for long, unsupervised tasks.

**3. Lloyd (Warp): the factory.** On top of the above:
- The factory defined as code, with its development lifecycle loop (triage → spec → implementation → review → verification → monitoring).
- Measurement, evals, in-house benchmarks and self-improvement.

In short: **workshop (Tan + Ronacher) → factory (Lloyd)**.

### Two nuances

- **It isn't linear, it's a cycle.** Lloyd's self-improvement (agents that detect repeated failures and open PRs against the factory definition) is Tan's rule ("every correction becomes a check") applied at scale. Once the factory is running, what it learns goes back to the workshop as new rules, tests and skills.
- **Tan also ends up at the factory.** The end of her talk is an automated loop: with each release, agents test the app like a user, find bugs and open PRs that merge on their own. Her point is that this only works because the workshop was already solid.

### Suggested viewing order
1. Tan: *All Code Is Slop (Except Mine)*
2. Ronacher: *Build the Workshop Before the Software Factory*
3. Lloyd: *Software Engineering Is Becoming Factory Engineering*. It's the most conceptual: the thesis and the development lifecycle loop.
4. Lloyd: *Engineer Your Coding Agents Like Any Other System*. It defines what a factory is and its layers.
5. Lloyd: *How to Build a Software Factory That Improves Itself*. It's the most practical: a demo of scores and benchmarks, plus the Q&A round.

For the kit, the consequence would be that phase 1 (the workshop) can also be delivered as a template: lint rules, verification with evidence and the "correction → check" convention. The factory part alone is not enough.

## 2026-11-24 09:33 · Diego

i'd like to write a post on linkedin this is my writing style, direct, very short paragraphs and no capital letters [image not included] .

*(tool calls omitted)*

## 2026-11-24 09:33 · Assistant

I read your posts. The ones that perform best are the shortest: a controversial opinion or a question that can be read in full without clicking "see more". The "AI code is garbage" one (8,342 impressions) and the "knowing what to do or what not to do" one (4,832) are one or two lines long and have 17 comments each. The long ones perform worse. So I'm proposing three options, from shortest to longest.

---

**option 1: short and controversial** (follows up on your most viewed post)

> a month ago i said AI code is garbage just like human code.
>
> i got one thing wrong: AI copies the garbage you already have.
>
> if your codebase is dirty, an agent factory just manufactures more garbage, faster.

---

**option 2: a question to drive comments**

> everyone wants a software factory with agents.
>
> but nobody wants to fix their codebase first.
>
> what comes first: automating or cleaning up?

---

**option 3: the sequence, a bit longer**

> i watched 5 ai engineer talks about software factories.
>
> the conclusion i drew is simple:
>
> first the workshop. then the factory.
>
> workshop = lint, tests, contracts, verification. every time you correct the agent, that becomes a rule in the code, not one more line in a markdown file.
>
> workshop also = human judgment. knowing when to tell the agent "no, not like that".
>
> only then, factory: agents in the cloud, specs, evals, metrics.
>
> automating a process that produces garbage only produces more garbage.

---

I'd pick **option 1**. It picks up your most successful post, so whoever read it already has the context, and it stays short like the ones that work best for you. I'd save option 3 for a carousel or for a pinned comment under the post.

Do you want me to adjust the tone or write a version that mentions the open source kit?

## 2026-11-24 09:38 · Diego

i'd prefer more of a story, mentioning who said what and that line i mentioned to you, first start with a workshop, then the software factory. as a transition. and all of this is to get speed and quality in code using ai

## 2026-11-24 09:38 · Assistant

Here's the story. It goes from the individual to the collective: first Lauren Tan's workshop, then Armin Ronacher's, and finally Zach Lloyd's factory. The line "first the workshop, then the factory" works as the hinge between the two parts.

---

> everyone talks about software factories.
>
> agents in the cloud doing triage, specs, code, review. humans only where it matters.
>
> i watched 5 ai engineer talks about this and one idea stuck with me:
>
> first the workshop. then the factory.
>
> lauren tan (grokbot) shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.
>
> her secret isn't a better agent. every time she corrects the agent, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.
>
> agents copy what they see. if your code has garbage, they multiply the garbage.
>
> armin ronacher (creator of flask) adds what can't be automated: judgment.
>
> he created 141 repos with agents in a year. he really maintains 10 or 15.
>
> the limit isn't the model. it's your attention. knowing when to tell the agent "no, not like that".
>
> that's the workshop: rules, tests, verification and human judgment.
>
> only then does zach lloyd (warp, ex google docs) arrive with the factory: agents defined as code, everything measured, evals on every session, and agents that propose improvements to the factory itself.
>
> what the factory learns goes back to the workshop as new rules.
>
> the goal of all this isn't to write more code with ai.
>
> it's to have speed and quality at the same time.
>
> automating a process that produces garbage only produces garbage faster.

---

Before posting, check two things:
- **Lauren Tan's company.** In the transcript it appears as "SpaceX SI" and "Grokbot", and it looks like a transcription error. That's why I only put "(grokbot)". Check how she introduces herself in the talk or on her LinkedIn, and tag her if you can.
- **"creator of flask".** The talks don't say this; it's a fact I added. Ronacher introduces himself as part of Earendil (the Pi agent). If you'd rather use only what the talks say, put "(earendil)".

If it feels long, you can cut the 141 repos paragraph or the "what the factory learns…" one without losing the thread.

## 2026-11-24 09:39 · Diego

mmm here in latam people talk very little about software factories

## 2026-11-24 09:39 · Assistant

Then the opening should change: I can't start with "everyone talks about this". There's also a problem: in LATAM "software factory" already has a meaning, that of outsourcing consultancies that sell developer hours. If you use it without explaining, a lot of people will understand that. It can be used as a hook:

---

> in latam, "software factory" means a consultancy that sells developer hours.
>
> abroad it's starting to mean something else.
>
> ai agents that do triage, write specs, code, review and verify. humans only where it matters.
>
> here almost nobody talks about this. so i watched 5 ai engineer talks on the topic and one idea stuck with me:
>
> first the workshop. then the factory.
>
> lauren tan (grokbot) shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.
>
> her secret isn't a better agent. every time she corrects the agent, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.
>
> agents copy what they see. if your code has garbage, they multiply the garbage.
>
> armin ronacher (creator of flask) adds what can't be automated: judgment.
>
> he created 141 repos with agents in a year. he really maintains 10 or 15.
>
> the limit isn't the model. it's your attention. knowing when to tell the agent "no, not like that".
>
> that's the workshop: rules, tests, verification and human judgment.
>
> only then does zach lloyd (warp, ex google docs) arrive with the factory: agents defined as code, everything measured, evals on every session, and agents that propose improvements to the factory itself.
>
> what the factory learns goes back to the workshop as new rules.
>
> the goal isn't to write more code with ai.
>
> it's to have speed and quality at the same time.
>
> automating a process that produces garbage only produces garbage faster.

---

The changes:
- **New hook.** It contrasts what "software factory" means in LATAM with what it's starting to mean abroad. It's a local tension and tends to generate comments.
- **A line that defines the concept**, for anyone who has never heard of it.
- **"here almost nobody talks about this"** justifies why you're sharing it.

If you want to invite comments, you can close with a question, as in your best-performing posts, for example: *"is anyone in latam already building something like this?"*. The two earlier checks are still pending: Lauren Tan's company and the "creator of flask" point.

## 2026-11-24 09:40 · Diego

not that either. the hook is wrong. in the end this workshop or software factories thing is an answer to a pain AI makes mistakes, and not just a few, when writing code, how do we use it to make quality code. That pain is very present in latam and that perception of AI in code

## 2026-11-24 09:40 · Assistant

Then we start from the pain and present the workshop and the factory as the answer:

---

> ai makes mistakes writing code. and not just a few.
>
> it invents functions, patches instead of fixing, leaves comments justifying the patch.
>
> that's why a lot of devs in latam still think code written with ai is garbage.
>
> the question isn't whether ai makes mistakes. it's how you use it so the code comes out right anyway.
>
> i watched 5 ai engineer talks about this and the answer has an order:
>
> first the workshop. then the factory.
>
> lauren tan (grokbot) shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.
>
> her secret isn't a better agent. every time the agent makes a mistake, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.
>
> the mistake doesn't get fixed once. it becomes impossible to repeat.
>
> armin ronacher (creator of flask) adds what can't be automated: judgment.
>
> the agent wants to finish the task, not to make your system make sense. someone has to tell it "no, not like that".
>
> that's the workshop: rules, tests, verification and human judgment.
>
> only then does zach lloyd (warp, ex google docs) arrive with the factory: agents that do triage, specs, code and review, everything measured, and agents that detect their own repeated mistakes and propose how to avoid them.
>
> what the factory learns goes back to the workshop as new rules.
>
> ai is going to keep making mistakes.
>
> the difference is whether each mistake slows you down or leaves you a new rule.
>
> that's how you get speed and quality at the same time.

---

The changes:
- **The hook is the pain**, and it connects with your "AI code is garbage" post without repeating it.
- **The whole thread is "AI mistakes → how you turn them into quality"**. Each person contributes a piece: Tan (mistakes become rules), Ronacher (human judgment stops the mistakes a rule doesn't catch), Lloyd (the factory detects repeated mistakes on its own).
- **I took out the 141 repos figure.** It didn't serve the mistakes thread and made the post longer.
- **The closing ties the two ideas together:** AI will keep making mistakes, and the advantage lies in what you do with each mistake.

Before posting, Lauren Tan's company and the "creator of flask" point are still pending.

## 2026-11-24 09:45 · Diego

give me the links to the videos with their author, because i'm going to do the post like this, with a made-up word for closeness:
AI makes mistakes writing code. and not just a few.

it invents functions, patches instead of fixing, leaves comments justifying the patch. that's why a lot of devs still think code written with AI is garbage.

the question isn't whether AI makes mistakes. it's how you use it so the code comes out right anyway.

i watched 5 ai engineer talks about this and the answer has an order: first the workshop. then the factory.

lauren tan (grokbot) shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.

her secret isn't a better agent. every time the agent makes a mistake, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.

the mistake doesn't get fixed once. it becomes impossible to repeat.

armin ronacher (creator of flask) adds what can't be automated: judgment.

the agent wants to finish the task, not to make your system make sense. someone has to tell it "no, not like that".

that's the workshop: rules, tests, verification and human judgment.

only then does zach lloyd (warp, ex google docs) arrive with the factory: agents that do triage, specs, code and review, everything measured, and agents that detect their own repeated mistakes and propose how to avoid them.

i'll leave the videos in the comments so you can marathon them like i did.

## 2026-11-24 09:45 · Assistant

Here's the comment. In the transcripts the links came as `youtube.com/watch/ID`, which isn't YouTube's usual format, so I converted them to `watch?v=`. They're in the order of the post:

---

> the videos 👇
>
> 1. lauren tan (grokbot): all code is slop (except mine)
> https://www.youtube.com/watch?v=O_zcc6Xl12g
>
> 2. armin ronacher (earendil): build the workshop before the software factory
> https://www.youtube.com/watch?v=JNexz3Tbiu8
>
> 3. zach lloyd (warp): software engineering is becoming factory engineering
> https://www.youtube.com/watch?v=tUPPVhBBcoM
>
> 4. zach lloyd (warp): engineer your coding agents like any other system
> https://www.youtube.com/watch?v=0LeT996Hz3E
>
> 5. zach lloyd (warp): how to build a software factory that improves itself
> https://www.youtube.com/watch?v=nKjPBAw_N_0

---

Before posting:
- **Open the links and check that they lead to the talks.** I took the IDs from the transcript headers and didn't open them.
- **The Lauren Tan point is still pending.** In the comment I only put "(grokbot)" because the company is misspelled in the transcript ("SpaceX SI").
- **Careful with "(creator of flask)".** That fact doesn't come from the talk; I added it. In the comment I put "(earendil)", which is what the transcript says. Both are correct.

"marathon them" works really well: it's friendly and signals that there are several videos.

## 2026-11-24 09:55 · Diego

is what i added a good close, i think not, but i feel something like this is needed:

AI makes mistakes writing code. and not just a few.


it invents functions, patches instead of fixing, leaves comments justifying the patch, it's really good at comments.


the question isn't whether AI makes mistakes. it's how you use it so the code comes out right anyway.


i watched 5 ai engineer talks about this and the answer has an order: first the workshop. then the factory.


lauren tan from grokbot shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.


her secret isn't a better agent. every time the agent makes a mistake, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.



an example, they banned the use of useEffect in apps written with react, haha good rule.



armin ronacher from earendil (they created Pi) adds what can't be automated: judgment.

the agent wants to finish the task, not to make your system make sense. someone has to tell it "no, not like that".



within the flow, you have to include your review. that's why htmls or claude artifacts are important, they speed up explanations through diagrams.



that's the workshop: rules, tests, verification and human judgment.



only then does zach lloyd from warp arrive with the software factory: agents that do triage, specs, code and review, everything measured, and agents that detect their own repeated mistakes and propose how to avoid them.



the agentic software factory, lives in some environment isolated from your machine and interacts where people work: slack, coding agents... 



i'll leave the videos in the comments so you can marathon them like i did.

## 2026-11-24 09:55 · Assistant

Your version works. The irony about comments and the "haha good rule" give it your voice. I made few changes: three so that the talks are represented accurately, and the closing you felt was missing.

---

> AI makes mistakes writing code. and not just a few.
>
> it invents functions, patches instead of fixing, leaves comments justifying the patch. to be fair, it's really good at comments.
>
> the question isn't whether AI makes mistakes. it's how you use it so the code comes out right anyway.
>
> i watched 5 ai engineer talks about this and the answer has an order: first the workshop. then the factory.
>
> lauren tan from grokbot shipped 3,000 PRs to production in a month. her team, 11,000. with only 0.5% reverts.
>
> her secret isn't a better agent. every time the agent makes a mistake, she turns that correction into a rule in the code: a lint, a test, a type. not one more line in a markdown file.
>
> an example: they banned useEffect in product code. haha, good rule.
>
> armin ronacher from earendil (they work on pi) adds what can't be automated: judgment.
>
> the agent wants to finish the task, not to make your system make sense. someone has to tell it "no, not like that".
>
> that's why your review has to be inside the flow. armin asks the agent for an html summary before verifying. i use claude artifacts with diagrams: i understand in a minute what used to take me reading the whole diff.
>
> that's the workshop: rules, tests, verification and human judgment.
>
> only then does zach lloyd from warp arrive with the software factory: agents that do triage, specs, code and review, everything measured, and agents that detect their own repeated mistakes and propose how to avoid them.
>
> the factory lives in isolation, off your machine, and works where your team already works: slack, linear, github.
>
> AI is going to keep making mistakes. the difference is whether each mistake holds you back or leaves you a new rule.
>
> that's how you get speed and quality at the same time.
>
> i'll leave the videos in the comments so you can marathon them like i did.

---

**What I changed and why**
- **useEffect:** they banned it in product code, and it's only allowed inside their own framework. "In apps written with react" made it look like they ban it in any React project.
- **Pi:** in the talk Ronacher says Earendil "is working on" Pi, not that they created it. I put "they work on pi" so as not to attribute to them something the talk doesn't say. Check it if you know more.
- **HTML and artifacts:** I separated what Ronacher says (the HTML summary) from what you do (Claude artifacts). It's still your contribution, but it isn't attributed to him.
- **Where the factory lives:** Lloyd talks about cloud sandboxes connected to Slack, Linear/Jira and GitHub. "Coding agents" isn't a place where people work, so I replaced it with those tools.
- **Closing:** "speed and quality" was your goal and it had dropped out of the text. It's back in two lines, before the invitation to the videos.
