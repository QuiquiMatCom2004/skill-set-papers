# [feat] Create paper-outline skill

## Context
This second MVP skill implements W-01 and W-02. It arranges a supported contribution into a paper route. It can start in `material-no-draft`, revise an incomplete outline in `partial-draft`, or propose a new section map for a `complete-draft` when restructuring or venue adaptation is requested.

## Work
Create `skills/paper-outline/SKILL.md` in standard Agent Skills format. The skill must:

- Require a current versioned contribution block with at least one supported central claim. If absent, route to `paper-contributions`; do not write an outline from idea alone.
- Produce a generic outline when no venue brief is supplied, explicitly declining venue-compliance claims. When a paper-specific venue brief is supplied, apply only its known constraints.
- Record the block version and claim IDs used. Show sections dependent on unresolved claims as visible gaps rather than silently dropping them or claiming results.
- For existing drafts, diagnose first and show an old-to-new section map before prose changes. Preserve scientific meaning, claim strength, numbers, figures, citations, and scope.
- State when to use, when not to use, and where prose drafting goes next. Enforce G- and applicable C- rules as pass/fail while mapping the communication job to W-01/W-02.

## Expected files
- `skills/paper-outline/SKILL.md`; optional sibling files for extended material.

## Dependencies
- `docs/principles.md` from `00-prepare-principles.md`.
- `01-mvp-paper-contributions.md` for the block contract; `docs/use-cases.md` and `docs/requirements.md` for gate and venue brief.

## Acceptance criteria
- [ ] Standard Agent Skills frontmatter and lean, portable instructions exist.
- [ ] No outline is written when the central-claim gate fails; the user receives the material-gap route.
- [ ] With support but no venue brief, output is explicitly generic. With a brief, only supplied rules are applied.
- [ ] Unresolved claims remain visible as gaps; output records block version and dependent claim IDs.
- [ ] An existing-paper restructure starts with a section map and preserves scientific meaning.
- [ ] W-01/W-02 traceability, use / do-not-use / next-skill conditions, and no book excerpts or tool/harness code are verified.

## Copyright constraints
Original synthesis only. Never quote, excerpt, commit, or distribute the private PDF or `.txt`.

## Depends on
- #00-prepare-principles
- #01-mvp-paper-contributions
