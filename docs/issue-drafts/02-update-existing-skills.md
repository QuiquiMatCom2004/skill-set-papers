# [feat] Update four existing SKILL.md for the paper-venue flow

## Context

The approved flow is `paper-contributions` (gate G-) → `paper-venue` →
`paper-outline` → `paper-opening` → `paper-ending`. The four existing
`SKILL.md` files currently cite `paper-outline` as "next skill" and treat the
venue brief as optional. They must be updated so routing is not broken and each
downstream skill declares the brief as required input with explicit `mode`,
records `venue_brief_version` and `language`, applies version re-verification,
and returns a gap remitting to `paper-venue` when the brief is missing or its
`mode` is absent. None duplicates the mode/language question.

Approved plan: `docs/plan-paper-venue.md` (decisions 4 and 8: `paper-venue` is not required for `local-edit` that
does not touch sections/structure/abstract/closing/venue restrictions; that
output records `venue_brief_version` or `venue_brief: none`; v0.1 conditions
outline/sections/abstract/closing, no body-text skill).

## Work

### 1) `skills/paper-contributions/SKILL.md`

- Change "**Next skill:** `paper-outline`" to "**Next skill:** `paper-venue`"
  (intake: records venue requirements before outline/opening/ending).
- Remove the optional venue-brief input: `paper-contributions` runs before
  `paper-venue` and neither consumes the brief nor labels its block generic.
- Add to "What this skill does not do": does not require or consume a venue
  brief; `paper-venue` is not a prerequisite of this skill.

### 2) `skills/paper-outline/SKILL.md`

- In "When to use this skill": add that a current venue brief from
  `paper-venue` with explicit `mode` is required input before producing ANY
  outline (a brief with `mode: generic` is valid and yields a generic
  outline); without it, return a gap remitting to `paper-venue` (do not write
  an outline and do not ask the mode/language question).
- In "Inputs": mark "Venue brief" as required (from `paper-venue`), not
  optional; add fields `venue_brief_version` (integer) and `language` as
  recorded dependencies.
- Add an entry-gate step: verify a ready brief with `mode: named-venue` or
  `mode: generic`; if missing or shortlist selection is pending, return a gap
  pointing to `paper-venue` and stop.
- Add re-verification: if the outline's recorded `venue_brief_version` is lower
  than the current brief version, list changed fields, mark affected outline
  elements, do not rewrite until the author confirms, then record the new
  version; if nothing changed affects the outline, record the new version and
  say so.
- Output "Recorded dependencies": add `venue_brief_version` and `language`
  alongside the contribution-block version and claim IDs.
- In "Venue handling": a missing ready brief blocks the outline; `mode:
  generic` yields explicitly generic output. Venue adaptation and compliance
  claims require `mode: named-venue`; unknown rules stay unknown.
- Update "Next skill" at the end: `paper-opening` (drafts introduction from
  the outline).

### 3) `skills/paper-opening/SKILL.md`

- In "When to use this skill": add that a current venue brief from `paper-venue`
  with explicit `mode` is required (a brief with `mode: generic` is valid);
  without it return a gap remitting to `paper-venue` and emit no introduction
  or abstract. Write the introduction and abstract in the brief's `language`;
  if `secondary_abstract_language` is set, also produce the abstract in that
  language.
- In "Inputs": mark "Venue brief" as required; add `venue_brief_version` and
  `language` to recorded dependencies for both introduction and abstract
  outputs.
- Add entry-gate step: verify a ready brief with `mode: named-venue` or
  `mode: generic`; if missing or selection pending, return a gap to
  `paper-venue` and stop.
- Add re-verification for introduction/abstract: version check as in
  `paper-outline`; changed fields affecting introduction/abstract are marked;
  no rewrite until author confirms; record new version or notify if unaffected.
- Output headings: add `venue_brief_version` and `language` to "Recorded
  dependencies" for introduction and for final abstract.
- "Next skill": `paper-ending` (unchanged job).
- Do not duplicate the mode/language question; `paper-venue` owns it.

### 4) `skills/paper-ending/SKILL.md`

- In "Required inputs": add venue brief from `paper-venue` with explicit
  `mode` as required; add `venue_brief_version` and `language`.
- Add entry-gate step: verify a ready brief with `mode: named-venue` or
  `mode: generic`; if missing or selection pending, return a gap to
  `paper-venue` and emit no closing prose.
- Add re-verification for the closing: same version-check pattern.
- "Record": add `venue_brief_version` and `language` to the recorded
  contribution-block version and claim IDs.
- Heading/length: apply known rules from the required brief. `mode: generic`
  yields explicitly generic output with no venue-compliance claim.
- "Next skill": none within v0.1 (unchanged); submission-ready gate after
  closing (unchanged).

### Language (applies to outline, opening and ending)

Each of the three skills writes its paper-facing text (section titles,
introduction, abstract, closing) in the brief's `language` and records that
`language` in its output. The SKILL.md files themselves stay in English
(AGENTS.md rule #2).

### 5) `local-edit` carve-out (applies to `paper-outline` local-edit and any
   existing-paper edit path)

A `local-edit` that does not touch section structure, abstract, closing, or
venue restrictions does not require the brief; its output records
`venue_brief_version` if a brief exists, or `venue_brief: none` if none.

## Expected files

- `skills/paper-contributions/SKILL.md` (edited)
- `skills/paper-outline/SKILL.md` (edited)
- `skills/paper-opening/SKILL.md` (edited)
- `skills/paper-ending/SKILL.md` (edited)

## Dependencies

- `skills/paper-venue/SKILL.md` from issue `02-paper-venue-skill.md`.
- `AGENTS.md` rule #6 and `docs/principles.md` section C- from issue
  `02-agents-rule-six-intake-skill.md`.

## Acceptance criteria (verifiable by grep/read)

- [ ] `skills/paper-contributions/SKILL.md`: "Next skill" is `paper-venue`;
      states `paper-venue` is not a prerequisite of this skill.
- [ ] `skills/paper-outline/SKILL.md`: venue brief marked required input with
      explicit `mode`; records `venue_brief_version` and `language`; entry gate
      returns gap to `paper-venue` when brief/mode missing; re-verification by
      version present; `paper-opening` as next skill.
- [ ] `skills/paper-opening/SKILL.md`: venue brief required input with
      explicit `mode`; records `venue_brief_version` and `language` for
      introduction and abstract; entry gate returns gap to `paper-venue`;
      re-verification present; `paper-ending` as next skill.
- [ ] `skills/paper-ending/SKILL.md`: venue brief required input with
      explicit `mode`; records `venue_brief_version` and `language`;
      entry gate returns gap to `paper-venue`; re-verification present.
- [ ] None of the four duplicates the mode/language question (that is owned by
      `paper-venue`).
- [ ] `local-edit` carve-out present: no brief required when it does not touch
      structure/sections/abstract/closing/venue restrictions; records
      `venue_brief_version` or `venue_brief: none`.
- [ ] No book text quoted or excerpted anywhere (hard rule #1).
- [ ] All edits in English; `PROBLEM.md` untouched.

## Depends on

- #02-paper-venue-skill
- #02-agents-rule-six-intake-skill
