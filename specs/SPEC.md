---
type: spec
title: "ACE (Attempto Controlled English) — Specification"
description: "Spec monolith for the ACE language documentation set: context, scope, and pointers into LANGUAGE.md"
tags: [spec, controlled-natural-language, ace]
created: "2026-08-08"
updated: "2026-08-08"
---

# ACE (Attempto Controlled English) — Specification

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

This `specs/` directory documents the **syntax and practical usage of ACE** — not a software system. The full syntax reference lives in [LANGUAGE.md](LANGUAGE.md); SPEC.md is deliberately light.

## Users

- Knowledge engineers and ontologists writing OWL/SWRL content via ACE
- Specifiers who want formal, unambiguous requirements without learning logic notation
- Anyone reading or writing ACE texts (queries, rules, domain descriptions)

## User Stories

Story: [US-001] — Read and write valid ACE

As a knowledge engineer,
I want a precise reference of ACE construction and interpretation rules,
so that I can write texts that parse unambiguously with the APE parser.

Acceptance criteria (EARS — 5 patterns in the spec-md skill, `references/ears-quickref.md`):

- The language reference SHALL document noun phrases, verb phrases, and sentence forms with valid examples.
- The language reference SHALL document the golden rules (determiner requirement, tense restriction, hyphenation, punctuation).

## Architecture

Not applicable — this `specs/` documents a language, not a system. Internal structure: SPEC.md (this monolith) → LANGUAGE.md (syntax reference) → index.md (registry) → log.md (activity log).

## Decisions

- The syntax content is a single citizen file, LANGUAGE.md, rather than sections inside SPEC.md — the language reference is the primary artifact of this directory. (2026-08-08)
- SPEC.md stays light; most checklist sections are marked not-applicable rather than fabricated. (2026-08-08)

## Stack

Not applicable — the documented subject is a natural-language grammar, not software. The reference implementation of ACE is the Attempto Parsing Engine (APE); see LANGUAGE.md → Tools.

## Ops

Not applicable — no infrastructure or deployment for a documentation-only directory.

## API

The "API" of this documentation set is the ACE language itself. Its contract is described in natural language with examples in [LANGUAGE.md](LANGUAGE.md); the authoritative external contract is the official ACE 6.7 Construction Rules (attempto.ifi.uzh.ch).
