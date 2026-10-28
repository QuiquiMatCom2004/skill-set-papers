# Skill Set Papers — Proposal for the First Release

**Status:** planning draft. No skills, rubric, or GitHub issues have been published.

## Scope and source

The project creates portable Agent Skills for writing, editing, and evaluating Computer Science papers, including figures inside those papers. Books, presentations, other disciplines, tool implementations, and harness code are outside scope. `PROBLEM.md` is canonical; `AGENTS.md` sets repository rules.

The private *Make It Clear* PDF and `.txt` are at the repository root and ignored by Git. Project output must be an original synthesis in English and must not reproduce book text. The accidental nested clone has been removed.

## Proposed principle inventory

These IDs are planning anchors. The principles task verifies chapter pointers against the private source and revises unsupported mappings before any skill or rubric criterion is written.

| ID | Original synthesis | Chapter pointer |
|---|---|---|
| W-01 | Make the desired outcome, route, new finding, and contribution explicit. | 1, 18 |
| W-02 | Give major sections a reasoned route through the paper. | 4, 18 |
| W-03 | Use the opening to orient the reader to the problem and route. | 19 |
| W-04 | Compress completed work into an abstract after the body is understood. | 18, 21 |
| W-05 | End by stating what the work contributed rather than replaying section headings. | 20 |
| W-06 | Make a graph's intended comparison and labels readable. | 28 |
| W-07 | Use specific criticism to find failures of communication. | 5 |
| W-08 | Give important ideas stable, recognizable signals. | 2, 17 |

## Writing starts with supported material

An idea alone is not a paper-writing case. `docs/requirements.md` defines the one entry and sentence-level rule: **a factual claim needs an author-confirmed ID, a resolvable pointer to real supporting material, and wording no broader than that material demonstrates or argues**. At least one central claim must pass before any paper prose is drafted. If none passes, `paper-contributions` returns `insufficient-evidence` and a material-gap list. The gate checks traceability and scope, not scientific correctness. A broad claim can be narrowed to what was actually observed or argued.

`docs/use-cases.md` is the source of truth for three writing cases: `material-no-draft`, `partial-draft`, and `complete-draft`. Venue constraints are a separate dimension; editing and rewriting are operations on existing drafts. Empirical, theoretical, systems, survey, and position papers can all enter when their own kind of central claim has suitable support. A raw dataset, code repository, or research idea alone does not establish an unmeasured performance or efficacy claim.

## MVP v0.1 — five skills (four writing skills + `paper-venue` intake)

| Skill | Job | Output | Principle |
|---|---|---|---|
| `paper-contributions` | Select and formulate a supported central claim from supplied material or an existing draft; own the `insufficient-evidence` outcome. | Versioned Vision / Steps / News / Contributions block referencing claim IDs. | W-01 |
| `paper-outline` | Arrange the supported contribution into a route; show unresolved claims as gaps. | Generic or venue-aware outline, with current block version and claim IDs. | W-01, W-02 |
| `paper-opening` | Draft an introduction from supported claims after an outline; draft the final abstract only after a complete supported body. | Introduction or abstract, linked to claims and block version. | W-03, W-04 |
| `paper-ending` | Close from a complete body and supported contribution, using the ready brief's known heading if required. | Contribution-centered closing linked to claims, block version, and brief version. | W-05 |
| `paper-venue` | Intake: records external venue requirements (source, access date, status) into VENUE_BRIEF.md; the only intake skill under AGENTS.md rule #6. | VENUE_BRIEF.md with brief_version, language, mode, readership, and per-field source/access date/state. | C- (venue requirements; pass/fail, not scored) |

Each portable `SKILL.md` declares input, output, when to use it, when not to use it, and the next skill. Editing skills include meaning-preservation instructions inside their own file. A changed claim or contribution block triggers review of dependent output. Skills do not fabricate research or venue requirements. The five MVP skills run in the order `paper-contributions` → `paper-venue` → `paper-outline` → `paper-opening` → `paper-ending`; `paper-venue` is not a prerequisite of `paper-contributions`.

v0.1 scope note: outline, sections, abstract, and closing are conditioned on the venue brief; there is no body-text skill in v0.1, and W-06 (graph readability) is not executable in v0.1.

## Preparation and validation

1. Verify the principle inventory in `docs/principles.md`, with stable IDs and observable implications.
2. Build `rubric/v0.md` independently from those principles. It scores communication qualities with W- anchors, not the G- integrity gate.
3. Write `docs/evaluation.md` with a representative corpus, the same model working with and without skills, a decision rule fixed before scoring, and rubric stability and sensitivity checks. Report G- and applicable C- compliance separately as pass/fail.
4. Implement the four writing skills and `paper-venue` intake; compare the four writing skills' effect on matched CS-paper drafts after the same venue brief is supplied to both arms. Local self-contained implementation drafts are in `docs/issue-drafts/`; they are not published GitHub issues.

## Later releases

- **v0.2:** `paper-figures` and `paper-terminology`, after confirming their principle mappings. Graphs, other images, and captions need distinct traceability before expanding the figures skill.
- **v0.3:** `paper-review`, applying a stable rubric to an existing draft rather than defining the rubric.
