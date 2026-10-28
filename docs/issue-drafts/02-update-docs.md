# [feat] Update docs for the paper-venue flow (requirements, use-cases, proposal, README, evaluation)

## Context

The approved flow is `paper-contributions` (gate G-) → `paper-venue` →
`paper-outline` → `paper-opening` → `paper-ending`. Several project docs still
describe the old four-skill flow or a silent `generic` mode. They must be
updated to: non-silent generic mode (explicit author choice), the new order,
`paper-venue` not required for minor `local-edit`, the intake skill in the
principles/proposal/README, and the evaluation doc's "four skills" mentions.

Decision document: `docs/research/venue-brief-decisiones.md`.

## Work

### 1) `docs/requirements.md:17`

Update the venue-brief paragraph (currently lines 17-18):

"The **venue brief** contains the selected venue's requirements when known:
paper type and track, sections or order if prescribed, abstract format and
length, page or word limits, citation style, and applicable disclosure rules.
It is produced by the intake skill `paper-venue` and always records an
explicit `mode` (`named-venue` or `generic`). `shortlist-requested` is pending
intake, not a ready brief. A brief with an explicit `mode` is required before
`paper-outline`, `paper-opening`,
`paper-ending`, a restructure, a venue adaptation, or submission checks; a
brief with `mode: generic` is valid for generic work, and its output is
labeled generic with unknown constraints left open. Generic mode is never
silent: the author explicitly chooses it via `paper-venue`. A venue-compliance
or adaptation claim requires `mode: named-venue`. Missing venue rules are
never invented. A compliance claim also requires author confirmation of every
applicable rule being checked."

Add flow order somewhere in the document (after the venue-brief paragraph or
in the shared-inputs section):

"Writing flow order: `paper-contributions` (evidence gate G-) → `paper-venue`
(intake, records `VENUE_BRIEF.md`) → `paper-outline` → `paper-opening` →
`paper-ending`. `paper-venue` is not a prerequisite of `paper-contributions`,
and it is not required for a `local-edit` that does not touch section
structure, sections, abstract, closing, or venue restrictions; such an edit
records `venue_brief_version` if a brief exists, or `venue_brief: none`."

### 2) `docs/use-cases.md:21`

Update the paragraph at line 21 ("A venue brief is a separate dimension…"):

"A venue brief is a separate dimension for all cases. It is produced by the
intake skill `paper-venue` after the evidence gate and always records an
explicit `mode`. Outline, opening, and ending work requires a brief, which may
be `mode: generic`; a local edit that does not touch structure, abstract,
closing, or venue restrictions does not. Venue adaptation or a
submission-ready claim requires `mode: named-venue`. Generic mode is never
silent: the author explicitly chooses it via `paper-venue`. Missing venue
rules are left unknown, never invented."

Also update the routing table example 8 and example 7 if they reference the
brief as optional without naming `paper-venue`; add that `paper-venue` produces
the brief before any `venue-adapt` compliance claim.

### 3) `docs/skill-proposal.md`

- In the MVP v0.1 table, add a row for `paper-venue`:

  "| `paper-venue` | Intake: records external venue requirements (source, access date, status)
    into VENUE_BRIEF.md; the only intake skill under AGENTS.md rule #6. |
    VENUE_BRIEF.md with brief_version, language, mode, readership, and
    per-field source/access date/state. | C- (venue requirements; pass/fail,
    not scored) |"

- Update the flow sentence: "The five MVP skills run in the order
  `paper-contributions` → `paper-venue` → `paper-outline` → `paper-opening` →
  `paper-ending`; `paper-venue` is not a prerequisite of
  `paper-contributions`."

- Add to "Later releases" or a note: v0.1 conditions outline/sections/
  abstract/closing via the venue brief; no body-text skill; W-06 not
  executable in v0.1.

### 4) `README.md`

- Update "Deliverables → Skill set" to mention five skills including
  `paper-venue` as the intake skill.
- Update "Repository layout" / "Status" to reflect five MVP skills and the
  intake-skill exception in AGENTS.md rule #6.
- Keep all text in English.

### 5) `docs/evaluation.md`

Review all mentions of "four skills" / "four MVP skills" and update to reflect
that `paper-venue` runs before and outside the comparison (per the decision:
"paper-venue se ejecuta antes y fuera de la comparación"). Specifically:

- Section 1 Purpose: "the project's four skills enabled" → "the project's
  four writing skills enabled (`paper-outline`, `paper-opening`,
  `paper-ending`, plus `paper-contributions`); `paper-venue` runs before and
  outside the comparison."
- Section 2: "The four skills compared are `paper-contributions`,
  `paper-outline`, `paper-opening`, and `paper-ending` (treatment)." Add:
  "`paper-venue` is executed before the comparison and is outside it; the same
  brief is used for both arms."
- Section 2 item 4: the same ready brief from `paper-venue` is required and
  identical in both arms, except for an eligible narrow `local-edit` that may
  record `venue_brief: none` in both arms.
- Section 6 item 6: freeze the ready brief with source and access date;
  `mode: generic` is an explicit author choice and claims no venue compliance.
- Section 10.4: report C- venue results per arm; `paper-venue` outside the
  comparison.
- Section 13 blocker 2: "The four skills are implementation drafts" → five
  skills including `paper-venue`; `paper-venue` must be reviewed and versioned
  too.

## Expected files

- `docs/requirements.md` (edited, line ~17 plus flow-order note)
- `docs/use-cases.md` (edited, line ~21 plus routing-table notes)
- `docs/skill-proposal.md` (edited)
- `README.md` (edited)
- `docs/evaluation.md` (edited)

## Dependencies

- `skills/paper-venue/SKILL.md` from issue `02-paper-venue-skill.md`.
- Four existing `SKILL.md` updates from issue `02-update-existing-skills.md`.
- `AGENTS.md` rule #6 and `docs/principles.md` section C- from issue
  `02-agents-rule-six-intake-skill.md`.

## Acceptance criteria (verifiable by grep/read)

- [ ] `docs/requirements.md` states the flow order
      `paper-contributions` → `paper-venue` → `paper-outline` →
      `paper-opening` → `paper-ending`.
- [ ] `docs/requirements.md` states generic mode is never silent (explicit
      author choice via `paper-venue`) and that `paper-venue` is not required
      for `local-edit` that does not touch structure/sections/abstract/
      closing/venue restrictions.
- [ ] `docs/use-cases.md` names `paper-venue` as the brief producer and
      repeats non-silent generic mode.
- [ ] `docs/skill-proposal.md` MVP table includes a `paper-venue` row with
      C- anchor; flow order updated; v0.1 partial value declared (outline/
      sections/abstract/closing conditioned; no body-text skill; W-06 not
      executable in v0.1).
- [ ] `README.md` mentions five skills including `paper-venue` as intake
      skill; status reflects the new flow.
- [ ] `docs/evaluation.md`: "four skills" mentions updated; `paper-venue`
      runs before and outside the comparison; same brief for both arms.
- [ ] `rubric/v0.md` untouched (C- stays pass/fail outside the rubric).
- [ ] No book text quoted or excerpted anywhere (hard rule #1).
- [ ] All edits in English; `PROBLEM.md` untouched.

## Depends on

- #02-update-existing-skills
- #02-paper-venue-skill
- #02-agents-rule-six-intake-skill
