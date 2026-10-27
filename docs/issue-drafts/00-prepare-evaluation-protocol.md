# [docs] Define evaluation protocol: no-skills control, pre-registered decision rule, stability/sensitivity, two-evaluator agreement

## Context
Test whether the skill set improves communication vs. the same model without skills. Use independent rubric v0 and fix the decision rule before scoring. Include the three evidence-backed writing cases and negative gate inputs (idea only, unsupported raw material, invented results).

## Work
Draft evaluation protocol containing:
- Paired control/treatment: same model on comparable CS-paper drafts with and without skills; hold prompt/context/evaluation conditions constant.
- Corpus: source, permitted use, sampling, number of drafts per case, exclusions; decided before scoring.
- Pre-registered decision rule: metric, improvement threshold, analysis method, inconclusive reporting; justified from corpus before scoring treatment outputs.
- Rubric checks: repeated scoring for stability; deliberately degraded draft for sensitivity.
- Two-evaluator agreement if ≥2 independent evaluators score; single evaluator reports stability, no agreement claim.
- Record venue brief, skill versions, model, case, requested edit operation, claim support states, cost per arm.
- Verify G- claim and integrity gates are pass/fail outside the rubric; a failed gate produces `insufficient-evidence` or a gap list, not polished prose. Rubric measures W- communication only.

## Expected files
- `docs/evaluation.md` (new)

## Dependencies
- `00-prepare-rubric-v0.md` (rubric v0 is the instrument).
- `docs/use-cases.md` (three cases and routing examples).
- `docs/requirements.md` (single claim gate, shared states, submission gate, G-/C- provenance).

## Acceptance criteria
- [ ] Protocol document exists in English.
- [ ] Control/treatment use matched model/input conditions; differences documented.
- [ ] Corpus selection, sample size per case, metric, threshold, analysis method fixed before scoring.
- [ ] Stability and sensitivity checks specified with reproducible inputs.
- [ ] Agreement only if ≥2 independent evaluators; single evaluator reports stability, no agreement claim.
- [ ] Records model, skill versions, venue brief if supplied, case, edit operation, and cost for both arms.
- [ ] Negative inputs test that an idea alone or unsupported raw material cannot trigger paper prose.
- [ ] G- gate outcomes are reported separately as pass/fail and never treated as communication-rubric scores.

## Notes
- Do not invent universal sample size or agreement threshold; justify before running evaluation.
- Case and requested edit operation are recorded per draft for disaggregation.

## Copyright constraints
- Original synthesis only. No quoted/excerpted book text.

## Depends on
- #00-prepare-rubric-v0
