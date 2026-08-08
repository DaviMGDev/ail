---
type: language-reference
title: "ACL (Agent Controlled Language) — Extension Reference"
description: "The ACL extension of ACE 6.7: superset guarantee, world model, control contexts, steps, Otherwise, For every, While, procedures, Stop!, failure semantics, fiat rulings, compatibility annex"
created: "2026-08-08"
updated: "2026-08-08"
---

# ACL (Agent Controlled Language) — Extension Reference

ACL is a fork of [ACE 6.7](LANGUAGE.md) (Attempto Controlled English). It is a **strict superset** of ACE: every valid ACE text is a valid ACL text, and ACL adds the constructs needed to describe **sequences and procedures** — ordered steps, branching, loops, and named procedures over an explicit world model.

ACL is a design exercise: no parser, compiler, or executor is planned. The specification itself is the language definition, so internal consistency is the quality bar. Where ACE is the base, [LANGUAGE.md](LANGUAGE.md) remains authoritative; this document defines only the extension.

Design rationale: `discussions/specs-directory/snapshots/` (esp. `2026-08-08-1706.md`).

## 1. Superset guarantee

- Every valid ACE text is a valid ACL text; ACE content is never modified by this extension.
- **ACL clarifies semantics, but never rejects syntax that ACE accepts.** Where ACE is underspecified, ACL may pin down a reading (see [Fiat rulings](#12-fiat-rulings)) — it may not declare an ACE construction invalid.
- ACL adds semantics where ACE had none: most notably, order of commands (ACE texts are unordered) and a world model (ACE is stateless). These additions are the point of the fork and apply to ACL texts; they do not change what ACE texts *mean*.

## 2. World model

The procedural constructs presume an operational world. The world is:

- a set of **objects** (entities introduced by noun phrases) and
- a set of **facts** about them (expressed by declarative sentences).

Rules:

- The **knowledge** of a text (all declarative sentences outside procedure bodies, in any position) seeds the initial world: objects and facts are in force from the start, regardless of where the sentence appears.
- **Commands** are actions that change the world. What exactly a command changes is the executor's domain semantics; the language does not define effects.
- **Conditions** (in `If`/`While`) read the world. Condition evaluation is **closed-world**: a fact that is not entailed by the current world is false — every condition can always be evaluated.
- **Declarative sentences inside a procedure body are assertions**: they add their objects and facts to the world at the point of execution. This is the ACL-native way to create entities mid-procedure (assert, then refer back with `the`).

## 3. Text structure

An ACL text is a sequence of sentences, with three roles:

| Role | Form | Meaning |
|---|---|---|
| Knowledge | declarative sentences outside procedure bodies | seed the initial world (objects + facts); order irrelevant |
| Main sequence | imperative sentences outside procedure bodies | the steps to perform, in written order |
| Procedures | `Procedure` headers with bodies | named, parameterized step sequences (see [§8](#8-procedures)) |

- **Queries** (`?`) are valid at top level (superset), but are **not steps**: tests appear only in `If`/`While` conditions. The procedure grammar has no interrogative production.
- A text with no imperative sentences is pure ACE — a valid ACL text with an empty main sequence.

## 4. Control contexts and ordering

A **control context** is the main sequence or a procedure body. In a control context, sentences execute **in written order** — this is the only new semantic rule of the language. Everything else is vocabulary and structure.

In a control context, a command **may omit the addressee**; the addressee is the executor (the agent). ACE commands with an explicit addressee (`John, go to your own bank!`) remain valid everywhere.

## 5. Steps

A **step** is one of:

1. a **command** — with explicit addressee (ACE) or implicit (ACL control context): `Insert the card!`
2. a **procedure call** — a procedure name with an argument list in command position: `check-card(the card)!`
3. an **if-otherwise construct** — see [§6](#6-branching-otherwise)

Composition rules:

- The arms of an if-otherwise construct are single steps (commands or calls). **Nested conditionals are not allowed** — express them by calling a procedure.
- The body of a loop is exactly one step (see [§7](#7-loops-for-every-and-while)). For multi-step iteration, call a procedure.
- A step that is a command whose head matches a defined procedure name, followed by an argument list, is a **call**; any other command is an ordinary (world-action) command. Procedure names are hyphenated, so no lexical collision with verbs arises.

## 6. Branching: `Otherwise`

`Otherwise` completes ACE's if-then. It means **the complementary case of the preceding condition** — one word, one meaning, in both contexts:

**Control context** (a step; arms are steps):

> `If the code of the card C is correct then accept the card C! Otherwise reject the card C!`

**Knowledge context** (a total-case rule; both sentences declarative):

> `If a card is valid then the card is accepted. Otherwise the card is rejected.`

Rules:

- `Otherwise` may only **immediately follow** an if-then sentence or another `Otherwise` clause — no steps may intervene. The if-otherwise construct is one unit.
- Chaining gives else-if: `Otherwise if B then ... !` — any number of links, then a final `Otherwise ... !`.
- Expansion (both contexts): `If A then X. Otherwise if B then Y. Otherwise Z.` means `If A then X. If not A and B then Y. If not A and not B then Z.` Each guard conjoins the negations of all earlier conditions; the result is order-independent.
- Punctuation disambiguates the contexts: declarative `.` in knowledge, imperative `!` in control. A bare `Otherwise` with no preceding if-sentence is invalid.

## 7. Loops: `For every` and `While`

Loop body = **exactly one step** (command, call, or if-otherwise construct). Multi-step bodies go through procedures.

**`For every <NP> <step>!`** — iterate over the entities of `<NP>`:

> `For every card in the queue Q: check-card(the card)!`

- The collection is **snapshotted at loop entry**: entities introduced during the loop are not visited. Deterministic, matches the English reading "for every card [that is there now]".

**`While <condition> <step>!`** — repeat while the condition holds:

> `While there is a card in the queue Q: remove a card from the queue Q!`

- The condition is **re-evaluated before each pass**; existential noun phrases in the condition introduce a **fresh entity each evaluation**, and the body's anaphora binds to that pass's witnesses.
- When several entities match, the choice is **non-deterministic**; procedures must not depend on which one matched.
- `While` is live (unlike `For every`): the world is re-read every pass. Termination is the author's responsibility — the language defines no effects, so it cannot guarantee that a body changes the world.

## 8. Procedures

**Definition** — a header line, then the body:

```
Procedure check-card(Card C):
  Check the code of the card C!
  If the code of the card C is correct then accept the card C! Otherwise reject the card C!
```

- **Name**: a hyphenated content word (`check-card`). Hyphenation is mandatory — it is what keeps calls distinct from world-action commands.
- **Parameters**: ACE apposition variables, typed by a noun phrase (`Card C`). The type annotation is a **constraint**: a call whose argument is not of that class makes the text invalid.
- **Body**: steps, one per line, indented by at least one space relative to the header; the body ends at the first non-indented line (or the next `Procedure` header, or end of text). Indentation is the body delimiter.
- **Namespace**: flat and global. Nested definitions and redefinition of a name are invalid.
- **Recursion is allowed** (each call is a fresh activation with the argument bound to the parameter); non-termination is the author's error.

**Call** — the name with an argument list, in command position:

> `check-card(the card)!` · `check-card(C)!` · `check-card(a card)!`

- Arguments may be any **entity-denoting** noun phrase: definite (`the card` — must have an accessible antecedent), indefinite (`a card` — introduces a fresh entity that remains accessible after the call), proper name, or variable.
- **Quantified and coordinated arguments are invalid** (`every card`, `the card and the receipt`) — one argument slot denotes one entity; iteration is `For every`, not argument smuggling.
- During the call, the parameter variable denotes the argument's referent. Inside the body, anaphora follows ACE's most-recent-antecedent rule, with the argument as the most recent entity at call entry.
- A call is a step: after it returns, execution continues with the next step.

## 9. `Stop!`

`Stop!` terminates the **current procedure** (early return); in the main sequence it ends the run. It is a reserved word in its bare, addressee-less, imperative form. To tell the executor to halt an action, use an ordinary command instead (`Stop acting!`, or an explicit addressee). A `Stop!` after the last step is harmless but redundant.

## 10. Sequence markers

`First`, `Next`, `Then`, `Finally` are optional sentence-initial markers for readability. Order is line order regardless; markers never change semantics:

> `First check the code of the card! Then accept the card!`

## 11. Failure semantics

- Conditions always evaluate (closed world) — there is no "unevaluatable".
- A step that **cannot be performed** aborts the whole run at that point. Impossible steps are: a command or branch referring to an entity with no accessible antecedent, a call to an undefined procedure, or a call with a type-mismatched argument.
- There is no recovery: no rollback, no try/catch, no `Otherwise`-on-failure. Side effects performed before the failing step persist. (Failure *handling* is the natural add-on if ACL ever gains an executor — deliberately out of scope.)

## 12. Fiat rulings

Where ACE is underspecified, ACL pins down readings (clarification only — never rejection, per [§1](#1-superset-guarantee)):

- `some` occurs with **plural and mass nouns only** (`some cards`, `some water`); the singular indefinite is `a`.
- **Superlative adjectives take `the`** (`the richest customer`); comparatives take any determiner (`a richer customer`).
- Keywords are reserved **only in their defined positions**: sentence-initial `Otherwise` immediately after an if-sentence; `Procedure` at the start of a definition header; `For every` / `While` opening a loop; bare `Stop!`; sentence-initial `First`/`Next`/`Then`/`Finally`. In any other position these remain ordinary words.
- `:` in a procedure header is a semantic token (body delimiter); indentation is the body delimiter inside procedures.

## 13. Worked example

```
Every card has a code.
If the code of a card is correct then the card is valid.
If a card is valid then the card is accepted. Otherwise the card is rejected.

Procedure check-card(Card C):
  Check the code of the card C!
  If the code of the card C is correct then accept the card C! Otherwise reject the card C!

Procedure process-queue(Queue Q):
  For every card in the queue Q: check-card(the card)!
  While there is a card in the queue Q: remove a card from the queue Q!
```

The first three lines are knowledge (a total-case rule among them). The two `Procedure` headers start control contexts. The main sequence is empty — a text may consist of knowledge and procedures only, or include top-level steps:

```
A card is in the queue Q.
First check-card(the card)!
If the card is valid then accept the card! Otherwise reject the card!
```

## 14. Compatibility annex

- **Guarantee:** every valid ACE 6.7 text is a valid ACL text. If a construction is accepted by ACE (per the official Construction Rules), ACL accepts it.
- **Clarification:** where the official rules are silent or ambiguous, ACL's rulings ([§12](#12-fiat-rulings)) apply to the ACL reading of a text.
- **Conformance corpus:** the examples marked * in [LANGUAGE.md](LANGUAGE.md) (counterexamples) and the examples in this document form a working corpus; any ACE-valid example from the official documentation is admissible as a conformance test. A dedicated corpus file may be added to `specs/` later.
- **Divergence:** this annex records the only intentional divergence from ACE — the addition of ordering and world-model semantics in control contexts ([§2](#2-world-model), [§4](#4-control-contexts-and-ordering)). Nothing in ACE is rejected.

## 15. Deliberately omitted

Kept out of the language, with reasons (all are expressible via the six constructs or out of scope):

- **Return values / value-returning procedures** — procedures are named sequences; tests happen via branching, mid-run values via assertion + anaphora.
- **Assignment / mutable variables** — replaced by the world model: declarative steps assert, `the` refers back.
- **Loop break** — restructure with `While` + conditions.
- **`Wait until`** — expressible as `While` over a negated condition; clunky by design, not worth a construct.
- **Concurrency, timing, events, interrupts** — a different paradigm; not claimed by "sequences/procedures".
- **Recovery constructs** — see [§11](#11-failure-semantics).
