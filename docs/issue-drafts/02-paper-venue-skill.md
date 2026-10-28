# [feat] Create paper-venue intake skill and brief template

## Context

The four writing skills need an explicit publication route before they make
an outline, opening, or ending. `paper-venue` records external requirements in
`VENUE_BRIEF.md`. It is the sole intake exception under AGENTS.md rule 6:
its anchor is C- venue requirements, outside the W- communication rubric.
The approved decisions are in `docs/research/venue-brief-decisiones.md`; the
field inventory is in `docs/research/venue-brief-investigacion.md`.

## Work

Create `skills/paper-venue/SKILL.md` with standard Agent Skills frontmatter
(`name: paper-venue`, description) and a lean, harness-independent body.
Create `skills/paper-venue/VENUE_BRIEF_TEMPLATE.md` as a sibling reference.

The skill has one job: produce or update the brief. It writes no paper prose,
gives no communication advice, and contributes no rubric score. It runs after
`paper-contributions` passes the evidence gate and before the writing skills.

Ask the author to choose explicitly among three intake responses:

1. `named-venue`: the author names a journal, conference, or other CS venue.
2. `generic`: the author explicitly chooses to work without a venue.
3. `shortlist-requested`: the author asks for candidate venues and makes the
   final choice. This is pending intake, not a ready brief; return names and
   public pointers only. No downstream writing skill runs until the author
   names a venue or explicitly chooses generic work.

Do not infer a mode from free text. For a ready mode, ask for the paper language
and whether a second abstract language is required. The author supplies the
guide when possible. If standard web access is available and the author named
a venue, the agent may read its official guide. Fields read by the agent stay
`agent-read-unconfirmed` until the author confirms them. Never invent a venue
rule or label a field "verified by agent".

The ready brief uses `mode: named-venue` or `mode: generic`, an integer
`brief_version` starting at 1, `language`, optional
`secondary_abstract_language`, and the venue-declared `readership` or
`UNKNOWN`. It records venue identity, paper type/track, mandatory sections,
abstract format/length, keywords/classification, page/word limit, template,
citation style, anonymity, disclosures, figure/table rules, supplementary
material rules, and result-presentation rules. Every venue fact records value,
source, access date, and state (`author-supplied`,
`agent-read-unconfirmed`, or `UNKNOWN`). Missing fields remain `UNKNOWN`.

When updating an existing brief, retain unchanged provenance and increment
`brief_version` for any field change. A switch to generic clears venue-specific
facts. A switch to shortlist archives the old brief so it is no longer
current. Show unknown and unconfirmed fields to the author for review. Save
the ready brief next to the claim register and contribution block for that
paper. The next skill is `paper-outline`.

## Acceptance criteria

- [ ] Both files exist; `SKILL.md` has valid frontmatter and a C- anchor.
- [ ] The three intake choices and two ready-brief modes have the meanings
      above; a pending shortlist cannot unlock downstream writing.
- [ ] The language question occurs only for a ready mode and is not repeated
      by the writing skills.
- [ ] The brief template has every field above with source, access date, and
      state; missing facts remain `UNKNOWN`.
- [ ] Existing-brief changes preserve provenance, version correctly, and
      retire a brief when selection becomes pending.
- [ ] No paper prose, communication advice, rubric criterion, tool code, or
      private-book text is added.

## Dependencies

- `02-agents-rule-six-intake-skill.md`
- `docs/requirements.md` and `docs/use-cases.md` for evidence and writing
  gates.
