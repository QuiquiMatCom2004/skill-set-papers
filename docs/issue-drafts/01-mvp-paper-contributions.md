# [feat] Create paper-contributions skill

## Context
This first MVP skill implements W-01: it selects and formulates a contribution from existing research material or an existing CS-paper draft. An idea alone is outside the writing cases. `docs/use-cases.md` defines `material-no-draft`, `partial-draft`, and `complete-draft`; `docs/requirements.md` defines the single factual-claim gate.

## Work
Create `skills/paper-contributions/SKILL.md` with standard Agent Skills YAML frontmatter (`name`, `description`) and lean instructions. The skill must:

- Accept the case-specific research index and material or draft. Propose claim IDs and evidence pointers from supplied records, then require author confirmation of claim class, support status, scope, and wording.
- Apply the same rule used throughout the paper: a factual claim needs an author-confirmed ID, resolvable pointer to real support, and wording no broader than that material demonstrates or argues. At least one central claim must pass to enter writing. This checks traceability and scope, not scientific correctness.
- Where a broad claim fails, offer a narrower claim that the material supports. If none passes, return `insufficient-evidence` with an exact material-gap list and no paper prose, outline, or introduction.
- Select and formulate a versioned Vision / Steps / News / Contributions block referencing supported claim IDs. Do not duplicate the claim register or venue brief. Record dependencies so a change in evidence, claim scope, or block meaning triggers review of affected output.
- State when to use, when not to use, and where to route outlining or focused editing. Enforce G- as pass/fail; map the skill's communication purpose to W-01.

## Expected files
- `skills/paper-contributions/SKILL.md`; optional sibling files for extended material.

## Dependencies
- `docs/principles.md` from `00-prepare-principles.md` for the verified W-01 anchor.
- `docs/use-cases.md` and `docs/requirements.md` for cases and the claim gate.

## Acceptance criteria
- [ ] Standard Agent Skills frontmatter and lean, portable instructions exist.
- [ ] Idea-only and raw-data-only inputs with no supported central claim return `insufficient-evidence` and a gap list, with no paper prose.
- [ ] A theorem with a complete proof or a bounded measured result can pass after author confirmation; an overbroad performance claim is narrowed or blocked.
- [ ] Output carries a version and claim IDs; changes in relevant evidence, scope, or block meaning trigger review of dependent output.
- [ ] Use / do-not-use / next-skill conditions and W-01 traceability are explicit.
- [ ] No book excerpts, tool code, or harness code are shipped.

## Copyright constraints
Original synthesis only. Never quote, excerpt, commit, or distribute the private PDF or `.txt`.

## Depends on
- #00-prepare-principles
