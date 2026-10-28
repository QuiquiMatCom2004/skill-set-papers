# [feat] AGENTS.md rule #6: named intake-skill exception for paper-venue

## Context

AGENTS.md rule #6 currently requires every skill and every rubric criterion to map
to at least one Winston-derived W- principle. The project is adding `paper-venue`,
an intake skill whose only job is to record external venue requirements (source,
access date, status). It does not write paper prose, gives no communication
guidance, and contributes no rubric criterion. Rule #6 must be amended to name
this sole exception and to register `paper-venue` in `docs/principles.md`
section C-. No other intake skill may be added without amending this rule first.

Source decision document: `docs/research/venue-brief-decisiones.md`.

## Work

Edit `AGENTS.md` rule #6. Replace the existing rule #6 text exactly with:

"6. **Traceability.** Every skill and every rubric criterion must map to at least
one Winston-derived principle (W-). Sole exception: `paper-venue`, the only
intake skill, maps to the C- venue-requirements category. An intake skill (a)
has the single job of recording external venue requirements and facts with
source, access date and status, (b) writes no paper prose and no communication
guidance, and (c) contributes no rubric criterion or score. Intake skills are
listed in `docs/principles.md` (C- section); adding another requires amending
this rule first. If you cannot name the W- principle, or for a listed intake
skill its C- category, it does not belong in this repo."

Edit `docs/principles.md`. In the section "C- venue requirements" (currently
lines 51-56), add an explicit entry listing `paper-venue` as the intake skill
with its C- anchor. For example:

"- `paper-venue`: intake skill. Single job — records external venue requirements
  and facts with source, access date, and status (`VENUE_BRIEF.md`). Maps to
  C- venue-requirements category (pass/fail compliance, not a rubric score).
  Writes no paper prose, gives no communication guidance, contributes no
  rubric criterion. The only intake skill permitted under `AGENTS.md` rule #6."

Do not change the W- inventory table or any W-ID mapping.

## Expected files

- `AGENTS.md` (rule #6 replaced with approved wording)
- `docs/principles.md` (section C- gains an explicit `paper-venue` entry)

## Dependencies

- None. First issue in the `paper-venue` sequence.

## Acceptance criteria (verifiable by grep/read)

- [ ] `AGENTS.md` rule #6 contains the exact approved wording above, including
      "Sole exception: `paper-venue`, the only intake skill, maps to the C-
      venue-requirements category."
- [ ] `docs/principles.md` section C- contains an explicit entry naming
      `paper-venue` as the intake skill with its C- anchor.
- [ ] No book text quoted or excerpted anywhere (hard rule #1).
- [ ] All edits in English; `PROBLEM.md` untouched.

## Depends on

- None.
