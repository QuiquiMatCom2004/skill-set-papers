# Skill Set Papers

A portable set of Agent Skills for communicating Computer Science research clearly. The
skills and [communication rubric](rubric/v0.md) are an original synthesis of principles
from Patrick Henry Winston's *Make It Clear*. They help agents structure and revise papers
while keeping research evidence and venue rules separate from writing quality.

## Available skills

| Skill | Job | Main output |
|---|---|---|
| [paper-contributions](skills/paper-contributions/SKILL.md) | Check the central claim against supplied material and state the contribution. | Claim register and versioned Vision / Steps / News / Contributions block, or an exact evidence-gap list. |
| [paper-venue](skills/paper-venue/SKILL.md) | Record requirements for a named venue or an explicitly chosen generic mode. This is an intake skill; it writes no paper prose. | Versioned `VENUE_BRIEF.md` with sources and unknown fields. |
| [paper-outline](skills/paper-outline/SKILL.md) | Arrange supported claims into a reasoned section route. | Outline with claim dependencies and visible gaps. |
| [paper-opening](skills/paper-opening/SKILL.md) | Write or revise the introduction; write the final abstract only after the body supports it. | Introduction and, when ready, abstract. |
| [paper-ending](skills/paper-ending/SKILL.md) | Close a complete paper by stating its supported contributions. | Contribution-centered ending or an exact closing-gap list. |

Each skill is a portable `SKILL.md` with YAML frontmatter. The repository contains no tool
or harness implementation. Harness-specific integration guides are planned; compatibility
with Claude Code, OpenCode, and Codex has not been formally tested.

## How to use the set

1. Supply a CS research artifact or existing draft, its provenance, and the desired paper
   task. An idea alone, raw data alone, or code alone cannot establish a result. See the
   [three writing cases](docs/use-cases.md) and [shared requirements](docs/requirements.md).
2. Run `paper-contributions`. The agent proposes claim IDs and pointers to supporting
   material; the author confirms the claim class, support, and intended scope. At least one
   central claim must pass this gate before paper prose is written. If none does, the output
   is `insufficient-evidence` with the precise material needed.
3. Choose a named venue or explicitly choose generic work, and declare the paper language.
   Run `paper-venue` to record the brief. A named venue's current rules need sources and
   author confirmation; generic output makes no venue-compliance claim.
4. Run `paper-outline`, then `paper-opening`. Draft or revise body sections only from
   material that supports their factual claims. Once the body is complete and supported,
   finish the abstract and run `paper-ending`.
5. Apply the [submission checks](docs/requirements.md#submission-ready-gate) and score
   communication with [rubric v0](rubric/v0.md). Research-integrity gates (`G-`) and venue
   compliance (`C-`) are pass/fail checks outside the communication score.

For an existing paper, diagnose the requested change first and preserve its scientific
meaning, numbers, figures, citations, and claim strength. The current set has no dedicated
technical-body drafting or paragraph-editing skill; general editing outside this MVP handles
that work under the same evidence and preservation rules.

## Project status

The five-skill MVP, [principle inventory](docs/principles.md),
[use cases](docs/use-cases.md), [requirements](docs/requirements.md), rubric, and
[evaluation protocol](docs/evaluation.md) are available. The controlled evaluation result
is **pending**: a permitted CS-paper corpus, frozen skill versions, and evaluators are
still needed. A polished draft is not automatically scientifically validated or ready to
submit.

## Scope and source material

This project covers CS papers in journal, conference, and preprint formats, including
figures within papers. Books, presentations, and papers outside CS are out of scope. All
skills, rubric, and official docs are in English; [PROBLEM.md](PROBLEM.md) is the canonical
user-authored problem statement in Spanish.

The private book PDF and text file at the repository root are reference material only.
They are ignored by Git and must never be quoted, copied, or published with this project.
See [AGENTS.md](AGENTS.md) for repository rules.
