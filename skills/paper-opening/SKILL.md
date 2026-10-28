---
name: paper-opening
description: Drafts or revises a CS paper's introduction and final abstract from a current contribution block and outline/section map; enforces the factual-claim gate before any introduction prose, writes the final abstract only from a complete supported body, records block version and dependent claim IDs, applies venue rules only from a supplied brief, and returns exact gap lists when claims fail. Maps to Winston principles W-03 and W-04.
---

# paper-opening — W-03, W-04

## Purpose

Writes or revises a CS paper's introduction and, only when the body is complete and supported, its final abstract. The introduction orients the reader to the problem worth solving, the approach taken, and the paper's route so a busy reader can decide whether to read on (W-03). The final abstract compresses the completed work — problem, route, new finding, contribution — using concrete details the body supports (W-04).

Maps to:

- **W-03**: use the opening to orient the reader to the problem worth solving and the route taken (docs/principles.md).
- **W-04**: compress completed work into an abstract after the body is understood, using concrete details appropriate to the contribution (docs/principles.md).

G- integrity gates (one-claim rule, no invented results or citations, preservation of meaning) and C- venue requirements are enforced as pass/fail, separately from W-03/W-04 communication quality. A gate failure blocks the paper regardless of communication quality.

## When to use this skill

Use when:

- A current, versioned contribution block exists (emitted by `paper-contributions`) and it references supported claim IDs.
- A current outline or existing-paper section map exists (emitted by `paper-outline` or derived from a complete draft).
- The request is to write or revise the introduction, or to write the final abstract after a complete supported body.
- A current venue brief from `paper-venue` with `mode: named-venue` or `mode: generic` is required; without it return a gap to `paper-venue` and emit no introduction or abstract. Write in the brief's `language`; produce a second abstract when its `secondary_abstract_language` is set. `paper-venue` owns the mode/language question.

Permitted entry cases (docs/use-cases.md), each only after the claim gate passes:

- `material-no-draft` — material exists, no paper prose yet
- `partial-draft` — an incomplete draft exists, central claim supported (abstract only once its body is complete)
- `complete-draft` — a full draft exists, central claim supported

## When not to use this skill (routing)

Do not use when:

- No current contribution block exists, or no central claim passes the one-claim gate → route to `paper-contributions`; return `insufficient-evidence` with the material-gap list (proposed claim, missing material, any narrower supported claim); emit **no introduction and no abstract**, and never a provisional introduction from an idea alone.
- The abstract is requested but the body is incomplete → defer the final abstract and identify which body claims remain unresolved. A planning note or outline is not a paper abstract.
- The request is to invent results, proofs, or citations → return a gap list or visibly marked scaffold, no factual prose.
- The paper is outside Computer Science → out of scope.
- A venue-compliance claim is requested but the current brief is not `mode: named-venue` → decline the compliance claim; leave unknown venue constraints open. A missing brief blocks this skill; a generic brief permits only explicitly generic output.

**Next skill:** `paper-ending` (writes the closing that states supported contributions, W-05). `paper-opening` does not write body prose, methods, results, proofs, related work, or the closing.

## Inputs (referenced, not copied)

- **Research index**: identifies the task and references the supplied material, any existing draft, the claim register, the current contribution block, and missing inputs.
- **Current versioned contribution block**: Vision / Steps / News / Contributions referencing supported claim IDs, plus the block version.
- **Outline or existing-paper section map**: major sections in reasoned order with dependent claim IDs; or the section map of an existing draft being edited.
- **Existing draft** (for edits): current draft plus the requested change.
- **Venue brief** (required, from `paper-venue`): the selected venue's known requirements, with `mode: named-venue` or `mode: generic`. Record `venue_brief_version` and `language` as dependencies for both outputs.

## Entry gate — G- integrity requirement (enforced separately from W-03/W-04 quality)

Apply before any introduction prose or final abstract is produced:

0. Verify a current venue brief from `paper-venue` exists with `mode: named-venue` or `mode: generic`. If missing or still awaiting a shortlist choice, return a gap to `paper-venue` and emit no introduction or abstract. This skill does not ask the mode/language question.

1. Verify the contribution block is current, versioned, and references supported claim IDs. If the block is absent → route to `paper-contributions`.
2. Confirm at least one central claim is `supported` and passes the one-claim rule: an author-confirmed claim ID, a resolvable pointer to real supporting material, and wording no broader than that material demonstrates or argues.
3. Apply the one-claim rule again to **every** factual claim the introduction or abstract will state — result, method, background, or contribution. Each needs an author-confirmed ID, a resolvable real support pointer, and scope no broader than the support.
4. A failed noncentral claim may be omitted **only with the omission recorded as a visible gap**; it is never polished into an achieved finding. If no central claim passes even after narrowing, return `insufficient-evidence` and emit no paper prose. If a required abstract claim fails, defer the final abstract until that claim is supported or the author confirms a narrower supported scope.
5. The agent proposes claim IDs, wording, and scope; the author confirms class, support status, and intended scope. The agent never approves its own inference and does not certify scientific correctness.

### Venue brief re-verification (introduction and abstract)

If the recorded `venue_brief_version` for the introduction/abstract is lower than the current `VENUE_BRIEF.md` version, list the changed fields, mark the affected introduction or abstract elements, do not rewrite until the author confirms, then record the new version. If no changed field affects the introduction or abstract, record the new version and say so.

## Output: introduction (W-03)

Draft the introduction from the current block and outline/section map only:

- State the problem, the approach, and the paper's route so a reader can decide whether to continue.
- State the contribution, outcome, and new finding explicitly and early, consistent with the block's Vision / Steps / News / Contributions.
- Tie every factual statement to a passing claim ID; wording no broader than the supporting material.
- Show any section or claim that is not `supported` as a visible gap; never silently omit it or assert its result.
- **Recorded dependencies**: record the contribution-block **version**, `venue_brief_version`, `language`, and every **dependent claim ID** the introduction uses. Every output citing these IDs depends on this version.

Heading, format, and length:

- Apply known format and length constraints from the required brief. With `mode: generic`, label the introduction **generic** and make no venue-compliance claim. A compliance claim requires `mode: named-venue` and author-confirmed applicable rules; missing rules stay unknown.

## Output: final abstract (W-04)

Draft the final abstract **only after a complete body that supports the contributions it states**:

- Compress the completed work: problem, route, new finding, contribution, with concrete details the body supports.
- A planning note, an outline, or an incomplete body is **not** a final abstract; do not present one as such.
- Tie every factual statement to a passing claim ID; do not increase claim strength beyond what the body supports.
- **Recorded dependencies**: record the contribution-block **version**, `venue_brief_version`, `language`, and every **dependent claim ID** the abstract uses.
- Apply known abstract format and length from the required brief. With `mode: generic`, label the abstract **generic** and make no venue-compliance claim. A compliance claim requires `mode: named-venue` and author-confirmed applicable rules.

## Before editing existing introduction or abstract text

Diagnose the requested change first:

1. Diagnose against the current block and claim IDs.
2. Produce an old-to-new map for any restructure before prose changes.
3. Preserve scientific meaning, claim strength, numbers, figures, citations, and scope.
4. Unsupported passages produce a gap list or visibly marked scaffold, never polished factual prose.
5. Present any substantive scientific change as a separate proposal for author review — never as a silent rewrite.

## What this skill does not do

- Does not write tool or harness code; no implementation is shipped.
- Does not quote, excerpt, or reproduce the private book.
- Does not certify scientific correctness of results or proofs.
- Does not duplicate the claim register or the venue brief.
- Does not produce an introduction or abstract when the central-claim gate fails, including no provisional introduction from an idea alone. A failed noncentral claim is shown as a visible gap; if omitted from an otherwise supported introduction, the omission is recorded as a visible gap.
- Does not invent venue requirements; missing venue rules stay unknown.

## Traceability

- W-03: opening orients to problem, approach, and route so a reader can decide to continue.
- W-04: final abstract compressed from the completed supported body.
- G-: one-claim evidence gate, no invented results/citations, preservation of scientific meaning (pass/fail, outside the communication rubric).
- C-: the required brief governs venue constraints; a compliance claim requires `mode: named-venue` and author-confirmed applicable rules. Compliance is pass/fail, not a rubric score.
