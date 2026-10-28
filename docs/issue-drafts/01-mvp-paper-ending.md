# [feat] Create paper-ending skill

## Context
This fourth writing skill implements W-05. It writes or revises a closing from a complete body and supported contribution, in `partial-draft` after completion or `complete-draft` during revision. A ready brief from `paper-venue` supplies known heading rules; it does not change the contribution-centered content.

## Work
Create `skills/paper-ending/SKILL.md` in standard Agent Skills format. The skill must:

- Require a current contribution block, complete body, and supported central claim IDs. If any required claim fails the factual-claim rule, return the exact gap rather than an affirmative closing.
- State only contributions demonstrated or argued by the body; do not merely replay section headings or increase claim strength.
- Require a ready brief from `paper-venue`; without one, return a gap and no closing. Use only its known heading and length rules; `mode: generic` yields explicitly generic output. A limitations section is not presented as a Winston requirement; include it only if the venue or author requires it.
- Diagnose existing text before editing; preserve meaning, claim strength, numbers, figures, citations, and scope. Present substantive scientific changes separately for author review.
- Record block version and dependent claim IDs; define use / do-not-use / next-skill routing. Enforce G-/C- gates separately from W-05 communication quality.

## Expected files
- `skills/paper-ending/SKILL.md`; optional sibling files for extended material.

## Dependencies
- `docs/principles.md` from `00-prepare-principles.md`.
- `01-mvp-paper-contributions.md` for the block contract; `docs/use-cases.md` and `docs/requirements.md` for gates.

## Acceptance criteria
- [ ] Standard Agent Skills frontmatter and lean, portable instructions exist.
- [ ] No affirmative closing is produced before a complete body supports its contribution claims.
- [ ] A ready brief is required; a known venue heading is respected; generic mode makes no venue-compliance claim.
- [ ] Output does not merely replay section order, strengthen claims, or alter scientific meaning silently.
- [ ] Output records block version and claim IDs; relevant changes trigger review.
- [ ] W-05 traceability, use / do-not-use / next-skill conditions, and no book excerpts or tool/harness code are verified.

## Copyright constraints
Original synthesis only. Never quote, excerpt, commit, or distribute the private PDF or `.txt`.

## Depends on
- #00-prepare-principles
- #01-mvp-paper-contributions
