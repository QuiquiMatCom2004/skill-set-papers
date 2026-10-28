---
name: paper-outline
description: Arranges a supported CS-paper contribution into a reasoned section route from a current versioned contribution block, showing unresolved claims as gaps; emits generic or venue-aware outlines without inventing venue rules. Maps to Winston principles W-01 and W-02.
---

# paper-outline — W-01, W-02

## Purpose

Takes the current versioned contribution block produced by `paper-contributions` and arranges the supported contribution into a reasoned route through the paper's major sections, ordered to lead the reader to the contribution rather than follow the history of the work. Shows sections that depend on unresolved claims as visible gaps instead of silently dropping them or asserting results.

Maps to:

- **W-01**: make the desired outcome, route, new finding, and contribution explicit so the reader knows what was done and why it matters (docs/principles.md).
- **W-02**: give major sections a reasoned route through the paper, ordered to lead the reader to the contribution (docs/principles.md).

## When to use this skill

Use when:

- A current, versioned contribution block exists (emitted by `paper-contributions`) and it references supported claim IDs.
- At least one central claim passes the one-claim gate: author-confirmed claim ID, resolvable pointer to real supporting material, wording no broader than that material demonstrates or argues.
- The request is to outline a paper, restructure an existing draft's sections, or adapt sections to a supplied venue brief.
- A current venue brief from `paper-venue` with `mode: named-venue` or `mode: generic` is required before producing any outline or restructuring sections. The narrow `local-edit` diagnosis described below is the only exception. Without a ready brief, return a gap to `paper-venue`; do not ask the mode/language question.

Permitted entry cases (docs/use-cases.md), each only after the claim gate passes:

- `material-no-draft` — material exists, no paper prose yet
- `partial-draft` — an incomplete draft exists, central claim supported
- `complete-draft` — a full draft exists, central claim supported

## When not to use this skill (routing)

Do not use when:

- No current contribution block exists, or no central claim passes the gate → route to `paper-contributions`; do not write an outline from an idea alone.
- The central-claim gate fails → return the `insufficient-evidence` route (material-gap list: proposed claim, missing material, any narrower supported claim); emit no outline, no introduction, no polished prose.
- The request is to invent results, proofs, or citations → return a gap list or visibly marked scaffold, no factual prose.
- The paper is outside Computer Science → out of scope.

## Inputs

- **Research index**: identifies the task and references the supplied material, any existing draft, the claim register, the current contribution block, and missing inputs. It does not copy those artifacts.
- **Current versioned contribution block**: Vision / Steps / News / Contributions referencing supported claim IDs, plus the block version.
- **Venue brief** (required for an outline or restructure, from `paper-venue`): the selected venue's requirements when known (paper type/track, prescribed sections or order, abstract format and length, page or word limits, citation style, applicable disclosure rules), with `mode: named-venue` or `mode: generic`. Record `venue_brief_version` (integer) and `language` as dependencies. Without a ready brief, return a gap to `paper-venue`; do not write an outline. Write section titles and outline text in the brief's `language`.
- **Existing draft** (for restructure / venue-adapt): current draft plus the requested change.

## Entry gate (claim gate G-)

Apply before any outline section is produced:

0. For outline, restructure, or venue adaptation, verify a current venue brief from `paper-venue` exists with `mode: named-venue` or `mode: generic`. A missing brief or pending shortlist returns a gap to `paper-venue`; produce no outline and do not ask the mode/language question. A narrow `local-edit` section-route diagnosis may proceed without the brief if it does not touch structure, abstract, closing, or venue restrictions; record `venue_brief: none` in that case.

1. Verify the contribution block is current, versioned, and references claim IDs.
2. Confirm at least one central claim is `supported` and passes the one-claim rule (author-confirmed ID; resolvable pointer to real supporting material; wording no broader than the material demonstrates or argues).
3. If the block is absent, missing claim IDs, or no central claim passes even after narrowing → route to `paper-contributions`, emit `insufficient-evidence` with the material-gap list, and do not write an outline.
4. Narrow overbroad claims to what the material actually supports, then recheck the same rule. The agent proposes claim IDs, wording, and scope; the author confirms. The agent never approves its own inference and does not certify scientific correctness.

### Venue brief re-verification

If the outline's recorded `venue_brief_version` is lower than the current `VENUE_BRIEF.md` version, list the changed fields, mark the affected outline elements, do not rewrite until the author confirms, then record the new version. If no changed field affects the outline, record the new version and say so.

## Output

Produce one outline containing:

1. **Recorded dependencies**: the contribution-block version used, `venue_brief_version` (integer), `language`, and every dependent claim ID used by each section. Change tracking: if evidence or claim scope changes, review outputs dependent on the affected claim IDs; if block meaning changes, review outputs tied to the older block version.
2. **Reasoned section route (W-02)**: order major sections so each follows from the last toward the contribution, not the project's history. State the contribution, outcome, and new finding explicitly (W-01).
3. **Visible gaps**: any section whose claims are not `supported` is shown as an unresolved-claim gap. Never silently omit such a section, never assert its result, and never invent results, proofs, or citations.
4. **Venue handling**:
   - `mode: generic` (explicit author choice via `paper-venue`, never a silent default): output is explicitly generic; decline any venue-compliance claim; leave unknown venue constraints open.
   - No ready venue brief: only the `local-edit` diagnosis may proceed without one; otherwise return a gap to `paper-venue`. Missing venue rules stay unknown, never invented.
   - `mode: named-venue`: apply only the rules explicitly recorded in the brief. Venue adaptation and any venue-compliance claim require this mode. Claim compliance only for applicable rules confirmed by the author; do not infer additional rules or claim full compliance from an incomplete brief.

## Existing drafts (partial-draft / complete-draft)

Before any prose change:

1. **Diagnose first**: diagnose the requested change against the current block and claim IDs.
2. **Old-to-new section map**: produce a map showing how each existing section maps to the new route, before making prose changes.
3. **Preservation**: preserve scientific meaning, claim strength, numbers, figures, citations, and scope.
4. **Unsupported passages**: produce a gap list or visibly marked scaffold, never polished factual prose.
5. **Substantive scientific changes**: present separately for author review, never as a silent rewrite.

Operations (docs/use-cases.md):

- **local-edit**: passage + nearby context + intended meaning → this skill diagnoses only which section the passage maps to in the section route (old-to-new map); it does not rewrite body prose. A `local-edit` that does not touch section structure, abstract, closing, or venue restrictions does not require the venue brief; its output records `venue_brief_version` if a brief exists, or `venue_brief: none` if none. Arbitrary body-paragraph wording edits are routed to general editing outside MVP.
- **restructure**: current draft + contribution block → old-to-new section map is the first output.
- **venue-adapt**: requires a current brief with `mode: named-venue` before any adaptation → constraint gap list and adaptation plan are the first outputs. With `mode: generic`, decline adaptation and leave venue constraints unknown; produce a generic outline only if the author also requests one. With no ready brief, return a gap to `paper-venue`.

## What this skill does not do

- Does not write tool or harness code; no implementation is shipped.
- Does not quote, excerpt, or reproduce the private book.
- Does not certify scientific correctness of results or proofs.
- Does not duplicate the claim register or the venue brief.
- Does not draft outline, introduction, or paper prose when the gate fails.
- Does not invent venue requirements; missing venue rules stay unknown.

## Traceability

- W-01: outcome, route, new finding, contribution explicit.
- W-02: reasoned route through sections ordered to the contribution.
- G-: one-claim evidence gate, no invented results/citations, preservation of scientific meaning (pass/fail, outside the communication rubric).
- C-: the required brief governs venue constraints; a compliance claim requires `mode: named-venue` and known applicable rules. Compliance is pass/fail, not a rubric score.

**Next skill:** `paper-opening` (drafts introduction from the outline).
