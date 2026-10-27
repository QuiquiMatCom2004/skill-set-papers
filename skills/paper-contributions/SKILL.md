---
name: paper-contributions
description: Use to check whether supplied CS research material can support a paper, select its central contributions, and produce a versioned Vision/Steps/News/Contributions block; returns an evidence-gap list when no central claim is supported. Maps to Winston principle W-01.
---

# paper-contributions — W-01

## Purpose

Selects and formulates one or more supported central claims from supplied real material or an existing CS-paper draft, enforces the one-claim evidence gate before any paper prose is written, and emits a versioned Vision / Steps / News / Contributions block that references supported claim IDs.

Maps to **W-01**: make the desired outcome, route, new finding, and contribution explicit so the reader knows what was done and why it matters (docs/principles.md).

## When to use this skill

Use when a CS-paper writing request needs its evidence checked and central contribution established before outlining or drafting. An idea-only request may invoke this skill to receive the `insufficient-evidence` outcome.

Permitted entry cases (docs/use-cases.md):

- `material-no-draft` — material exists, no paper prose yet
- `partial-draft` — an incomplete draft exists, central claim supported
- `complete-draft` — a full draft exists, central claim supported

## When not to use this skill (routing)

Do not use when:

- A current contribution block already passes the gate and the request is only for an outline → route to `paper-outline`; opening → `paper-opening`; ending → `paper-ending`. A focused body-paragraph wording edit → route to general editing outside MVP (this skill set ships no local prose-editing skill); do not send it to a paper-writing skill.
- The input is raw data or code only, with no bounded central claim it supports → return `insufficient-evidence`: identify the analysis or observation needed to bound a claim; emit no paper prose.
- The request is to invent results, proofs, or citations → return a gap list, no factual prose.
- The paper is outside Computer Science → out of scope

**Next skill:** `paper-outline` (arranges the supported contribution into a route; shows unresolved claims as gaps). Do not call any other writing skill before this gate passes.

## Inputs

- **Research index**: identifies the task and references the supplied material, any existing draft, the claim register, the current contribution block, and missing inputs. It does not copy those artifacts.
- **Supplied material or draft**: real research material (result tables and protocols, proofs or theorem numbers, artifact paths and observations, verifiable source identifiers) or an existing CS-paper draft.
- **Venue brief** (optional): venue requirements when known; required only for venue adaptation or a submission-compliance claim. Without it, label output generic and leave constraints open.

## Claim gate (G- integrity requirement)

Before any paper prose, apply the one-claim rule to every candidate central claim:

> A factual claim may be written as fact only if it has (1) an author-confirmed claim ID, (2) a resolvable pointer to real supporting material, and (3) wording no broader than that material demonstrates or argues.

Procedure:

1. **Propose** candidate central claim IDs and evidence pointers from the supplied material. Claim class is one of: empirical, theoretical, design, literature-based, position.
2. **Check** each candidate: does it have an author-confirmed ID? a resolvable pointer? wording no broader than the support?
3. **Narrow** any overbroad claim to what the material actually supports, then recheck the same rule. A tested prototype may support "we implemented this architecture" while "it is faster than prior systems" stays blocked until a comparison exists.
4. **Require author confirmation** of claim class, support status, and intended scope. The agent proposes; the author confirms. The agent never approves its own inference and does not certify scientific correctness.
5. **Require at least one central claim to pass** before entering writing.

A passing central claim does not authorize other claims: retain unsupported noncentral claims in the register as visible gaps until each separately passes the same rule before factual prose uses it.

## `insufficient-evidence` outcome

If no central claim passes the gate even after narrowing:

- Return `insufficient-evidence`.
- Include an exact material-gap list: for the proposed claim, what material is missing, and — if the existing material supports one — a narrower supported claim for author confirmation.
- Emit **no paper prose, no outline, and no introduction**.

## Output: versioned contribution block

When at least one central claim passes, emit a compact, versioned block:

**Vision / Steps / News / Contributions**

Each entry references supported claim IDs. The block is a projection, not a second claim register.

Record the contribution-block version and the claim IDs it uses. Every downstream output that cites these IDs depends on this version.

## Invalidation and change tracking

- Change the contribution-block version when the block's meaning changes.
- If evidence or claim scope changes, review outputs dependent on the affected claim IDs.
- If block meaning changes, review outputs tied to the older block version.
- A matching block version alone does not guarantee the evidence remains current.

## Preservation of existing-paper wording

Before editing an existing draft (`partial-draft` or `complete-draft`):

1. Diagnose the requested change first.
2. Preserve scientific meaning, claim strength, numbers, figures, citations, and scope.
3. Present any substantive scientific change separately for author review — never as a silent rewrite.
4. Unsupported passages produce a gap list or visibly marked scaffold, never polished factual prose.

## What this skill does not do

- Does not write tool or harness code; no implementation is shipped.
- Does not quote, excerpt, or reproduce the private book.
- Does not certify scientific correctness of results or proofs.
- Does not duplicate the claim register or the venue brief.
- Does not draft outline, introduction, or paper prose when the gate fails.
- Does not invent venue requirements; missing venue rules stay unknown.
