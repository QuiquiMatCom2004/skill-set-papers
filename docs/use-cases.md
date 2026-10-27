# Use Cases and Writing Start Points for CS Papers

**Status:** planning draft for the four-skill MVP. This document is the source of case selection and permitted work. The single evidence rule, claim register, and submission gate live in `docs/requirements.md`.

## Entry rule

An idea by itself is **not a paper-writing case**. Before selecting a writing case, at least one central claim must satisfy the same rule used for every factual claim in the paper: **an author-confirmed claim ID, a resolvable pointer to real supporting material, and wording no broader than that material demonstrates or argues**. The check establishes traceability and scope, not scientific correctness.

If no central claim passes, return `insufficient-evidence`: identify the proposed claim, what material is missing, and a narrower claim if the existing material supports one. Do not produce a paper outline, introduction, or polished draft from an unsupported idea. Research planning may happen outside this paper-writing skill set.

## Three writing cases

Classify by the supplied document after the entry rule passes. The case selects required research-index fields and work permitted now; it is not just a label.

| Case | Required fields | Work permitted after the gate |
|---|---|---|
| **material-no-draft** | Research problem; supported central claim ID; material pointer and provenance; requested output. No paper prose exists. | Formulate the contribution block, outline the paper, and draft only sections whose factual claims pass the same rule. |
| **partial-draft** | Existing incomplete draft; supported central claim ID; material pointers; requested change and known gaps. | Diagnose and revise existing text; draft supported missing sections; update block and outline if needed. |
| **complete-draft** | Full draft; supported central claim ID; material pointers; requested change and known gaps. | Diagnose, edit, restructure, or adapt to a supplied venue; revise abstract and ending; run submission checks. |

A complete draft with no supported central claim still routes to **diagnosis and a gap list only**. Its presence is not permission to polish unsupported science. A venue brief is a separate dimension for all cases. It is optional for generic work or a local edit, and required for venue adaptation or a submission-ready claim. Missing venue rules are left unknown, never invented.

## Material appropriate to the contribution

| Paper type | Example of material that can support a *bounded* central claim | Claim still blocked without more material |
|---|---|---|
| Empirical | Measured result with enough protocol detail to identify what was measured and in what setting. | General superiority or causality from unanalysed data or selected anecdotes. |
| Theoretical | A stated result with a complete proof, or a narrower lemma whose proof is complete. | A theorem whose proof still has an unacknowledged gap. |
| Systems or design | Implemented or documented design plus an observation, analysis, or test appropriate to the property claimed. | Performance, usability, or reliability from code or a demo alone. |
| Survey or review | Verified source corpus, explicit selection basis, and traceable synthesis or comparison. | Field-wide conclusions from a remembered or unverified reading list. |
| Position or vision | A reasoned argument about a documented gap, grounded in verifiable sources or concrete prior work. | A claim that the proposed direction already works without supporting results. |

The minimum is **one central claim that passes the rule**, not a universal experiment quota. Narrow an overbroad claim to what the material supports: a tested prototype may support an existence or design claim while a speed claim remains blocked. A raw dataset or code repository can be the object of a paper, but their mere existence does not establish utility, accuracy, or performance.

## When each artifact may be written

| Artifact | Earliest start | If a required claim fails the rule |
|---|---|---|
| Contribution block | At least one supported central claim; author confirms its scope. | `paper-contributions` returns `insufficient-evidence` or a narrower supported claim for author confirmation. |
| Outline | Current contribution block with claim IDs; venue brief or explicit generic mode. | Show the unsupported section as a gap; do not silently omit it or assert its result. |
| Introduction | Current block and outline; each factual claim passes the rule. | Remove the unsupported result claim or show a visibly marked gap, not an achieved finding. |
| Methods, design, results, proof, related work | Material appropriate to each factual claim and a resolvable pointer. | Gap list or marked scaffold for that passage; no factual prose for the failed claim. |
| Abstract and ending | Complete body that supports the contributions they state. | Defer final versions; identify which body claims remain unresolved. |
| Figure and caption | Real figure or traceable source data/design, the claim it serves, and its place in the body. | Figure plan or marked placeholder only; no invented result plot. |
| Submission-ready paper | Every check in `docs/requirements.md` passes, including venue route and author review. | Keep `submission: blocked` with exact unresolved items. |

A fixed outline may coexist with unresolved claims, but the paper remains blocked for submission. `docs/requirements.md` defines the independent structure, support, and submission states.

## Rewriting existing work

Editing is an operation on `partial-draft` or `complete-draft`, not a separate writing case or skill.

| Operation | Extra input | First output |
|---|---|---|
| **local-edit** | Passage, nearby context, intended meaning. | Focused diagnosis followed by a meaning-preserving edit. |
| **restructure** | Current draft and contribution block. | Old-to-new section map before prose changes. |
| **venue-adapt** | Current draft and target venue brief. | Constraint gap list and adaptation plan before prose changes. |

Preserve scientific meaning, claim strength, numbers, citations, figures, and scope. A substantive scientific change is a separate proposal for the author, not a silent rewrite. If a central claim fails the entry rule, the first and only output is a diagnosis of evidence gaps until the author supplies or confirms adequate material.

## Routing examples

| # | Input | Expected route and output |
|---|---|---|
| 1 | Measurements with protocol, no prose | `material-no-draft`; a bounded empirical claim can support an outline and relevant result prose. |
| 2 | Stated theorem with complete proof, no prose | `material-no-draft`; a proof-backed claim can support theoretical prose. |
| 3 | Implemented system with documented observation, no prose | `material-no-draft`; describe the observed property, not unmeasured superiority. |
| 4 | Verified source corpus and documented gap, no prose | `material-no-draft`; survey or position argument limited to those sources. |
| 5 | Partial draft with a supported central claim | `partial-draft`; diagnose and revise supported passages. |
| 6 | Partial draft whose central claim has no support | Gap diagnosis only; no prose embellishment until a narrower claim or material passes. |
| 7 | Complete draft, request to edit one paragraph | `complete-draft` + `local-edit`; preserve meaning and citations. |
| 8 | Complete draft, request to adapt to a named venue | `complete-draft` + `venue-adapt`; require a current venue brief before claiming compliance. |
| 9 | Only an idea or question, no supporting material | `insufficient-evidence`; list needed research, no paper prose. |
| 10 | Only raw data or code, with no bounded central claim they support | `insufficient-evidence`; identify analysis or observation needed. |
| 11 | Request to invent results, proofs, or citations | No factual draft; provide a gap list or marked scaffold. |
| 12 | Paper outside Computer Science | Out of scope for this skill set. |

## Provenance

Every skill and communication-rubric criterion maps to a Winston-derived `W-` principle under `AGENTS.md`. Evidence integrity (`G-`) is a pass/fail gate, and selected-venue conventions (`C-`) are external requirements; neither is presented as a Winston principle. See `docs/requirements.md`. No Toulmin, IMRaD, or PRISMA template is imposed across CS paper types.

The private book PDF and `.txt` at the repository root are reference material. This guide is an original synthesis and contains no book excerpts.
