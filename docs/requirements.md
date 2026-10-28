# Shared Requirements for CS Paper Skills

**Status:** planning draft. `docs/use-cases.md` defines the three writing cases. This document defines the shared evidence gate, inputs, states, and publication checks. Neither document is a skill.

## One claim rule for entry and prose

**A claim may be written as fact only if it has an author-confirmed ID, a resolvable pointer to real supporting material, and wording no broader than that material demonstrates or argues.** To enter the paper-writing flow, at least one *central* claim must pass this same rule. Apply it again to each factual claim in each section.

The author confirms the claim class, support status, and intended scope. The agent may propose them from supplied material, but cannot approve its own inference. A pointer can be a result table and protocol, a proof or theorem number, an artifact path and observation, or a verifiable source identifier. This gate checks traceability and scope; it does not certify that a result or proof is scientifically correct.

If a broad claim fails, narrow it to what the material actually supports and recheck the same rule. For example, a working prototype may support "we implemented this architecture" while leaving "it is faster than prior systems" blocked until a suitable comparison exists. If no central claim passes even after narrowing, `paper-contributions` returns `insufficient-evidence` with the missing material and no paper prose.

## Case-independent inputs

The **research index** identifies the requested task and references the supplied research material, any existing draft, the claim register, the current contribution block, and missing inputs. It does not copy those artifacts. Required fields for each case appear only in `docs/use-cases.md`.

The **venue brief** contains the selected venue's requirements when known:
paper type and track, sections or order if prescribed, abstract format and
length, page or word limits, citation style, and applicable disclosure rules.
It is produced by the intake skill `paper-venue` and always records an
explicit `mode` (`named-venue` or `generic`). `shortlist-requested` is an
intake outcome while the author chooses a candidate, not a ready brief. A brief
with an explicit `mode` is required before `paper-outline`, `paper-opening`,
`paper-ending`, a restructure, a venue adaptation, or submission checks; a
brief with `mode: generic` is valid for generic work, and its output is
labeled generic with unknown constraints left open. Generic mode is never
silent: the author explicitly chooses it via `paper-venue`. A venue-compliance
or adaptation claim requires `mode: named-venue`; a compliance claim also
requires confirmation of every applicable rule being checked. Unconfirmed or
missing venue rules are never invented or treated as passed.

Writing flow order: `paper-contributions` (evidence gate G-) → `paper-venue`
(intake, records `VENUE_BRIEF.md`) → `paper-outline` → `paper-opening` →
`paper-ending`. `paper-venue` is not a prerequisite of `paper-contributions`,
and it is not required for a `local-edit` that does not touch section
structure, sections, abstract, closing, or venue restrictions; such an edit
records `venue_brief_version` if a brief exists, or `venue_brief: none`.

## Claim register and contribution block

Each material claim has a stable ID, proposed wording, author-confirmed class (empirical, theoretical, design, literature-based, or position), support status (`planned`, `partially_supported`, `supported`), a resolvable material pointer or explicit gap, and the scope that material permits. Only a `supported` claim that passes the rule above may be stated as a factual finding. The contribution block is a compact, versioned Vision / Steps / News / Contributions projection referencing claim IDs; it is not a second register.

Each output records the contribution-block version and claim IDs it uses. Change the block version when its meaning changes. If evidence or claim scope changes, review outputs dependent on the affected IDs; if block meaning changes, review outputs tied to its older version. A matching block version alone does not guarantee that the evidence remains current.

## Independent states

| State | Scope | Values |
|---|---|---|
| Structure | Each artifact | `provisional`, `fixed` |
| Claim support | Each claim | `planned`, `partially_supported`, `supported` |
| Submission | Whole paper | `blocked`, `ready` |

A fixed structure can coexist with an unresolved claim, but the paper remains blocked. The submission state never follows automatically from a fixed outline or polished prose.

## Submission-ready gate

Mark a paper `ready` only when all checks pass:

1. Every material claim passes the claim rule above and the author confirms its accuracy; no material claim remains planned or partially supported.
2. The body supports the abstract and ending. Every placeholder, missing figure/table, and unresolved cross-reference has been resolved.
3. Citations and bibliography entries used for factual or related-work claims have been checked against real sources.
4. A publication route is declared and the applicable venue brief, required checklist, and disclosure rules have been checked. A generic draft with no target remains blocked for submission.
5. The author has reviewed the final scientific meaning, scope, numbers, figures, and citations.

`structure: fixed` plus any unresolved material claim can never coexist with `submission: ready`.

## Rule provenance and scoring

| Series | Role | Communication-rubric score? |
|---|---|---|
| `W-` | Winston-derived communication principles in `docs/principles.md`; every skill and rubric criterion needs a genuine W- anchor under `AGENTS.md` rule 6. | Yes, when the criterion measures that principle. |
| `G-` | Research-integrity gates, including the claim rule, no invented results or citations, and preservation of scientific meaning. | Pass/fail outside the rubric; never scored as a G- criterion. |
| `C-` | Current external venue requirements, recorded with source and access date. | Compliance pass/fail; not scored unless a distinct communication criterion has a genuine W- anchor. |

The [NeurIPS paper checklist](https://neurips.cc/public/guides/PaperChecklist) and [CHI 2026 author guide](https://chi2026.acm.org/guide-to-a-successful-submission/) are official examples checked on 2026-10-27. They illustrate venue-specific expectations about claims and supporting material; they are not universal CS-paper rules or Winston principles. Recheck the chosen venue's current requirements before submission. Toulmin, IMRaD, and PRISMA are not universal architecture for this skill set.

## Existing-paper preservation

Before editing an existing draft, diagnose the requested change. Preserve scientific meaning, claim strength, numbers, figures, citations, and scope. Present any substantive scientific change separately for author review. Unsupported passages produce a gap list or visibly marked scaffold, never polished factual prose. Each portable skill that edits text must include these preservation rules in its own `SKILL.md`.

## Source handling

The PDF and `.txt` at the repository root are private reference material and ignored by Git. Use an original synthesis; do not reproduce or publish book text. The project ships no tool or harness code.
