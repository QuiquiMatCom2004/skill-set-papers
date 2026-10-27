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
- **Venue brief** (optional): the selected venue's requirements when known (paper type/track, prescribed sections or order, abstract format and length, page or word limits, citation style, applicable disclosure rules). Without it, label output generic and leave unknown constraints open.
- **Existing draft** (for restructure / venue-adapt): current draft plus the requested change.

## Entry gate (claim gate G-)

Apply before any outline section is produced:

1. Verify the contribution block is current, versioned, and references claim IDs.
2. Confirm at least one central claim is `supported` and passes the one-claim rule (author-confirmed ID; resolvable pointer to real supporting material; wording no broader than the material demonstrates or argues).
3. If the block is absent, missing claim IDs, or no central claim passes even after narrowing → route to `paper-contributions`, emit `insufficient-evidence` with the material-gap list, and do not write an outline.
4. Narrow overbroad claims to what the material actually supports, then recheck the same rule. The agent proposes claim IDs, wording, and scope; the author confirms. The agent never approves its own inference and does not certify scientific correctness.

## Output

Produce one outline containing:

1. **Recorded dependencies**: the contribution-block version used and every dependent claim ID used by each section. Change tracking: if evidence or claim scope changes, review outputs dependent on the affected claim IDs; if block meaning changes, review outputs tied to the older block version.
2. **Reasoned section route (W-02)**: order major sections so each follows from the last toward the contribution, not the project's history. State the contribution, outcome, and new finding explicitly (W-01).
3. **Visible gaps**: any section whose claims are not `supported` is shown as an unresolved-claim gap. Never silently omit such a section, never assert its result, and never invent results, proofs, or citations.
4. **Venue handling**:
   - No venue brief: output is explicitly generic; decline any venue-compliance claim; leave unknown venue constraints open.
   - Venue brief supplied: apply only the rules explicitly supplied in the brief. Do not infer additional venue rules or claim full venue compliance from an incomplete brief; missing rules stay unknown.

## Existing drafts (partial-draft / complete-draft)

Before any prose change:

1. **Diagnose first**: diagnose the requested change against the current block and claim IDs.
2. **Old-to-new section map**: produce a map showing how each existing section maps to the new route, before making prose changes.
3. **Preservation**: preserve scientific meaning, claim strength, numbers, figures, citations, and scope.
4. **Unsupported passages**: produce a gap list or visibly marked scaffold, never polished factual prose.
5. **Substantive scientific changes**: present separately for author review, never as a silent rewrite.

Operations (docs/use-cases.md):

- **local-edit**: passage + nearby context + intended meaning → this skill diagnoses only which section the passage maps to in the section route (old-to-new map); it does not rewrite body prose. Arbitrary body-paragraph wording edits are routed to general editing outside MVP.
- **restructure**: current draft + contribution block → old-to-new section map is the first output.
- **venue-adapt**: requires a current target venue brief before any adaptation → constraint gap list and adaptation plan are the first outputs. Without a current venue brief, decline venue adaptation; emit an explicit generic outline and leave unknown venue constraints open; never claim venue compliance.

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
- C-: venue brief applied only when supplied; compliance pass/fail, not a rubric score.
