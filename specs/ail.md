---
type: language-reference
title: "AIL — Heritage and Migration Note"
description: "What AIL (Agent Instruction Language) was, and how each of its constructs maps onto Structured Agent English (SAE) after the 2026-08-14 reframing"
created: "2026-08-08"
updated: "2026-08-14"
---

# AIL — Heritage and Migration Note

> **Retired.** AIL (Agent Instruction Language) was a fork of ACE 6.7 — a strict superset adding sequences and procedures over an explicit world model. On 2026-08-14 the repository reframed its language as **Structured Agent English (SAE)** (see [LANGUAGE.md](LANGUAGE.md)); the reframing proposal was accepted. This file preserves what AIL was and maps every AIL construct onto SAE. The former full extension reference is superseded.

## What AIL was

AIL's defining properties:

- **Strict superset of ACE 6.7** — every valid ACE text was a valid AIL text; AIL clarified semantics but never rejected ACE syntax.
- **Three text roles** — knowledge (declarative sentences outside procedure bodies, in any position), a main sequence (imperatives in written order), and procedures (named, parameterized step sequences).
- **A world model** — objects and facts; commands change the world; conditions read it, evaluated closed-world.
- **Six constructs** — implicit-addressee commands, `Otherwise`, `For every`, `While`, `Procedure`/calls, `Stop!` — plus explicit failure semantics (an impossible step aborts the run; no recovery) and fiat rulings where ACE was underspecified.

## Why SAE replaced it

The reframing was driven by a readability goal AIL could not meet: a first-time reader should understand what the agent does, in what order, under what conditions, with what effects — without reading the specification. AIL inherited ACE's formal machinery (determiner grammar, punctuation-as-semantics, hyphenation, anaphora rules), which makes texts unreadable without training. SAE keeps AIL's procedural ideas and drops the machinery; the superset guarantee toward ACE is retired along with it ([ace.md](ace.md) stays as heritage).

## Construct mapping

| AIL construct | SAE equivalent |
|---|---|
| Knowledge section (declaratives, any position) | unordered statements — unnumbered top-level lines are knowledge, anywhere ([LANGUAGE.md §2](LANGUAGE.md#2-blocks-and-modes)) |
| Main sequence (imperatives in written order) | numbered lists — ordered flow, resumptive ([§2](LANGUAGE.md#2-blocks-and-modes)) |
| `Procedure check-card(Card C):` + indented body | `To check a card:` title + numbered body; parameter slots are the title's indefinite noun phrases, bound by the invocation ([§10](LANGUAGE.md#10-procedures)) |
| Call `check-card(the card)!` | ordinary-English invocation: `the agent checks the card` ([§10](LANGUAGE.md#10-procedures)) |
| `If A then X! Otherwise Y!` | `If A:` / `Otherwise:` paired by indentation and adjacency — `Otherwise` is ordinary English ([§6](LANGUAGE.md#6-conditions)) |
| `For every card in the queue Q: ...` | `For each card in the queue Q: ...` — snapshot at entry, same as AIL ([§7](LANGUAGE.md#7-repetition)) |
| `While there is a card ...: ...` | `While ...` — live re-evaluation per pass, same as AIL ([§7](LANGUAGE.md#7-repetition)) |
| `Stop!` | the failure default: stop and report — no reserved word ([§8](LANGUAGE.md#8-failure-behavior)) |
| Closed-world conditions | open-world tri-state — an undecidable condition makes the step fail; closed world is a profile opt-in ([§6](LANGUAGE.md#6-conditions)) |
| "An impossible step aborts the run" | the three-layer failure cascade, default stop-and-report ([§8](LANGUAGE.md#8-failure-behavior)) |
| Fiat rulings (some/superlatives/keyword positions) | obsolete — no determiner grammar, no reserved keywords |
| Sequence markers `First`/`Next`/`Then`/`Finally` | obsolete — numbering shows order |

## What survives unchanged in spirit

- **Written order is the only ordering rule** — now carried by numbering instead of punctuation.
- **Assertions at the point of execution** — AIL's declaratives-in-procedure-bodies became SAE's indented declaratives (the two-axis rule, [§2](LANGUAGE.md#2-blocks-and-modes)).
- **Loops with complementary jobs** — `For each` fixed, `While` live.
- **Termination is the author's responsibility** — no effects are defined, so no loop can be guaranteed to terminate.
- **A design exercise** — no parser, compiler, or executor; the specification is the artifact.
