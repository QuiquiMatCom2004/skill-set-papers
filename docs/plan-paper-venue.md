# Plan: paper-venue skill (MVP addition)

## Problem summary (from user)

The four original writing skills (`paper-contributions`, `paper-outline`, `paper-opening`,
`paper-ending`) lack an initial intake phase that records where the paper is
going to be published (venue, style, language, limits, anonymity, mandatory
disclosures). As a result the agent does not know how to present results or
which structure to follow, and output is silently labeled `generic`. The user
wants the agent to know the target venue's style and structure before writing
outline, opening, or ending. Decision: modify AGENTS.md rule #6 and create the
skill `paper-venue`.

## Approved decisions

1. Rule #6 rewritten verbatim (exception named to `paper-venue`, intake-skill
   definition, registration in `docs/principles.md` section C-, prohibition of
   adding another intake skill without amending the rule first).
2. New skill `skills/paper-venue/SKILL.md` with explicit C- anchor, single job
   (produce/update `VENUE_BRIEF.md`), closed mode literal
   `named-venue` / `generic` ready-brief modes plus a pending
   `shortlist-requested` intake outcome, integer `brief_version`,
   `language` + optional `secondary_abstract_language`, `readership` as external
   venue-declared fact with source/access date/state or UNKNOWN, per-field
   source/access date/state (`author-supplied` / `agent-read-unconfirmed` /
   `UNKNOWN`), never invented, never "verified by agent", web only if the
   harness offers it and the author named the venue, a closed mode question, no
   natural-language detection of "no venue yet", candidate list only on author
   request, choice always by author, shortlist pending until chosen.
3. New `skills/paper-venue/VENUE_BRIEF_TEMPLATE.md` with venue identity,
   language, readership, structure, limits, anonymity, and disclosure fields.
4. Four existing `SKILL.md` updated: `paper-contributions` next skill →
   `paper-venue`; `paper-outline`, `paper-opening`, `paper-ending` declare the
   brief as input with explicit `mode`, record `venue_brief_version` and
   `language`, apply version re-verification, return a gap pointing to
   `paper-venue` if the brief is missing or its `mode` absent. None duplicates
   the mode/language question.
5. `docs/requirements.md:17` and `docs/use-cases.md:21` updated: non-silent
   generic mode (explicit author choice), flow evidence gate → `paper-venue` →
   `paper-outline` → `paper-opening` → `paper-ending`, `paper-venue` not
   required for `local-edit` that does not touch sections/structure, abstract,
   closing, or venue restrictions.
6. `docs/principles.md` section C- updated: lists `paper-venue` as intake skill
   with its C- anchor.
7. `docs/skill-proposal.md` and `README.md` updated to the new flow and new
   skill.
8. Partial value declared: v0.1 conditions outline/sections/abstract/closing;
   no body-text skill; W-06 not executable in v0.1.

## Architecture (flow and dependencies)

```
paper-contributions (gate G-) → paper-venue → paper-outline → paper-opening → paper-ending
```

- `paper-contributions` emits a versioned contribution block (G- gate) and runs
  first; `paper-venue` runs after the gate passes. `paper-venue` is NOT a
  prerequisite of `paper-contributions`.
- `paper-venue` intake: records external venue requirements in
  `VENUE_BRIEF.md`, one job only, no paper prose, no communication guidance,
  no rubric criterion. Ready modes: `named-venue` / `generic`.
  `shortlist-requested` stays pending until the author chooses a route.
- `paper-outline`, `paper-opening`, `paper-ending` require the brief with an
  explicit `mode`; record `venue_brief_version` and `language`; re-verify by
  version; gap-remit to `paper-venue` if missing.
- `local-edit` that does not touch structure/sections/abstract/closing/venue
  restrictions does not require the brief; records `venue_brief_version` or
  `venue_brief: none`.

## Ordered issue list

| # | Slug | Job | Depends on |
|---|------|-----|------------|
| 1 | 02-agents-rule-six-intake-skill | AGENTS.md rule #6 + register `paper-venue` in `docs/principles.md` section C- | — |
| 2 | 02-paper-venue-skill | `skills/paper-venue/SKILL.md` + `skills/paper-venue/VENUE_BRIEF_TEMPLATE.md` | #1 |
| 3 | 02-update-existing-skills | Update four existing `SKILL.md` + their brief contracts | #2 |
| 4 | 02-update-docs | `docs/requirements.md:17`, `docs/use-cases.md:21`, `docs/skill-proposal.md`, `README.md`, `docs/evaluation.md` ("four skills" mentions) | #3 |

## Acceptance criteria (repo-level)

- `grep -c 'named-venue' skills/paper-venue/SKILL.md` ≥ 1
- `grep -c 'generic' skills/paper-venue/SKILL.md` ≥ 1
- `grep -c 'shortlist-requested' skills/paper-venue/SKILL.md` ≥ 1
- `grep -c 'brief_version' skills/paper-venue/SKILL.md` ≥ 1
- Each field in the brief template carries source, access date, and state
  (`author-supplied` / `agent-read-unconfirmed` / `UNKNOWN`).
- No quote/excerpt from the Winston book files anywhere (hard rule #1).
- All deliverables in English (hard rule #2); `PROBLEM.md` stays Spanish.
- AGENTS.md rule #6 text matches the approved wording exactly.
- Rubric `rubric/v0.md` intact; C- stays pass/fail outside the rubric.
