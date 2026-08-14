# AGENTS.md

Project conventions for this repository.

## What this repository is

Documentation set for **SAE** (Structured Agent English), a readability-first
controlled subset of English for writing agent instructions. No code, no
tooling — the documents are the artifact. The authoritative content lives in
`specs/`; `skills/sae/` is a derived artifact that applies the SAE spec to
writing instruction texts.

SAE's ancestry is documented as heritage: **ACE 6.7** (Attempto Controlled
English, see `specs/ace.md`) and its former fork **AIL** (see
`specs/ail.md`). SAE is a **formal break** from both, not an extension: it
drops ACE's punctuation-as-semantics, determiner grammar, and hyphenation.

## Repository layout

- `specs/` — MKF compound node: `SPEC.md` (the spec monolith, the only
  contract), citizen files (`LANGUAGE.md` = SAE language reference,
  `ace.md` = ACE heritage reference, `ail.md` = AIL migration note),
  `index.md` (registry), `log.md` (activity log).
- `skills/sae/` — Agent Skill for writing SAE texts: `SKILL.md` plus
  references (grammar, constructs, worked example, assumptions), written in
  valid SAE. SAE content never names the language ("SAE", "ACE", "AIL") —
  the frontmatter carries the `tags: [sae]` marker instead.
- `.pi*` — local agent state (plans, discussion records, subagent
  artifacts); **never commit** (ignored via `.gitignore`).

## Spec editing rules

- `SPEC.md` declares its own contract in frontmatter: the `sections:` list
  is the set of `##` headings the document must contain, and the body must
  match it exactly (bijection). `context` and `decisions` are the floor;
  they are never removed. Edit the list and the body together.
- Every file in `specs/` carries MKF frontmatter
  (`type`, `title`, `description`, `created`, `updated` — ISO 8601 dates).
- Every change to `specs/` is logged in `log.md` (date + change + reason).
- `index.md` lists every file in `specs/`; internal relative links must
  resolve.
- SAE is a formal break from ACE: SAE may not reintroduce ACE's formal
  machinery, and ACE content stays in `ace.md` as heritage. New SAE
  constructs must respect the accepted proposal's locked core (two layout
  modes, stop-and-report default, open-world conditions, English-phrase
  procedure binding); strictness belongs in profiles.

## Git workflow

- Work directly on `main` (local, single-user project).
- Commit **atomically**: one logical change per commit; stage explicitly
  (`git add <paths>`), then review with `git status` / `git diff --cached`.
- **Never** stage ignored files (`.pi*`).
- Commit message format — Conventional Commits:

  ```
  type(scope): summary
  ```

  - `type`: `docs` (spec/doc changes), `chore` (housekeeping, repo setup),
    `feat`/`fix` (reserved for future code, none today).
  - `scope`: `specs`, `skills`, `project`, or a file name when it fits.
  - `summary`: imperative mood, lowercase, ≤ 72 chars, no trailing period.
  - Add a body (what + why) when the summary alone is not enough.

  Examples:
  - `chore(project): initialize repository with AGENTS.md and specs`
  - `docs(specs): introduce AIL extension reference`
  - `docs(specs): reframe SPEC.md around the ACE-AIL fork`
