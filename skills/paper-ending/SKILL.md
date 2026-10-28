---
name: paper-ending
description: Write or revise the closing of a CS paper from a complete body, supported contribution claims, and a ready venue brief. Return an exact gap list when a required claim fails, respect known venue rules, and record block, brief, and claim dependencies. Maps to Winston principle W-05.
---

# paper-ending — W-05

## Purpose

Write or revise a closing that states what the work actually contributed, based only on the complete body and its supported contribution claims.

Maps to **W-05**: end by stating what the work contributed, instead of merely replaying section headings or the problem (docs/principles.md). A venue-required heading may be used without changing that contribution-centered content.

## When to use this skill

Use when the CS paper has a complete body and the request is to write or revise its closing. This skill applies in:

- `partial-draft` — after the body is complete, to write a missing closing
- `complete-draft` — during revision, to revise an existing closing

Required inputs (referenced, not copied):

- **Research index**: task, supplied material, any existing draft, claim register, current contribution block, missing inputs.
- **Current contribution block**: versioned Vision / Steps / News / Contributions block referencing supported claim IDs (paper-contributions).
- **Complete body**: the sections whose claims the closing will state.
- **Section map**: the current outline or a map derived from the complete draft, used to check body completeness.
- **Supported central claim IDs**: each required closing claim must pass the one-claim rule.
- **Venue brief** (required, from `paper-venue`): known heading and length constraints, with `mode: named-venue` or `mode: generic`. Record `venue_brief_version` and `language`. Without a ready brief, return a gap to `paper-venue` and emit no closing prose. A generic brief permits explicitly generic output. Write in the brief's `language`.

## Entry gate — G- integrity requirement (enforced separately from W-05 quality)

Body completeness check: confirm every required body section in the current outline, draft-derived section map, or venue brief is present and its material claims are supported; otherwise return the closing gap list and emit no affirmative closing prose. Verify a current brief from `paper-venue` exists with `mode: named-venue` or `mode: generic`; if missing or still awaiting a shortlist choice, return a gap to `paper-venue` and emit no closing prose. Before any affirmative closing, apply the one-claim rule (docs/requirements.md) to every claim the closing will state:

> A factual claim may be written as fact only if it has (1) an author-confirmed claim ID, (2) a resolvable pointer to real supporting material, and (3) wording no broader than that material demonstrates or argues.

Each required closing claim needs: an author-confirmed ID, resolvable real support, and scope no broader than the support. If the body or contribution block is missing or stale, or any required claim fails, return the **exact gap list** (CLOSING_GAP_LIST.md) naming the incomplete artifact or failed claim, the missing material, and any narrower supported claim — and emit **no affirmative closing prose**. A gap failure blocks the paper regardless of communication quality.

Do not narrow or confirm claims on the author's behalf. The agent proposes; the author confirms class, support status, and intended scope.

## Output: contribution-centered closing

State only contributions demonstrated or argued by the complete body:

- Do not merely replay section headings or the problem.
- Do not increase claim strength beyond what the body supports.
- Do not silently alter scientific meaning, numbers, figures, citations, or scope.

Heading and length:

- Use known heading and length constraints from the required brief (for example, a venue-required 'Conclusions' heading is allowed).
- With `mode: generic`, label the result **generic** and make **no venue-compliance claim**. A compliance claim requires `mode: named-venue` and author-confirmed applicable rules. Missing venue rules stay unknown, never invented.

Limitations:

- A limitations section is **not** a Winston requirement. Include it only if the venue or author requires it, and present it as venue/author input.

Record:

- Record the contribution-block **version**, `venue_brief_version`, `language`, and the **claim IDs** the closing uses. Every downstream output citing these IDs depends on this version.

### Venue brief re-verification (closing)

If the closing's recorded `venue_brief_version` is lower than the current `VENUE_BRIEF.md` version, list the changed fields, mark the affected closing elements, do not rewrite until the author confirms, then record the new version. If no changed field affects the closing, record the new version and say so.

## Before editing existing closing text

Diagnose the existing closing first. Preserve meaning, claim strength, numbers, figures, citations, and scope. Present any substantive scientific change as a separate proposal for author review — never as a silent rewrite. Unsupported passages produce a gap list or visibly marked scaffold, never polished factual prose.

## Invalidation and change tracking

- Change the contribution-block version when the block's meaning changes.
- If evidence or claim scope changes, review the closing output dependent on the affected claim IDs.
- If block meaning changes, review the closing tied to the older block version.
- A matching block version alone does not guarantee the evidence remains current.

## Use / do-not-use / next-skill routing

**Use this skill when:**

- a current contribution block exists with supported central claim IDs;
- the body is complete and supports the contributions the closing will state;
- the request is to write or revise the closing.

**Do not use this skill when:**

- no central claim passes the one-claim rule or the body is incomplete → return an exact gap list, no prose;
- the request is to invent results, proofs, or citations → gap list, no factual prose;
- the paper is outside Computer Science → out of scope;
- an existing closing must be edited but evidence or block meaning changed → re-review first.

**Next skill:** none within the v0.1 writing skills (paper-ending is the last). After a closing is written, run the submission-ready gate (docs/requirements.md); `paper-review` (v0.3) is the later candidate for diagnosing weak endings. Do not call any other writing skill before the entry gate passes.

## G- / C- gates vs W-05 communication quality

G- integrity gates (claim rule, no invented results or citations, preservation of meaning) and C- venue requirements are pass/fail and enforced separately from W-05 communication quality. A gate failure blocks the paper regardless of rubric score; a venue-compliance claim requires a current brief with `mode: named-venue` and author-confirmed applicable rules.

## What this skill does not do

- Does not write tool or harness code; no implementation is shipped.
- Does not quote, excerpt, or reproduce the private book.
- Does not certify scientific correctness of results or proofs.
- Does not duplicate the claim register or the venue brief.
- Does not produce affirmative closing prose when the entry gate fails.
- Does not invent venue requirements; missing venue rules stay unknown.
