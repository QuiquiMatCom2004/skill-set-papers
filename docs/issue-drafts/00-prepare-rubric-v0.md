# [docs] Draft rubric v0 independent of skills

## Context
Rubric is the acceptance test for skill changes: a skill change should measurably improve rubric scores on sample drafts, not merely read well. Rubric v0 must exist before skills and be independent of them (no skill names in criteria). Per approved decision, G- gates are PASS/FAIL and not rubric-scored; rubric measures W- communication only.

## Work
Draft rubric v0 as a standalone document:
- Evaluation criteria, each mapped to one or more principle IDs from `docs/principles.md`.
- Scoring scale (levels or numeric) defined without reference to skills.
- Guidance for applying to CS-paper drafts (conference/journal/preprint, figures in scope).
- Statement that rubric v0 is independent of skills; skill names not used in criteria.
- Statement that G- integrity gates are PASS/FAIL outside the rubric; rubric scores W- communication only.

## Expected files
- `rubric/v0.md` (new)

## Dependencies
- `00-prepare-principles.md` (principle IDs must exist first).
- `docs/requirements.md` (G- PASS/FAIL, not rubric-scored).

## Acceptance criteria
- [ ] Rubric v0 draft exists in English.
- [ ] Every criterion maps to ≥1 principle ID from `docs/principles.md`.
- [ ] No criterion references a specific skill name.
- [ ] Each criterion has observable scoring anchor per level, including low-scoring example, applicable to CS-paper draft.
- [ ] Figures inside papers in scope of rubric.
- [ ] G- gates declared PASS/FAIL, not rubric-scored; W- communication only scored.

## Notes
- `rubric/` directory does not exist yet; create it for this deliverable. Derive criteria from principles, not from skills.

## Copyright constraints
- Original synthesis only. No quoted/excerpted book text.

## Depends on
- #00-prepare-principles
