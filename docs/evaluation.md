# docs/evaluation.md — Evaluation protocol: skills vs. no-skills control

## Status

Planning draft. Original synthesis only. This document contains no book text, no skill code, no tool or harness code, no commit references, and no GitHub issue references. It references `rubric/v0.md` and `docs/principles.md` by path and version only; it does not reproduce their content.

## 1. Purpose

This protocol executes a fair, controlled comparison of the same coding-assistant model on matched Computer Science paper tasks, once with the project's four writing skills enabled (`paper-outline`, `paper-opening`, `paper-ending`, plus `paper-contributions`) (treatment arm) and once without them (control arm). It measures whether the skills improve *communication quality* as scored by rubric v0, while keeping research-integrity and venue-compliance gates separate from communication scores. `paper-venue` runs before the comparison and is outside it.

Scope: CS papers only — empirical, theoretical, systems/design, survey/review, and position/vision — in any venue format (conference, journal, preprint), including figures inside those papers. Out of scope: books, presentations, and papers from other disciplines, per `PROBLEM.md` and `AGENTS.md`.

The four skills compared are `paper-contributions`, `paper-outline`, `paper-opening`, and `paper-ending` (treatment). `paper-venue` is executed before the comparison and is outside it; the same brief is used for both arms. The control arm uses the same model with none of them enabled. Skill names appear here only as arm labels; no skill text is reproduced.

## 2. Arms and matched conditions

Both arms are identical except for skill enablement:

- **Treatment arm:** the model performs the requested writing/edit operation with the four writing skills enabled.
- **Control arm:** the same model performs the same requested operation on the same input with no skills enabled.

Matched conditions (held constant across arms for each draft):

1. Same model name/version and fixed sampling parameters (temperature, top_p, seed where supported).
2. Same input draft (or no draft, per case) and same requested edit operation (`local-edit`, `restructure`, `venue-adapt`, or draft formulation for `material-no-draft`).
3. Identical **author-confirmed claim inventory** and identical **evidence packet** supplied to both arms. The inventory lists each claim ID, claim class (empirical/theoretical/design/literature-based/position), support status (`planned`/`partially_supported`/`supported`), resolvable material pointer or explicit gap, and permitted scope. The evidence packet contains the referenced supporting material. Both are versioned and frozen before scoring. The no-skills baseline is therefore *not* penalized for missing internal skill metadata: it receives the same claim IDs, pointers, and material as the treatment arm.
4. Same ready venue brief (produced by `paper-venue`, with explicit `named-venue` or `generic` mode and source/access dates) supplied to both arms for outline, opening, ending, restructure, venue adaptation, or submission tasks. Only a narrow `local-edit` outside those operations may have no brief; record `venue_brief: none` for both arms.
5. Same prompt template structure; the only difference is the skill enablement flag. No skill-specific hints, examples, or internal metadata leak into the control prompt.

Per-draft records for both arms capture: model, skill versions (treatment) or "none" (control), ready venue brief or `venue_brief: none` for an eligible `local-edit`, case, requested edit operation, claim-inventory version, evidence-packet version, normalized rubric score, G- gate result, C- venue result, and cost per arm.

## 3. Corpus sourcing, permissions, and contamination avoidance

### Corpus sourcing

The corpus is a set of CS-paper drafts (or draft-start materials) drawn only from material the project is permitted to use. Acceptable sources:

- Drafts authored by the project or by contributors who have granted written permission for their use in this evaluation.
- Previously completed project drafts where the author has confirmed reuse rights.
- Synthetic matched drafts constructed by the project solely for this protocol, clearly labeled as synthetic, never presented as real research.

Sources must be recorded with: origin, author, permission status, license or reuse terms, paper type, and whether it contains a graph (relevant to R-6). Papers from other disciplines, books, and presentations are excluded.

### Permissions

No draft enters the corpus without the author's confirmed permission for evaluation use. Permission is recorded per draft (who granted it, when, and under what terms). Drafts without confirmed permission are excluded. Missing venue rules are left UNKNOWN, never invented.

### Contamination avoidance

To keep the comparison fair and the scores meaningful:

- The same source draft or evidence packet is input to both arms. Each arm's output is stored and scored separately; an output from one arm is never used as input to the other.
- Evaluators never see both arms' outputs for the same draft in a way that reveals arm assignment (see blinding, section 8).
- Corpus drafts are checked for overlap with the model's training data where feasible; any confirmed overlap is recorded as an exclusion or noted as a limitation.
- Drafts are deduplicated by content hash before sampling; near-duplicates are excluded or grouped and recorded.

### Sampling and exclusions

Selection, sample size per case, and exclusion rules are fixed *before confirmatory scoring* (section 6). Sample size per case is not a universal constant: choose a practically meaningful margin first, then use independent pilot or baseline variability to estimate the sample size needed to detect it. If no corpus exists, sample size remains undetermined (section 10.3).

## 4. Cases and routing covered

The protocol exercises all three writing cases plus negative unsupported-idea routing, each with examples spanning empirical/theoretical/systems/survey/position paper types. Routing follows `docs/use-cases.md`; example numbers below refer to that document's routing table.

### material-no-draft

No paper prose exists; at least one supported central claim is required at entry.

- Empirical: measurements with protocol, no prose → outline and result prose bounded by the measured result (use-cases example 1).
- Theoretical: stated theorem with complete proof, no prose → theoretical prose backed by the proof (example 2).
- Systems/design: implemented system with documented observation, no prose → describe the observed property, not unmeasured superiority (example 3).
- Survey/review: verified source corpus and documented gap, no prose → survey or position argument limited to those sources (example 4).
- Position/vision: documented gap grounded in verifiable sources, no prose → position argument limited to those sources.

### partial-draft

An incomplete draft with a supported central claim.

- Empirical partial draft: diagnose and revise supported passages, draft missing supported sections.
- Theoretical partial draft: complete a supported lemma's prose; leave unsupported claims as gaps.

### complete-draft

A full draft with a supported central claim.

- Systems/design complete draft: `venue-adapt` to a named venue; requires a current venue brief before any compliance claim (example 8).
- Position complete draft: `local-edit` on one paragraph; preserve meaning and citations (example 7).
- Complete draft with one-paragraph edit request: diagnose first, then edit meaning-preservingly.

`local-edit` is a requested edit operation (passage + nearby context + intended meaning), not a writing case or a skill. It is tested with generic editing instructions applied identically in both arms, and it is not functionality owned by `paper-outline` (which arranges the supported contribution into a route and does not write body prose). No MVP skill owns arbitrary body-paragraph editing: body-paragraph edits occur only as the `local-edit` operation, with meaning- and citation-preserving instructions, and only when a supported central claim exists.

### Negative unsupported-idea routing (must not produce paper prose in either arm)

- Only an idea or question, no supporting material → `insufficient-evidence`; list needed research, no prose (example 9).
- Only raw data or code, no bounded central claim they support → `insufficient-evidence`; identify needed analysis or observation (example 10).
- Request to invent results, proofs, or citations → no factual draft; gap list or marked scaffold only (example 11).

The negative test asserts that the treatment arm must not convert an unsupported idea, raw material, or invented content into paper prose. Control-arm behavior is recorded separately; a control failure does not invalidate the communication comparison, but a treatment failure blocks a positive claim about the skill set's safe operation.

## 5. What is scored: normalized communication score

Rubric v0 scores communication only (W- principles). Each scored criterion is rated 0/1/2:

- R-1 Contribution clarity (W-01)
- R-2 Route coherence (W-02)
- R-3 Opening orients (W-03)
- R-4 Abstract fidelity (W-04)
- R-5 Ending states contributions (W-05)
- R-6 Graph readability (W-06) — conditional; N/A when the paper has no graph
- R-7 Signal strength (W-08)

W-07 is excluded (review-process principle, not a paper property). G- integrity gates and C- venue compliance are pass/fail/unknown outside the rubric and are never assigned rubric points.

### Normalization (graph criterion may be N/A)

Because R-6 is N/A for papers without a graph, the denominator differs across drafts. The normalized score per draft is:

```
normalized score = (sum of scored criteria) / (max possible for that draft) × 100
```

- No graph: scored on R-1..R-5 and R-7, max 12 → report `X/12 (N%)`, list R-6 as N/A.
- With graph: scored on all seven, max 14 → report `X/14 (N%)`, list no N/A.

The primary analysis compares mean normalized scores (percentage points) between arms on matched **complete-paper outputs**. For `material-no-draft` and `partial-draft` tasks, both arms use the same generic body-drafting instructions and evidence packet to reach a complete draft; only skill enablement differs. If a task yields only an outline or section, it is evaluated for routing and artifact-specific behavior, not included in the full-paper rubric mean. The raw `X/Y` and N/A list accompany every scored complete draft.

## 6. What must be frozen before scoring

The following are fixed and recorded before any treatment output is scored. Changing any item after scoring begins requires a new protocol run and voids prior results.

1. **Corpus:** drafts selected, case assignment per draft, number of drafts per case, exclusion rules, permissions confirmed per draft.
2. **Claim inventory and evidence packet:** versioned and identical for both arms (section 2).
3. **Model:** name/version and fixed sampling parameters, identical across arms.
4. **Skill versions:** treatment arm skill versions recorded; control arm recorded as "none".
5. **Prompt template:** identical structure across arms; only the skill enablement flag differs; requested edit operation recorded per draft.
6. **Venue brief:** freeze the same ready brief with explicit `named-venue` or `generic` mode and field provenance for both arms. Only an eligible narrow `local-edit` may record `venue_brief: none` for both arms. Generic mode makes no venue-compliance claim; a pending shortlist is not a ready brief.
7. **Rubric version and scoring procedure:** rubric v0, 0/1/2 anchors, normalization rule, N/A handling.
8. **Evaluators and blinding:** who scores, how many, whether blinded, and the blinding procedure (section 8).
9. **Decision rule:** metric, practically meaningful threshold Δ* justified before confirmatory treatment scoring, α level if a significance test is used, analysis method, and inconclusive handling (section 10).
10. **Cost recording:** method and currency for cost per arm.

## 7. Prompt controls

- The treatment and control prompts share one template; the only controlled difference is whether the four writing skills are active.
- The requested edit operation (`local-edit`, `restructure`, `venue-adapt`, or draft formulation) is the same for both arms on a given draft.
- No skill-specific instructions, internal skill metadata, claim IDs from the skill's internal register (beyond the shared claim inventory), or tool names are injected into the control prompt.
- The control arm's output is generated by the same model under the same sampling parameters as the treatment arm.

## 8. Evaluators and blinding

### Blinding (if feasible)

Where feasible, scoring is blind: evaluators receive anonymized, shuffled drafts and are not told which arm produced each output or which version of the skill set was used. Arm assignment is revealed only after scoring is complete. If full blinding is not feasible (e.g., a single evaluator who also generated the outputs), the limitation is recorded and no blinding claim is made.

### Agreement

- **≥2 independent evaluators:** compute agreement on each ordinal criterion (for example, weighted kappa or Krippendorff's alpha) and agreement on the continuous normalized score using a suitable measure such as an intraclass correlation or absolute score differences. Report agreement per case and overall. Do not average scores without reporting their agreement.
- **Single evaluator:** report scoring stability only (repeat scoring after a washout, section 9.1). No inter-evaluator agreement claim is made.

## 9. Rubric stability and sensitivity (reproducible inputs)

### 9.1 Stability (repeat scoring)

Rescore a fixed subset of drafts (e.g., 20% of the corpus, or a fixed minimum number, pre-registered) after a washout period by the same evaluator(s). Report intra-evaluator stability: agreement between the two scorings of the same draft, per criterion and on the normalized score. Instability beyond a pre-registered tolerance triggers a scoring-procedure review before results are finalized.

### 9.2 Sensitivity (deliberately degraded draft)

Verify the scoring procedure detects a communication failure. Construct a deliberately degraded draft fixture by applying one reproducible degradation to a valid draft, for example:

- burying the contribution so it is never stated explicitly (targets R-1),
- scrambling section order so the route no longer leads to the contribution (targets R-2),
- opening with background only and never stating the problem, approach, or route (targets R-3),
- an abstract that claims a result absent from the body (targets R-4),
- an ending that only replays section headings (targets R-5),
- a graph with a truncated/misleading scale or unlabeled axes (targets R-6), or
- the core idea called by three inconsistent names and absent from abstract/headings (targets R-7).

The degraded draft and the exact degradation operation are recorded as reproducible fixtures. The rubric must assign a measurably lower score to the degraded draft than to the original in both arms' scoring. If it does not, the scoring procedure is revised before results are finalized.

## 10. Decision rule, threshold, and analysis

### 10.1 Metric

Primary metric: mean normalized communication score difference (treatment − control) in percentage points, paired by draft, on the shared corpus.

### 10.2 Threshold Δ* justified from the corpus (not invented)

The improvement threshold Δ* (minimum mean normalized-score gain required to claim the skills help communication) is pre-registered *before* scoring treatment outputs and must be justified from the chosen corpus, not invented as a universal constant. Acceptable justifications include:

- a practical margin tied to the rubric anchors and the paper types in the chosen corpus, decided by the project before confirmatory treatment outputs are scored; or
- a separate calibration pilot that is excluded from the confirmatory corpus, used to choose and justify a meaningful margin and estimate variability.

Choose Δ* for practical meaning first. Then use pilot or baseline variability to estimate the sample size needed to detect that margin. Do not define Δ* from the same confirmatory treatment scores used to test it.

A universal constant (for example, "+1 point" or "+10%" regardless of corpus) is explicitly forbidden.

### 10.3 Pre-run gate when no corpus exists

At protocol-authoring time no scored or scoreable corpus exists in this repository. Therefore the explicit pre-run gate is:

> **Corpus pre-run gate:** before any confirmatory treatment output is scored, a corpus must be selected, permissions confirmed, Δ* justified and frozen, and a feasible sample size and analysis method fixed from an independent pilot or baseline estimate. If the corpus is too small for a meaningful significance test, pre-register a descriptive paired analysis and label its conclusion exploratory. Until this gate passes, the evaluation result is **PENDING**. No validation or improvement claim is made.

The result remains PENDING until the gate passes. Do not falsely claim validation.

### 10.4 Analysis method

- Paired comparison on matched complete drafts: report mean normalized score per arm, mean difference in percentage points, and uncertainty appropriate to the pre-registered sample size. Use a one-sided paired significance test only if its method, assumptions, and α were frozen before confirmatory scoring; otherwise report a descriptive paired analysis without a significance claim.
- Disaggregate by case (`material-no-draft`, `partial-draft`, `complete-draft`) and by paper type (empirical/theoretical/systems/survey/position) so effects are not hidden by aggregation.
- Report negative-route results separately for both arms. Treatment production of factual prose from unsupported input is a gate failure; control behavior is a comparison result.
- Report G- gate results (PASS/FAIL) and C- venue results (PASS/FAIL/UNKNOWN) per arm and per draft, separate from communication scores. `paper-venue` runs before the comparison and is outside it; the same brief feeds both arms.
- Report cost per arm and per draft.

### 10.5 Decision and inconclusive results

Claim "the skills improve communication" only when all of the following hold:

1. mean normalized-score difference ≥ Δ* (threshold justified from the corpus),
2. the pre-registered uncertainty or significance criterion supports the difference when the confirmatory design has adequate power,
3. G- gates PASS for the treatment outputs being claimed, and
4. the treatment arm passed the negative-route test.

Otherwise the result is **inconclusive** or **no support**, and is reported as such. Specific inconclusive conditions:

- The pre-registered uncertainty criterion does not support a positive difference, or the observed mean difference is below Δ*. In an exploratory run, report the estimated difference without a confirmatory claim.
- G- gate FAIL for a treatment output (that output is blocked regardless of rubric score).
- C- venue result UNKNOWN where a venue-specific claim was requested (no compliance claim is made).
- Contamination, permissions, or blinding failure detected.
- Pre-run gate not satisfied (result PENDING, section 10.3).

Inconclusive results are never re-analyzed post-hoc to force a positive conclusion; a new protocol run with a corrected corpus or procedure is required.

## 11. Cost

Cost per arm (and per draft) is recorded: model-inference cost estimate or actual cost, in a stated currency, plus any evaluator cost if applicable. Cost is reported alongside effectiveness so the comparison is cost-aware, not outcome-only.

## 12. Reproducibility

A full run record is archived per protocol run and includes everything in section 6 plus: corpus hashes, claim-inventory and evidence-packet versions, model and sampling parameters, skill versions, prompt template, venue brief (if any), rubric version, evaluator list and blinding status, per-draft raw `X/Y` and normalized scores with N/A lists, G- and C- results per draft, cost per arm, agreement/stability/sensitivity results, and the final decision (supported / inconclusive / PENDING). Any item in section 6 changed after scoring invalidates the run.

## 13. Execution blockers (at protocol-authoring time)

The following blockers prevent executing this protocol now:

1. **No corpus exists.** No scored or scoreable CS-paper corpus with confirmed author permissions is present in the repository. The corpus pre-run gate (section 10.3) is unsatisfied; the result is PENDING. A corpus must be selected, permissions confirmed, and Δ* justified from it before scoring.
2. **No frozen skill versions.** The five skills (including intake skill `paper-venue`) are implementation drafts in this branch; their content must be reviewed and versioned, `paper-venue` among them, before a treatment run can be reproduced.
3. **No evaluators appointed.** No independent evaluator(s) are named, and blinding feasibility is unassessed.
4. **No baseline/variance data.** Without a scored corpus there is no baseline variability from which to derive Δ* or a per-case sample size.

Until these are resolved, no evaluation is run and no validation claim is made.
