# Skill Set Papers

A portable set of agent skills and a paper-evaluation rubric, derived from the communication
methodology of Patrick Henry Winston's *Make It Clear*, that help coding agents write, edit,
and evaluate Computer Science papers.

## The problem

Coding agents increasingly assist with scientific paper writing, but they do it without a
communication methodology: the result is often technically correct text that is poorly
structured and unclear. No portable skill set encodes established scientific-communication
principles so that any harness (Claude Code, OpenCode, Codex) can apply them when writing,
editing, and evaluating papers.

## Deliverables

1. **Skill set** — one directory per skill, each with a standard-format `SKILL.md`. Skills may
   orchestrate existing tools where deterministic checks are possible (e.g., clarity linters);
   no tool code is produced in this project.
2. **Evaluation rubric** — a paper-quality rubric built from Winston's principles, used to
   validate the skill set's effect on drafts.

## Out of scope

- Tool implementations (assumed to already exist; skills only reference and orchestrate them).
- Harness implementations (Claude Code, OpenCode, Codex assumed to exist; this project ships
  integration documentation only).
- Books and presentations.
- Papers outside Computer Science, even if they use computational methods.

In scope: CS papers in any venue format (conference, journal, preprint), **including figures
inside those papers**.

## Harness integration

The skills use portable Agent Skills files. Harness-specific installation and usage guides
are planned for `docs/integrations/`; compatibility has not yet been tested here.

## Source material

All skills and the rubric are an **original synthesis** of the principles in *Make It Clear*.
The book's text is never reproduced, excerpted, or distributed with this project.

## Language

All deliverables (skills, rubric, docs) are in **English**. `PROBLEM.md`, the canonical problem
definition, is kept in Spanish as the user-authored source of truth.

## Repository layout

```
PROBLEM.md    # Canonical problem definition (Spanish) — everything derives from it
AGENTS.md     # Working rules for coding agents in this repo
README.md     # This file
docs/         # Principles, use cases, requirements, evaluation protocol, issue drafts
skills/       # MVP skills (one directory per skill, each with SKILL.md)
rubric/       # Communication rubric
```

## Status

MVP draft available on `feat/skill-set-papers-mvp`: principle inventory,
communication rubric, evaluation protocol, and four writing skills. The evaluation result
is **PENDING** until a permitted CS-paper corpus, frozen skill versions, and evaluators
are available. See `docs/evaluation.md` for the pre-run gate.
