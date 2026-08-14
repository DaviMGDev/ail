# SAE — Documentation Set

Reference documentation for **Structured Agent English (SAE)**, a controlled
subset of English for writing agent instructions that remain understandable to
an ordinary reader even without access to the formal specification.

SAE has one primary design goal:

> A person who reads a SAE text for the first time should be able to
> understand what the agent is supposed to do, in what order, under what
> conditions, and with what expected effects.

SAE's normative core is deliberately small: two layout modes (ordered steps
and unordered statements), a stop-and-report failure default, open-world
conditions, English-phrase procedure binding, and one scenario exception.
Content-kind labels are a recommended vocabulary, not a contract; strictness
lives in profiles.

> This is a design exercise: the specification itself is the artifact. No
> parser, compiler, or executor is planned.

**Heritage.** SAE descends from [Attempto Controlled English 6.7](specs/ace.md)
and its former fork [AIL](specs/ail.md) — both kept in the repo as heritage
and migration references. SAE is a formal break from them, not an extension.

## Repository layout

| Path | Contents |
|------|----------|
| [`specs/`](specs/index.md) | MKF compound node — the authoritative content: `SPEC.md` (spec monolith), `LANGUAGE.md` (SAE reference), `ace.md` (ACE heritage), `ail.md` (AIL migration note), `index.md` (registry), `log.md` (activity log) |
| [`skills/sae/`](skills/sae/SKILL.md) | Agent Skill for writing SAE texts: `SKILL.md` + references (grammar, constructs, worked example, assumptions) |

## Reading order

1. [`specs/SPEC.md`](specs/SPEC.md) — the spec monolith: context, users,
   conformance, decisions.
2. [`specs/LANGUAGE.md`](specs/LANGUAGE.md) — the full SAE reference: blocks
   and modes, numbering and indentation, conditions, repetition, failure
   behavior, procedures, scenarios, style, profiles.
3. [`specs/ace.md`](specs/ace.md) — the ACE 6.7 heritage reference (SAE's
   ancestor, kept for comparison).
4. [`specs/ail.md`](specs/ail.md) — the AIL heritage and migration note, with
   the construct-by-construct mapping onto SAE.

## Status

Draft. The reframing from the ACE / AIL fork to SAE was accepted on
2026-08-14.

## Contributing

See [`AGENTS.md`](AGENTS.md) for the project conventions: MKF frontmatter on
every `specs/` file, every change logged in `specs/log.md`, and atomic
Conventional Commits (`docs(scope): summary`).
