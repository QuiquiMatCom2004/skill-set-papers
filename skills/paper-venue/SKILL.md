---
name: paper-venue
description: Intake skill. Records external venue requirements (source, access date, status) into VENUE_BRIEF.md. The only intake skill under AGENTS.md rule #6; maps to C- venue-requirements (pass/fail, not scored). Writes no paper prose, gives no communication guidance, contributes no rubric criterion.
---

# paper-venue — C- venue-requirements (intake skill)

## Purpose

Records the target venue's external requirements and facts so downstream
writing skills know the style, language, structure, limits, anonymity, and
mandatory disclosures before producing outline, introduction, abstract, or
ending. Its single job is to produce or update `VENUE_BRIEF.md`. It writes no
paper prose, gives no communication guidance, and contributes no rubric
criterion or score.

Maps to **C- venue-requirements** (external compliance facts, pass/fail,
outside the Winston W- principles and outside the communication rubric).
Not a Winston principle: venue rules are current external requirements recorded
with source and access date; `paper-venue` never invents them and never marks
them "verified by agent".

## When to use this skill

Use at the start of the paper-writing flow, after `paper-contributions`
passes the evidence gate and before `paper-outline`, `paper-opening`, or
`paper-ending` produce venue-aware output. `paper-venue` is NOT a prerequisite
of `paper-contributions`.

Permitted entry cases:
- The author names a venue (journal, conference, transaction, workshop).
- The author explicitly chooses generic work while no venue is selected;
  never invent restrictions.
- The author asks for candidate venues: only on explicit request; the author
  always makes the final choice.

Do not use this skill to draft paper text, propose an opening angle, or advise
on how to present results. Those jobs belong to `paper-outline`,
`paper-opening`, and `paper-ending`.

## Inputs (referenced, not copied)

- **Author-supplied venue guide** (preferred): link, PDF, or text the author
  provides for the named venue.
- **Official venue guide** (only if the harness offers standard web access and
  the author named the venue): the venue's own author instructions / call for
  papers / aims & scope. Every field read this way is recorded as
  `agent-read-unconfirmed` with source and access date.
- **Existing `VENUE_BRIEF.md`** (for updates): current brief version and
  field states.

## Intake choice and brief mode

- `named-venue`: the author named a venue. Fields are filled from the
  author-supplied guide first, then the official venue guide if web access is
  available. Missing fields stay `UNKNOWN`, never invented.
- `generic`: no venue chosen yet. Constraints are left open; output of
  downstream skills is explicitly labeled generic. No venue-compliance claim
  is ever made.
- `shortlist-requested`: the author asked for candidate venues. This is an
  intake outcome, not a ready brief mode. Return only a shortlist (names and
  public pointers); the author chooses. While the choice is pending, no venue
  restrictions apply and no downstream writing skill runs. Create a brief only
  after the author names a venue or explicitly chooses generic work.

Never detect "no venue yet" from free text. Ask the mode question with the
three closed choices below. Ask for the paper language only after a ready
mode is chosen.

## Steps

1. If `VENUE_BRIEF.md` exists, read its mode, language, field states, and
   version. Ask the same three-choice mode question as step 2, showing the
   current choice and venue name so the author can retain or change them.
   Never infer the answer from free text. If the author requests a shortlist,
   archive the old brief as `VENUE_BRIEF.archive-v<version>.md` so it is no
   longer current; return candidates and stop. Otherwise recheck changed
   fields against supplied sources, retain unchanged fields and provenance,
   and continue at step 3 if language is missing or changed, otherwise step 4.
   Changing the named venue or switching to generic clears old venue-specific
   fields to `UNKNOWN` until they are sourced again.
2. Otherwise ask the mode question, offering exactly three answers: "Where
   will this paper be submitted? (a) a named venue — give its name; (b) no
   venue yet — work generic; (c) suggest candidate venues — I will choose." Record the
   answer literally as the intake choice `named-venue`, `generic`, or
   `shortlist-requested`; never infer one from free text.
3. If the intake choice is `shortlist-requested`, return candidates with
   public pointers only. Do not save a ready brief or proceed to downstream
   writing. When the author later names a venue or explicitly chooses generic
   work, restart at step 2 with that choice. For a ready mode, ask: "In which
   language will the paper be written, and does the venue require an abstract
   in a second language?" Record `language` and any
   `secondary_abstract_language`; retain recorded values on an unchanged
   existing brief.
4. For `named-venue`, ask the author for the venue's author guide (link, PDF,
   or pasted text). Fill fields from it as `author-supplied`. Only if the
   harness already offers standard web access, read the official guide of the
   named venue and record those fields as `agent-read-unconfirmed`. Leave
   everything else `UNKNOWN`. For `generic`, keep venue-specific fields
   `UNKNOWN` and make no venue-compliance claim.
5. On any field change, increment `brief_version`.
6. Show the brief to the author, list every `UNKNOWN` and every
   `agent-read-unconfirmed` field, and ask the author to confirm or correct
   them. Confirmed fields become `author-supplied`.
7. Save `VENUE_BRIEF.md` next to the claim register and contribution block of
   the same paper.

**Next skill:** `paper-outline`.

## Output: VENUE_BRIEF.md (create or update)

Every field carries: source, access date, and state
(`author-supplied` / `agent-read-unconfirmed` / `UNKNOWN`). Never invented;
never "verified by agent".

Required header fields:
- `brief_version`: integer. Starts at 1. Increments on ANY field change.
- `language`: paper language declared for the venue (e.g. English, Spanish).
- `secondary_abstract_language`: optional; only when the venue requires an
  abstract in a second language (e.g. Spanish + English abstract).
- `mode`: one of `named-venue` / `generic`; a pending shortlist is an intake
  outcome, not a ready brief.
- `readership`: the readership the venue itself declares (aims & scope / call
  for papers), with source, access date, state or UNKNOWN. External fact, not
  writing guidance. Vocabulary/detail adjustment stays in `paper-opening` /
  `paper-outline`, not scored, no rubric criterion.

Venue-requirement fields (fill only what is known; leave the rest UNKNOWN):
- Venue name, type (journal / conference / transaction / workshop), publisher.
- Paper type / track / subcommittee, if the venue prescribes one.
- Mandatory sections and their order, if the venue prescribes them.
- Abstract format and length; keywords / classification (e.g. ACM CCS).
- Page or word limit; template (IEEE, ACM, LNCS, Elsevier, …).
- Citation and bibliography style.
- Anonymity (double-blind / single-blind / none).
- Mandatory disclosures (data/code, ethics/IRB, AI/LLM use, conflicts,
  reproducibility checklist).
- Figure/table requirements and supplementary material rules.
- How results must be presented (required limitations section, claims vs.
  results form, …).

## Re-verification (for downstream skills, referenced here for completeness)

If a downstream skill's recorded `venue_brief_version` is lower than the
current `VENUE_BRIEF.md` version, it lists changed fields, marks affected
output elements, does not rewrite until the author confirms, then records the
new version. If no changed field affects its output, it records the new
version and says so.

## What this skill does not do

- Does not write tool or harness code; no implementation is shipped.
- Does not write paper prose, introduction, abstract, outline, or ending.
- Does not give communication guidance or vocabulary advice.
- Does not contribute a rubric criterion or score.
- Does not quote, excerpt, or reproduce the private book.
- Does not detect "no venue yet" from free text; the mode question uses the
  three explicit choices.
- Does not choose a venue or rank candidates; the author always chooses.
- Never invents venue rules; never marks a field "verified by agent".

## Traceability

- C- venue-requirements: external venue facts recorded with source, access
  date, state; pass/fail compliance, not a rubric score.
- AGENTS.md rule #6: sole intake-skill exception to the W- traceability rule.
