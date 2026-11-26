---
status: proposed
origin: diego
updated: 2026-11-24
superseded_by:
---

# Plan: core-definition v1

**State:** planned. Phase 0 is done (evidence and diagnosis); nothing else starts until Diego says go.
**Diagnosis:** [DIAGNOSIS.md](DIAGNOSIS.md)

This is a definition project. It produces documents in this folder and one ADR; it writes nothing in `core/` and no code ([ADR 0005](../../../decisions/0005-documentation-before-code.md)). Woku is the case the definitions are tested against; woku specifics go to woku's private vault ([ADR 0008](../../../decisions/0008-telar-is-a-method-and-framework.md)).

## Goal

Observable scenarios. The iteration is done when all of them hold.

1. **S1, the lifecycle.** Diego walks a woku work item, from the first need through research, requirement, build, verification, production and an incident afterwards, through the lifecycle model. For every stage he can read what the system may decide, what a person keeps, what evidence lets work advance, and what lands in the dossier.
2. **S2, the catalog.** Every candidate non-negotiable has a level (T, M, B, P), an enforcement point, its sources, and Diego's decision: accepted, rejected or deferred. No open contradiction (C1 to C12) remains without a decision.
3. **S3, the woku test.** Applying the project baseline to woku produces, in woku's private vault, a list of what woku's repositories already have and what is missing, concrete enough to plan work from. This repository only records that the analysis exists and what it taught about the baseline.
4. **S4, a rule end to end.** A real correction (C-0001 or C-0002, plus at least two woku corrections recorded privately) can be modeled with the rule model: origin, layer, enforcement point, owner, and how its effect is measured.
5. **S5, the structure.** An ADR, accepted by Diego, states what `core/` will contain (derived only from accepted T and M rows and the formats inventory), what it will never contain (P rows), and which follow-up project builds it.

## Open decisions

Asked before the phase that needs them. Answering one is not a go.

| ID | Question | Options | Recommendation | Decision |
|---|---|---|---|---|
| D1 | Context policy (C2) | (a) compact above 50%; (b) a fresh session per stage from the dossier, native compaction inside a stage; (c) both, with (b) as the default | (c): the evidence against a fixed threshold is strong (CompAct-Bench), and a fresh session per stage already gives handoff | |
| D2 | Where "done" is for version zero (C10) | (a) merged; (b) verified in production | (b) as the definition, with the line ending at merge in version zero and production verification as an explicit later step, so the gap stays visible | |
| D3 | Research stage in the first line (C11) | (a) its own stage with output and gate; (b) part of the spec stage | (a), because R2 says research can change or cancel the requirement, and that needs its own decision | |
| D4 | When the isolated, always-on environment arrives (C1) | (a) in version zero; (b) as a later profile with entry criteria | (b), with entry criteria written in phase 6 | |
| D5 | Level taxonomy | Accept T, M, B, P as defined in the diagnosis, or change it | Accept | |
| D6 | Names (C9) | Format namespace, work item prefix, folder name in project repositories | Decide in phase 5 | |
| D7 | Where woku's private analysis lives | Woku's engineering vault or a new private repository | Woku's engineering vault | |

## Phases

Each phase ends with a document in this folder that Diego reviews. The next phase starts after his OK.

### Phase 0: evidence and diagnosis (done 2026-11-24)

- [x] Research conversations, documents, prototype and figures translated into [`vault/evidence/`](../../../evidence/README.md), with provenance and redactions.
- [x] [DIAGNOSIS.md](DIAGNOSIS.md): evidence inventory, Diego's requirements R1 to R19, settled decisions, process model, contradictions, levels, candidate non-negotiables, baseline, gaps.
- [ ] Diego reviews the diagnosis.

### Phase 1: lifecycle model (S1)

- [ ] Finish reading E5 (paper), E8 (multi-project) and E10 (Warp adaptation) and update the inventory.
- [ ] Write `lifecycle.md`: the creation stages from intake to production and the four operation processes. Per stage: purpose, what the system may decide, what a person keeps, the gate and its evidence, what the dossier gains, the unit of outcome.
- [ ] Map it against the version zero line of the kit design and mark what version zero covers.
- [ ] Ask D2 and D3 before writing the research and release stages.
- [ ] Verification: walk two examples through it (the daily cash closing from E6 and the support agent from E7 and E10); record where the model failed to answer.

### Phase 2: non-negotiables catalog (S2)

- [ ] Write `non-negotiables.md` from N-01 to N-44 plus whatever phase 1 adds. Each row: statement, level, enforcement point, sources, version (zero or later).
- [ ] Ask D1, D4 and D5.
- [ ] Diego decides each row. Rejected rows stay in the file with the reason.
- [ ] Verification: no row without level, enforcement point and decision; no contradiction C1 to C12 left open.

### Phase 3: project baseline (S3)

- [ ] Write `project-baseline.md`: what any project repository must provide (B-1 to B-11 and changes), minimum versus recommended, and how Telar would check each item.
- [ ] Ask D7. In woku's private vault, analyze woku's repositories against the baseline.
- [ ] Bring back to this folder only the generic lessons (items that were unclear, missing or wrong).
- [ ] Verification: the woku analysis exists and Diego finds it actionable.

### Phase 4: rule model (S4)

- [ ] Write `rule-model.md`: what a rule is in Telar (origin, layer, enforcement point, owner, evidence of effect, status), its lifecycle (correction, proposed, encoded, measured, retired), and how it relates to the corrections ledger, the manifest and the checks.
- [ ] Model C-0001 and C-0002 here, and at least two woku corrections in woku's private vault.
- [ ] Verification: each modeled rule can say how its effect would be measured.

### Phase 5: formats inventory

- [ ] Write `formats.md`: every format the core must define (manifest, dossier and its files, run record, decision record, correction, rule record, verification artifact, metrics row), with fields taken from the kit design, Telar names (D6), level, and versioning policy. Prose and tables only; no schema files.
- [ ] Verification: every T and M row of the catalog points to the format that carries it, or says it needs none.

### Phase 6: maturity model

- [ ] Write `maturity.md`: one sequence from R15, the talks, ADR 0006 and the kit roadmap, with entry criteria for each step (including the isolated environment, D4).
- [ ] Propose the fate of [ADR 0006](../../../decisions/0006-workshop-before-factory.md): accept as revised, or supersede.
- [ ] Verification: woku's current position in the sequence can be stated.

### Phase 7: core structure (S5)

- [ ] Write an ADR (proposed) with the structure of `core/`: what it contains, organized from the accepted catalog and formats; what it will never contain; what stays in project repositories.
- [ ] Propose the follow-up project that builds version zero of the core, as a `proposed` plan.
- [ ] Verification: Diego accepts the ADR.

### Phase 8: closeout

- [ ] `CLOSEOUT.md`: what was learned, corrections raised and how they were encoded, what moves to the build project.

## Out of scope

- Any code, schema file or configuration in `core/` or elsewhere.
- Woku's domain rules and any woku-internal detail in this repository.
- Telar developed with Telar, and a public example project (later, per ADR 0008).
- Choosing tools beyond what the evidence already settled; designing the isolated environment, channels or a database.

## Log

- 2026-11-24: Diego set this as the first project: "the first project is to define the structure of core, which are the non-negotiables; there is a lot of information in the OpenResearch sessions, for example YAML, lint, tests; the idea is to put it in order and distinguish what is at repository level (the project, woku in this first case) and what is Telar's; there is a lot to define before doing anything in core; for example the proposed model that goes from research to production has several stages" (translated). He also said the work was being taken too lightly (C-0002) and that all the chats are extremely important and belong in the vault as evidence, translated.
- 2026-11-24: Phase 0 done: evidence translated into `vault/evidence/`, diagnosis written. Plan written. Status `proposed`.
- 2026-11-26: Diego changed the first installation from woku to wondeya, a new private project started from zero. [ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md) is `proposed`. If it is accepted, a v2 retargets S3 and S4 to wondeya and adds the question of what "the current way of working" means in a project with no history; this iteration keeps its status.
