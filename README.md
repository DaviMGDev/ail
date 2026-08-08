# ACE / AIL — Documentation Set

Reference documentation for **Attempto Controlled English (ACE) 6.7** and its
fork **AIL** (Agent Instruction Language).

**ACE** is a controlled natural language developed at the University of Zurich
since 1995: a strict subset of English that is human-readable yet translates
unambiguously into first-order logic. It serves as a knowledge representation,
specification, and query language.

**AIL** is a fork of ACE: a strict superset that keeps ACE fully intact and
adds sequences and procedures for describing agent behaviour. Where ACE is
declarative (a text is an unordered set of sentences), AIL adds control —
ordered steps, branching, loops, and named procedures over an explicit world
model.

> This is a design exercise: the specification itself is the artifact. No
> parser, compiler, or executor is planned.

## Repository layout

| Path | Contents |
|------|----------|
| [`specs/`](specs/index.md) | MKF compound node — the authoritative content: `SPEC.md` (spec monolith), `LANGUAGE.md` (ACE 6.7 base reference), `ail.md` (AIL extension reference), `index.md` (registry), `log.md` (activity log) |
| [`discussions/`](discussions/) | Design discussion snapshots — read for design rationale |
| [`skills/ail/`](skills/ail/SKILL.md) | Agent Skill for writing AIL texts: `SKILL.md` + references (grammar, constructs, worked example, assumptions) |
| `.pi/plans/` | Plan state — committed like any other doc |
| `.pi-subagents/` | Transient agent artifacts — never committed |

## Reading order

1. [`specs/SPEC.md`](specs/SPEC.md) — the spec monolith: context, users,
   conformance, decisions.
2. [`specs/LANGUAGE.md`](specs/LANGUAGE.md) — the full ACE 6.7 syntax and
   practical reference (golden rules, noun/verb phrases, sentences, queries,
   commands, semantics, cheat sheet).
3. [`specs/ail.md`](specs/ail.md) — the AIL extension: superset guarantee,
   world model, control contexts, steps, branching, loops, procedures,
   failure semantics, compatibility annex.

## Status

Draft. The AIL extension is a strict superset of ACE: every valid ACE text is
a valid AIL text; AIL clarifies semantics but never rejects ACE syntax.

## Contributing

See [`AGENTS.md`](AGENTS.md) for the project conventions: MKF frontmatter on
every `specs/` file, every change logged in `specs/log.md`, and atomic
Conventional Commits (`docs(scope): summary`).
