# AGENTS.md — Skill Set Papers

## What this repo is

`Skill Set Papers` produces a portable set of agent skills and a paper-evaluation rubric,
derived from the communication methodology of Patrick Henry Winston's *Make It Clear*, for
writing, editing, and evaluating Computer Science papers with coding agents
(Claude Code, OpenCode, Codex).

**Source of truth:** `PROBLEM.md` (Spanish, user-authored) is the canonical problem definition.
Every other document derives from it. Never contradict it; if the problem or scope changes,
update `PROBLEM.md` first and propagate the change outward.

## Hard rules

1. **Never reproduce the book.** The book files at the repo root
   (`_OceanofPDF.com_Make_it_Clear_-_Patrick_Henry_Winston.pdf` and its `.txt` version) are
   personal reference material only. Do not quote, excerpt, or copy their text into any
   deliverable, document, commit message, or comment. Skills, docs, and rubric content must be
   an original synthesis of the principles, written in our own words. Never publish,
   redistribute, or track those files in a public remote.
2. **Deliverables are in English.** Skills, rubric, and official docs are written in English
   (`PROBLEM.md` → Idioma). `PROBLEM.md` itself stays in Spanish.
3. **Scope: CS papers only.** In: CS papers in any venue format, including figures inside
   those papers. Out: books, presentations, and papers from other disciplines, even if they
   use computational methods.
4. **No tool or harness code.** Skills may reference and orchestrate existing standard tools,
   but this repository ships no tool implementations and no harness code.
5. **Portable skill format.** Each skill lives in its own directory under `skills/` with a
   `SKILL.md` using the standard Agent Skills format: YAML frontmatter (`name`,
   `description`), then instructions. Keep the `SKILL.md` body lean; move extended material
   into additional files in the same skill directory (progressive disclosure). Skill content
   stays harness-agnostic; harness-specific setup lives in `docs/integrations/`.
6. **Traceability.** Every skill and every rubric criterion must map to at least one
   Winston-derived principle. If you cannot name the principle it implements, it does not
   belong in this repo.

## Repository layout

```
PROBLEM.md   # Canonical problem definition (Spanish) — source of truth
AGENTS.md    # This file
README.md    # Project overview for humans
docs/        # Official documents: principle synthesis, harness integration (planned)
skills/      # The skill set, one directory per skill (planned)
rubric/      # Paper-evaluation rubric (planned)
```

Book files at the root are reference only (see Hard rules #1).

## Working conventions

- There is no build system, test suite, or linting setup in this repo; changes are
  documentation and skill-authoring edits. Keep markdown valid and copy tight.
- Prefer small, focused skills (one job per skill) over monolithic instruction dumps.
- Do not reformat or rewrite `PROBLEM.md` beyond what a task explicitly requires; it is the
  user's document.
- When the rubric exists, treat it as the acceptance test for skill changes: a change should
  measurably improve rubric scores on sample drafts, not merely read well.
