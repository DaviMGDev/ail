---
type: spec
title: "ACE / AIL — Specification"
description: "Spec monolith for the ACE language documentation set and its fork AIL (Agent Instruction Language): context, scope, and pointers into LANGUAGE.md and ail.md"
tags: [spec, controlled-natural-language, ace, ail]
created: "2026-08-08"
updated: "2026-08-08"
---

# ACE / AIL — Specification

## Must contain

- Context: problem statement, goals, stakeholders
- Users: personas or user groups
- User Stories: at least one story per persona, each with EARS acceptance criteria
- Architecture: data models, auth, key flows
- Decisions: choices with trade-offs recorded (or "none yet")
- Stack: languages/frameworks, dependencies, testing tiers
- Ops: infrastructure, deployment, NFRs, security
- API: contract in natural language + code blocks (or linked file)
- `index.md` registry lists every file in `specs/`
- All `[placeholders]` replaced with concrete content

---

## Context

Attempto Controlled English (ACE) is a controlled natural language developed at the University of Zurich since 1995 (current version 6.7). It is a strict subset of English that is human-readable yet translates unambiguously into first-order logic, serving as a knowledge representation, specification, and query language.

**AIL (Agent Instruction Language)** is a fork of ACE: a strict superset that keeps ACE fully intact and adds sequences and procedures for describing agent behaviour. Where ACE is declarative (a text is an unordered set of sentences), AIL adds control: ordered steps, branching, loops, and named procedures, over an explicit world model. AIL is a design exercise — the specification is the artifact; no parser or tooling is planned. The ACE base reference lives in [LANGUAGE.md](LANGUAGE.md); the AIL extension reference lives in [ail.md](ail.md).

Design context: the full decision record for AIL is captured in `discussions/specs-directory/snapshots/` (see esp. `2026-08-08-1706.md`).

## Users

- Knowledge engineers and ontologists writing OWL/SWRL content via ACE
- Specifiers who want formal, unambiguous requirements without learning logic notation
- Anyone reading or writing ACE texts (queries, rules, domain descriptions)
- Authors of AIL texts: people describing agent behaviour as sequences/procedures (knowledge section + control section)

## User Stories

Story: [US-001] — Read and write valid ACE

As a knowledge engineer,
I want a precise reference of ACE construction and interpretation rules,
so that I can write texts that parse unambiguously with the APE parser.

Acceptance criteria (EARS — 5 patterns in the spec-md skill, `references/ears-quickref.md`):

- The language reference SHALL document noun phrases, verb phrases, and sentence forms with valid examples.
- The language reference SHALL document the golden rules (determiner requirement, tense restriction, hyphenation, punctuation).

Story: [US-002] — Write AIL procedures

As an author of AIL texts,
I want a precise reference of the AIL extension constructs,
so that I can write sequences and procedures that describe agent behaviour unambiguously.

Acceptance criteria (EARS):

- The AIL reference SHALL define control contexts (main sequence, procedure bodies) and their ordering semantics.
- The AIL reference SHALL define the world model (objects, facts, closed-world condition evaluation).
- The AIL reference SHALL define the extension constructs: implicit-addressee commands, `Otherwise`, `For every`, `While`, `Procedure`/calls, `Stop!` — with examples.
- The AIL reference SHALL state the superset guarantee: every valid ACE text is a valid AIL text, and AIL clarifies semantics but never rejects ACE syntax.

## Architecture

Not applicable — this `specs/` documents languages, not a system. Internal structure: SPEC.md (this monolith) → [LANGUAGE.md](LANGUAGE.md) (ACE 6.7 base reference) → [ail.md](ail.md) (AIL extension reference) → index.md (registry) → log.md (activity log).

## Decisions

- The syntax content is a single citizen file, LANGUAGE.md, rather than sections inside SPEC.md — the language reference is the primary artifact of this directory. (2026-08-08)
- SPEC.md stays light; most checklist sections are marked not-applicable rather than fabricated. (2026-08-08)
- AIL is a fork of ACE defined as a strict superset: every valid ACE text remains a valid AIL text; the ACE base reference stays untouched and authoritative for the base language. (2026-08-08)
- The AIL extension lives in its own citizen file, ail.md, rather than inside LANGUAGE.md — one concern per file: the base language vs. the extension. (2026-08-08)
- AIL is a design exercise: no parser, compiler, or executor is planned; the specification itself is the language definition, so internal consistency is the quality bar. (2026-08-08)
- The AIL extension set is deliberately minimal: order (the only new semantic rule), an explicit world model, implicit-addressee commands, `Otherwise`, `For every`, `While`, `Procedure`/calls, and `Stop!`. Full rationale in the design snapshots. (2026-08-08)

## Stack

Not applicable — the documented subject is natural-language grammars, not software. The reference implementation of the ACE base is the Attempto Parsing Engine (APE); see LANGUAGE.md → Tools. AIL has no implementation by design.

## Ops

Not applicable — no infrastructure or deployment for a documentation-only directory.

## API

The "API" of this documentation set is the two languages themselves: the ACE base and the AIL extension. Their contracts are described in natural language with examples in [LANGUAGE.md](LANGUAGE.md) and [ail.md](ail.md); the authoritative external contract for the ACE base is the official ACE 6.7 Construction Rules (attempto.ifi.uzh.ch). AIL adds the superset guarantee: AIL clarifies readings of the base where ACE is underspecified, but never rejects syntax that ACE accepts (see ail.md → Compatibility).
