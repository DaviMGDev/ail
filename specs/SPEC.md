---
type: spec
title: "ACE / AIL — Specification"
description: "Spec monolith for the ACE language documentation set and its fork AIL (Agent Instruction Language): context, users, conformance, and decisions; the language content lives in the citizen files LANGUAGE.md and ail.md"
tags: [spec, controlled-natural-language, ace, ail]
created: "2026-08-08"
updated: "2026-08-08"
sections: [context, users, conformance, decisions]
---

# ACE / AIL — Specification

## Context

Attempto Controlled English (ACE) is a controlled natural language developed at the University of Zurich since 1995 (current version 6.7). It is a strict subset of English that is human-readable yet translates unambiguously into first-order logic, serving as a knowledge representation, specification, and query language.

**AIL (Agent Instruction Language)** is a fork of ACE: a strict superset that keeps ACE fully intact and adds sequences and procedures for describing agent behaviour. Where ACE is declarative (a text is an unordered set of sentences), AIL adds control: ordered steps, branching, loops, and named procedures, over an explicit world model. AIL is a design exercise — the specification is the artifact; no parser or tooling is planned. The ACE base reference lives in [LANGUAGE.md](LANGUAGE.md); the AIL extension reference lives in [ail.md](ail.md).

Design context: the full decision record for AIL is captured in `discussions/specs-directory/snapshots/` (see esp. `2026-08-08-1706.md`).

## Users

- Knowledge engineers and ontologists writing OWL/SWRL content via ACE
- Specifiers who want formal, unambiguous requirements without learning logic notation
- Readers and writers of ACE texts (queries, rules, domain descriptions)
- Authors of AIL texts: people describing agent behaviour as sequences/procedures (knowledge section + control section)

## Conformance

The conformance contract of this specification set has two levels:

- **ACE base** — conformance is defined by the official ACE 6.7 Construction Rules (attempto.ifi.uzh.ch), the authoritative external contract; [LANGUAGE.md](LANGUAGE.md) is the in-repo reference that documents what makes a text valid ACE.
- **AIL extension** — conformance is the superset guarantee: every valid ACE text SHALL also be a valid AIL text; AIL SHALL clarify readings where ACE is underspecified, but SHALL never reject syntax that ACE accepts. The compatibility annex in [ail.md](ail.md) → Compatibility verifies this per construct.

Acceptance criteria (EARS):

- The ACE base reference SHALL document noun phrases, verb phrases, and sentence forms with valid examples.
- The ACE base reference SHALL document the golden rules (determiner requirement, tense restriction, hyphenation, punctuation).
- The AIL reference SHALL define control contexts (main sequence, procedure bodies) and their ordering semantics.
- The AIL reference SHALL define the world model (objects, facts, closed-world condition evaluation).
- The AIL reference SHALL define the extension constructs — implicit-addressee commands, `Otherwise`, `For every`, `While`, `Procedure`/calls, `Stop!` — with examples.
- The AIL reference SHALL state the superset guarantee: every valid ACE text is a valid AIL text, and AIL clarifies semantics but never rejects ACE syntax.

## Decisions

- The syntax content is a single citizen file, LANGUAGE.md, rather than sections inside SPEC.md — the language reference is the primary artifact of this directory. (2026-08-08)
- SPEC.md stays light; most checklist sections are marked not-applicable rather than fabricated. (2026-08-08)
- AIL is a fork of ACE defined as a strict superset: every valid ACE text remains a valid AIL text; the ACE base reference stays untouched and authoritative for the base language. (2026-08-08)
- The AIL extension lives in its own citizen file, ail.md, rather than inside LANGUAGE.md — one concern per file: the base language vs. the extension. (2026-08-08)
- AIL is a design exercise: no parser, compiler, or executor is planned; the specification itself is the language definition, so internal consistency is the quality bar. (2026-08-08)
- The AIL extension set is deliberately minimal: order (the only new semantic rule), an explicit world model, implicit-addressee commands, `Otherwise`, `For every`, `While`, `Procedure`/calls, and `Stop!`. Full rationale in the design snapshots. (2026-08-08)
- SPEC.md follows the v4 spec-md contract — the frontmatter `sections:` list is the contract and the body matches it exactly: enforced-only template sections (architecture, stack, ops, api) were dropped rather than declared "not applicable", and the user-stories + api content was reworked into conformance. (2026-08-08)
