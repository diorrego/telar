---
status: proposed
origin: diego
updated: 2026-11-26
superseded_by:
---

# Plan: core-definition v2

**State:** planned. Phase 0 is done (this iteration's diagnosis); nothing else starts until Diego says go.
**Diagnosis:** [DIAGNOSIS.md](DIAGNOSIS.md), which carries the [v1 diagnosis](../v1/DIAGNOSIS.md).

This iteration keeps v1's goal and retargets it to the first installation of [ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md): a new product started from zero, built by one engineer, in a local repository until its first MVP. It produces documents in this folder and one ADR; it writes nothing in `core/` and no code ([ADR 0005](../../../decisions/0005-documentation-before-code.md)). Everything specific to the installation goes to its private vault.

## Goal

Observable scenarios. The iteration is done when all of them hold.

1. **S1, the lifecycle.** Diego walks a real work item of the first installation, from the first need through research, requirement, build, verification, release and an incident afterwards, through the lifecycle model. For every stage he can read what the system may decide, what a person keeps, what evidence lets work advance, and what lands in the dossier.
2. **S2, the catalog.** Every candidate non-negotiable has a level (T, M, B, P), an enforcement point, its sources, and Diego's decision: accepted, rejected or deferred. The catalog states its scope: it governs how software is built and released in the workshop, not what a product does for its users ([C-0005](../../../qa/corrections/C-0005-product-proposed-through-its-risks.md)). No open contradiction (C1 to C12) remains without a decision.
3. **S3, the baseline built.** As the first installation creates its repository, it records in its private vault the order in which each baseline item entered, what it cost, and, for each item that assumes a forge, its local equivalent or that it waits for one. This repository records only the generic lessons.
4. **S4, a rule end to end.** C-0001 to C-0005, plus at least two corrections recorded privately by the installation, can be modeled with the rule model: origin, layer, enforcement point, owner, and how its effect is measured.
5. **S5, the structure.** An ADR, accepted by Diego, states what `core/` will contain (derived only from accepted T and M rows and the formats inventory), what it will never contain (P rows), and which follow-up project builds it.
6. **S6, measurement without history.** A measurement protocol for a project with no current mode is written and applied by the installation from a stated work item on; its first numbers are reported here without the installation's details.

## Open decisions

Asked before the phase that needs them. Answering one is not a go.

| ID | Question | Options | Recommendation | Decision |
|---|---|---|---|---|
| D1 | Context policy (C2) | (a) compact above 50%; (b) a fresh session per stage from the dossier, native compaction inside a stage; (c) both, with (b) as the default | (c): the evidence against a fixed threshold is strong (CompAct-Bench), and a fresh session per stage already gives handoff | |
| D2 | Where "done" is for version zero (C10) | (a) merged; (b) verified in production | (b) as the definition, with the line ending at merge in version zero and production verification as an explicit later step, so the gap stays visible | |
| D3 | Research stage in the first line (C11) | (a) its own stage with output and gate; (b) part of the spec stage | (a), because R2 says research can change or cancel the requirement, and that needs its own decision. Diego said research "is always part of Telar's framework and method" (2026-11-26) | |
| D4 | When the isolated, always-on environment arrives (C1) | (a) in version zero; (b) as a later profile with entry criteria | (b), with entry criteria written in phase 6 | |
| D5 | Level taxonomy | Accept T, M, B, P as defined in the v1 diagnosis, or change it | Accept | |
| D6 | Names (C9) | Format namespace, work item prefix, folder name in project repositories | Decide in phase 5 | |
| D7 | Where the installation's private analysis lives | Its own private vault | Settled by ADR 0010 | Its private vault |
| D8 | Measurement protocol without history (S6) | (a) per-item records from the first item, compared over time; (b) alternate Telar's line by hand with a person and an interactive agent; (c) both | (a) from the start, (b) once the installation has enough comparable items | |

## Phases

Each phase ends with a document in this folder that Diego reviews; the next phase starts after his OK. A phase that needs the installation's work runs when the installation has produced it (noted per phase).

### Phase 0: diagnosis (done 2026-11-26)

- [x] [DIAGNOSIS.md](DIAGNOSIS.md): what changed since v1.
- [ ] Diego reviews it.

### Phase 1: lifecycle model (S1)

- [ ] Finish reading E5, E8 and E10 and update the inventory (carried from v1).
- [ ] Write `lifecycle.md`: the creation stages from intake to production and the four operation processes. Per stage: purpose, what the system may decide, what a person keeps, the gate and its evidence, what the dossier gains, the unit of outcome.
- [ ] Ask D2 and D3 before writing the research and release stages.
- [ ] Verification: walk two examples from the evidence and one real work item of the installation (U1) through it; record where the model failed to answer.

### Phase 2: non-negotiables catalog (S2)

- [ ] Write `non-negotiables.md` from N-01 to N-44 plus whatever phase 1 adds, with the scope statement of S2. Each row: statement, level, enforcement point, sources, version.
- [ ] Ask D1, D4 and D5. Diego decides each row; rejected rows stay with the reason.
- [ ] Verification: no row without level, enforcement point and decision; no contradiction C1 to C12 left open.

### Phase 3: project baseline (S3)

Runs while the installation creates its repository and adds its first checks.

- [ ] Write `project-baseline.md`: B-1 to B-11 and changes, minimum versus recommended, how Telar would check each item, and for each forge-dependent item its local equivalent or that it waits for a forge.
- [ ] The installation records the order and cost of each item in its private vault.
- [ ] Verification: the installation's record exists and Diego finds it actionable; this folder holds only the generic lessons.

### Phase 4: rule model (S4)

Runs once the installation has logged corrections of its own.

- [ ] Write `rule-model.md`: what a rule is (origin, layer, enforcement point, owner, evidence of effect, status), its lifecycle, and how it relates to the corrections ledger, the manifest and the checks.
- [ ] Model C-0001 to C-0005 here, and at least two of the installation's corrections in its private vault.
- [ ] Verification: each modeled rule can say how its effect would be measured.

### Phase 5: formats inventory

- [ ] Write `formats.md`: every format the core must define (manifest, dossier and its files, run record, decision record, correction, rule record, verification artifact, metrics row), plus the template changes proposed by C-0004 and C-0005, with Telar names (D6), level and versioning policy. Prose and tables only.
- [ ] Verification: every T and M row of the catalog points to the format that carries it, or says it needs none.

### Phase 6: maturity model and measurement (S6)

Runs once the installation has comparable work items, at the latest during its pilot.

- [ ] Ask D8. Write `measurement.md`: the protocol for a project with no history.
- [ ] Write `maturity.md`: one sequence with entry criteria for each step (including the isolated environment, D4), and propose the fate of [ADR 0006](../../../decisions/0006-workshop-before-factory.md).
- [ ] Verification: the installation's position in the sequence can be stated, and its first numbers under the protocol are reported here without its details.

### Phase 7: core structure (S5)

- [ ] Write an ADR (proposed) with the structure of `core/`; propose the follow-up project that builds version zero as a `proposed` plan.
- [ ] Verification: Diego accepts the ADR.

### Phase 8: closeout

- [ ] `CLOSEOUT.md`: what was learned, corrections raised and how they were encoded, what moves to the build project.

## Out of scope

- Any code, schema file or configuration in `core/` or elsewhere.
- The installation's domain rules, users, data and any internal detail; about it, this repository says only that it is a new product started from zero.
- Woku, while paused; Telar developed with Telar, and a public example project (later, per ADR 0008).
- Choosing tools beyond what the evidence already settled.

## Log

- 2026-11-26: Diego accepted [ADR 0010](../../../decisions/0010-first-installation-is-a-new-project.md). This iteration opened in the same commit, superseding [v1](../v1/PLAN.md): S1, S3 and S4 retargeted to the new first installation, D7 settled by the ADR, S6 and D8 added for measurement without history, and the catalog's scope statement added to S2 from C-0005. Status `proposed`.
