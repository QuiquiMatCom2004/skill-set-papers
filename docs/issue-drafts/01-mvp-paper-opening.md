# [feat] Create paper-opening skill

## Context
This third MVP skill implements W-03 and W-04 in two phases: introduction after an outline, final abstract after a complete supported body. It may write or revise the relevant opening in any of the three writing cases after the central-claim gate passes.

## Work
Create `skills/paper-opening/SKILL.md` in standard Agent Skills format. The skill must:

- Require the current contribution block and an outline or existing-paper section map. If the block is absent, route to `paper-contributions`; an idea alone never produces an introduction.
- Apply the single factual-claim rule to every result, method, background, or contribution statement: author-confirmed ID, resolvable support pointer, and wording no broader than the material supports. A failed claim becomes a visible gap or is omitted, not polished into a finding.
- Draft the final abstract only from a complete body supporting the contribution. A planning note is not presented as a paper abstract.
- Require a ready brief from `paper-venue`; without one, return a gap and no introduction or abstract. Apply known format and length rules only from that brief. `mode: generic` yields explicitly generic output. For edits, diagnose first and preserve meaning, claim strength, numbers, figures, citations, and scope.
- Record block version and dependent claim IDs; define use / do-not-use / next-skill routing. Enforce G-/C- gates separately from W-03/W-04 communication quality.

## Expected files
- `skills/paper-opening/SKILL.md`; optional sibling files for extended material.

## Dependencies
- `docs/principles.md` from `00-prepare-principles.md` (verify W-04 against organization and abstract chapters).
- `01-mvp-paper-contributions.md` and `01-mvp-paper-outline.md` for block and outline contracts; `docs/use-cases.md` and `docs/requirements.md` for gates.

## Acceptance criteria
- [ ] Standard Agent Skills frontmatter and lean, portable instructions exist.
- [ ] Idea-only input returns the material-gap route; no provisional paper introduction is produced.
- [ ] Every factual statement is linked to a passing claim; unsupported result claims become gaps rather than achieved findings.
- [ ] Final abstract requires a complete supported body, not just an outline.
- [ ] Output records block version and claim IDs; existing-text edits preserve scientific content.
- [ ] W-03/W-04 traceability, use / do-not-use / next-skill conditions, and no book excerpts or tool/harness code are verified.

## Copyright constraints
Original synthesis only. Never quote, excerpt, commit, or distribute the private PDF or `.txt`.

## Depends on
- #00-prepare-principles
- #01-mvp-paper-contributions
- #01-mvp-paper-outline
