# AGENTS.md

Project conventions for this repository.

## What this repository is

Documentation set for **ACE 6.7** (Attempto Controlled English) and its fork
**AIL** (Agent Instruction Language), a strict superset of ACE adding
sequences and procedures. No code, no tooling — the documents are the
artifact. The authoritative content lives in `specs/`; `skills/ail/` is a
derived artifact that applies the AIL spec to writing instruction texts.

## Repository layout

- `specs/` — MKF compound node: `SPEC.md` (the spec monolith, the only
  contract), citizen files (`LANGUAGE.md` = ACE base reference, `ail.md` =
  AIL extension reference), `index.md` (registry), `log.md` (activity log).
- `discussions/` — design discussion snapshots; read them for design
  rationale (esp. before changing AIL content).
- `skills/ail/` — Agent Skill for writing AIL texts: `SKILL.md` plus
  references (grammar, constructs, worked example, assumptions), written in
  valid AIL. AIL content never names the language ("AIL", "ACE") — the
  frontmatter carries the `tags: [ail]` marker instead.
- `.pi/plans/` — plan state; commit it like any other project doc.
- `.pi-subagents/` — transient agent run artifacts; **never commit**
  (ignored via `.gitignore`).

## Spec editing rules

- `SPEC.md` has a `## Must contain` checklist — the only hard contract.
  Replace content and `[placeholders]`; never restructure the checklist.
- Every file in `specs/` carries MKF frontmatter
  (`type`, `title`, `description`, `created`, `updated` — ISO 8601 dates).
- Every change to `specs/` is logged in `log.md` (date + change + reason).
- `index.md` lists every file in `specs/`; internal relative links must
  resolve.
- AIL is a strict superset of ACE: the AIL docs may clarify semantics but
  must never reject syntax that ACE accepts.

## Git workflow

- Work directly on `master` (local, single-user project).
- Commit **atomically**: one logical change per commit; stage explicitly
  (`git add <paths>`), then review with `git status` / `git diff --cached`.
- **Never** stage `.pi-subagents/` or anything ignored.
- Commit message format — Conventional Commits:

  ```
  type(scope): summary
  ```

  - `type`: `docs` (spec/doc changes), `chore` (housekeeping, repo setup),
    `feat`/`fix` (reserved for future code, none today).
  - `scope`: `specs`, `skills`, `project`, or a file name when it fits.
  - `summary`: imperative mood, lowercase, ≤ 72 chars, no trailing period.
  - Add a body (what + why) when the summary alone is not enough; reference
    `discussions/` snapshots for design rationale.

  Examples:
  - `chore(project): initialize repository with AGENTS.md and specs`
  - `docs(specs): introduce AIL extension reference`
  - `docs(specs): reframe SPEC.md around the ACE-AIL fork`
