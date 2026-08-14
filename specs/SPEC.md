---
type: spec
title: "SAE — Specification"
description: "Spec monolith for Structured Agent English (SAE), a readability-first controlled English for agent instructions: context, users, conformance, and decisions; the language content lives in the citizen files LANGUAGE.md (SAE reference), ace.md (heritage), and ail.md (migration note)"
tags: [spec, controlled-natural-language, sae]
created: "2026-08-08"
updated: "2026-08-14"
sections: [context, users, conformance, decisions]
---

# SAE — Specification

## Context

Structured Agent English (SAE) is a controlled subset of English for writing agent instructions. Its primary design goal: a person who reads a SAE text for the first time should be able to understand what the agent is supposed to do, in what order, under what conditions, and with what expected effects — without access to the formal specification.

SAE is therefore optimized for readable, disciplined English, not for the smallest grammar. Its normative core is deliberately small: exactly two semantic modes carried by visible layout — **ordered steps** (numbered lists, resumptive) and **unordered statements** (knowledge) — plus one safe failure default (stop and report), open-world tri-state conditions, English-phrase procedure binding, and one narrow exception (an explicit `Expected results:` section in a scenario is verified). Content-kind labels (Facts, Rules, Actions, Tasks, Scenarios) are a recommended vocabulary, not a contract; strictness lives in **profiles**. The full language reference is [LANGUAGE.md](LANGUAGE.md).

SAE is a design exercise: no parser, compiler, or executor is planned — the specification itself is the language definition, so internal consistency is the quality bar.

**Heritage.** SAE descends from Attempto Controlled English 6.7 ([ace.md](ace.md), kept as a heritage reference) and its former fork AIL ([ail.md](ail.md), kept as a migration note). SAE is a **formal break** from both: it abandons ACE's formal machinery (punctuation-as-semantics, determiner grammar, hyphenation, anaphora rules) and retires the ACE superset guarantee. The reframing decision record is `.pi/discussions/sae-reframing/` (proposal v1, accepted 2026-08-14).

## Users

- **Authors of agent instruction texts** — prompt engineers, skill authors, automation designers writing what an agent should do, in what order, under what conditions.
- **Readers and reviewers** — anyone who must understand an instruction text without prior training; SAE's readability contract is written for them.
- **Executors** — language-understanding agents (typically LLMs) that carry out the texts; the reader's understanding of the surface English is the canonical semantics.
- **Profile authors** — people who need determinism beyond the base language: pinned labels, exact invocation matching, closed-world conditions, tightened failure defaults.

## Conformance

Conformance of a SAE text is judged against [LANGUAGE.md](LANGUAGE.md); there is no parser, so the rules are structural and readable. Acceptance criteria (EARS):

- **WHEN** a text contains numbered lists, **THE** numbered lines SHALL be the ordered flow and **SHALL** execute in written order.
- **WHEN** a numbered list resumes after an interruption, **THE** list SHALL continue while its numbers increase; a list restarting at `1.` SHALL open a new flow.
- **WHEN** a line is indented under a step, **THE** line SHALL belong to that step's flow; an indented declarative SHALL be an assertion performed at that point; a top-level unnumbered line SHALL be knowledge.
- **WHEN** a `For each` loop starts, **THE** iterated collection SHALL be fixed at loop entry; **WHEN** a `While` loop repeats, **THE** condition SHALL be re-evaluated before each pass.
- **WHEN** a step fails and no failure clause applies, **THE** agent SHALL stop and report (plain English to the issuing channel: failed step and observed condition); failure clauses SHALL read as deltas on that default, in the order: step-local override, standing failure rules, default.
- **WHEN** a condition cannot be determined, **THE** step SHALL fail rather than take a branch; closed-world evaluation SHALL require a declared profile.
- **WHEN** a step's action phrase matches a `To`-title by ordinary-English understanding, **THE** procedure's steps SHALL be followed at that point; an invocation matching no title SHALL be an ordinary action.
- **WHEN** a scenario block contains an explicit `Expected results:` section, **THE** expectations SHALL be verified after the task steps; a false or unverifiable expectation SHALL be a failed outcome reported as expected versus actual.
- **WHEN** a text uses labels outside the recommended vocabulary, **THE** labels SHALL be inert; only a declared profile SHALL pin them.

## Decisions

- The repository's language was reframed from the ACE / AIL fork to SAE; the reframing proposal was accepted 2026-08-14 with recommended defaults: name SAE, formal break with ACE (kept as heritage), and the scenario verification exception kept. Record: `.pi/discussions/sae-reframing/`. (2026-08-14)
- The normative core is two layout modes, not five content kinds: the kinds are a recommended, non-contractual label vocabulary. (2026-08-14)
- Failure defaults to stop-and-report with a three-layer cascade; outcomes stay ordinary English. (2026-08-14)
- Conditions are open-world tri-state; an undecidable condition fails the step; closed world is a profile opt-in — reversing AIL's closed-world default. (2026-08-14)
- `For each` snapshots at loop entry; `While` is the live construct. (2026-08-14)
- Procedures are `To`-titled blocks invoked by English-phrase binding; unmatched invocations are ordinary actions. (2026-08-14)
- SPEC.md follows the v4 spec-md contract — the frontmatter `sections:` list is the contract and the body matches it exactly. (2026-08-08)
- SPEC.md stays light; the language reference is the primary artifact of this directory. (2026-08-08)
