# docs/principles.md — Winston-derived communication principles (W-01…W-08)

**Status:** planning draft. Original synthesis only. This document is the single place where principle IDs are defined; later skills and rubric criteria cite these IDs.

## Source and authorization

These principles are an original synthesis, in the project's own words, of the communication methodology in Patrick Henry Winston's *Make It Clear*. Per `AGENTS.md` hard rule #1, this document contains no quotation, excerpt, or copied wording from the book. The private PDF and `.txt` at the repository root were consulted as reference material. Nothing here reproduces, publishes, or redistributes them.

## Principle inventory (W-01…W-08)

Each principle has a stable ID, an original one-to-two sentence synthesis, observable communication behavior, and verified source chapter(s). Chapter pointers were checked against the private reference (chapters 1–5, 17–23, 28). Every mapping below is supported; none was removed or revised.

| ID | Original synthesis | Source chapter(s) | Observable communication behavior |
|----|--------------------|-------------------|-----------------------------------|
| W-01 | Make the desired outcome, route, new finding, and contribution explicit so the reader knows what was done and why it matters. | 1, 18 | A reader can identify the contribution and its relation to the problem in the abstract, opening, and ending; a venue-required heading may be used without changing that content. |
| W-02 | Give major sections a reasoned route through the paper, ordered to lead the reader to the contribution rather than to follow the history of the work. | 4, 18 | Section order and transitions support the contribution; the reader can explain why each major section follows the last. |
| W-03 | Use the opening to orient the reader to the problem worth solving and the route taken, so a busy reader can decide whether to read on. | 19 | The opening states the problem, the approach, and the paper's route. |
| W-04 | Compress completed work into an abstract after the body is understood, using concrete details appropriate to the contribution. | 18, 21 | The abstract accurately reflects the completed body, including the problem, route, new finding, and contribution; details are specific where the work supports them. |
| W-05 | End by stating what the work contributed, instead of merely replaying section headings or the problem. | 20 | The ending states the supported contributions plainly. |
| W-06 | Make a graph's intended comparison and labels readable without a misleading visual scale or distracting decoration. | 28 | When a graph is present, its labels and scale let the reader identify the intended comparison accurately; decorative choices do not obscure it. |
| W-07 | Use specific criticism to find failures of communication and make feedback actionable and principled. | 5 | A review comment identifies a concrete communication problem, proposes a change, and explains its benefit. This is a review-process behavior, not a property of the final paper. |
| W-08 | Give important ideas stable, recognizable signals and surface clues readers can extract quickly. | 2, 17 | Key ideas are named consistently and signaled in the title, abstract, headings, or summaries where appropriate; those signals help readers find the paper's main points. |

## Traceability matrix

Each skill and each rubric criterion maps to at least one Winston-derived principle (`AGENTS.md` rule 6). The rubric finalizes its criteria independently of skill text; the matrix below records the proposed mappings only.

| W-ID | Principle | MVP skill(s) (v0.1) | Proposed rubric criterion | Later candidate |
|------|-----------|---------------------|---------------------------|-----------------|
| W-01 | Outcome, route, finding, contribution explicit | `paper-contributions` | Contribution clarity: the central claim and what it contributes are stated explicitly and early | `paper-terminology` (stable naming of the core idea) |
| W-02 | Reasoned route through sections | `paper-outline` | Route coherence: section order leads to the contribution | `paper-terminology` (consistent signals for section roles) |
| W-03 | Opening orients to problem and route | `paper-opening` (introduction) | Opening orients: problem, approach, and route are stated so a reader can decide to continue | `paper-review` (diagnosing weak openings) |
| W-04 | Abstract compressed from completed body | `paper-opening` (abstract) | Abstract fidelity: problem, route, finding, and contribution match the completed body | `paper-review` (abstract–body consistency) |
| W-05 | Ending states contributions | `paper-ending` | Ending states supported contributions instead of replaying section order | `paper-review` (diagnosing weak endings) |
| W-06 | Graph comparison and labels readable | — (no v0.1 skill; figures reserved for v0.2) | Conditional graph readability: labels, scale, and visual choices make the intended comparison clear | `paper-figures` (v0.2) |
| W-07 | Specific criticism finds communication failures | — (no v0.1 skill; review reserved for v0.3) | — (review-process principle; do not score as a paper property) | `paper-review` (v0.3) |
| W-08 | Stable, recognizable signals for important ideas | — (terminology reserved for v0.2) | Signal strength: salient ideas and surface clues let a reader extract the essence quickly | `paper-terminology` (v0.2) |

Coverage: all four MVP skills (`paper-contributions`, `paper-outline`, `paper-opening`, `paper-ending`) are traced to at least one W- principle. Later candidates — `paper-figures` (figures), `paper-terminology` (terminology), and `paper-review` (review) from `docs/skill-proposal.md` — are traced so their W- anchors exist before those skills are written.

## G- integrity gates (distinct from W- principles)

`G-` items are research-integrity gates, not Winston principles and not rubric scores. They are evaluated as pass/fail outside the communication rubric:

- The one-claim rule: a factual claim is stated only with an author-confirmed ID, a resolvable pointer to real supporting material, and wording no broader than the material demonstrates or argues (`docs/requirements.md`).
- No invented results, proofs, or citations.
- Preservation of scientific meaning, claim strength, numbers, figures, citations, and scope when editing existing drafts.

A `G-` gate failure blocks the paper regardless of rubric score.

## C- venue requirements (distinct from W- principles)

`C-` items are current external venue requirements, recorded with source and access date. They are compliance pass/fail, not scored as rubric criteria unless a distinct communication criterion has a genuine `W-` anchor. Examples (illustrative only, checked 2026-10-27): the NeurIPS paper checklist and the CHI 2026 author guide. Recheck the chosen venue's current requirements before submission; missing venue rules are left unknown, never invented.

A `C-` compliance failure blocks a venue-specific submission claim but does not change rubric scores.

## Verification note

All eight chapter pointers in `docs/skill-proposal.md` (W-01: 1, 18; W-02: 4, 18; W-03: 19; W-04: 18, 21; W-05: 20; W-06: 28; W-07: 5; W-08: 2, 17) were verified against the table of contents and chapter bodies of the private reference. No mapping was unsupported, so no W-ID was removed or revised. No book text is quoted or excerpted anywhere in this file.
