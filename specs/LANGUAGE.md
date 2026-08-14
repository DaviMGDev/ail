---
type: language-reference
title: "SAE — Structured Agent English Reference"
description: "The SAE language reference: two layout modes, block model, conditions, repetition, failure behavior, procedures, scenarios, style, profiles"
created: "2026-08-08"
updated: "2026-08-14"
---

# Structured Agent English (SAE)

Structured Agent English (SAE) is a controlled subset of English for writing agent instructions that remain understandable to an ordinary reader even without access to this specification.

SAE has one primary design goal:

> A person who reads a SAE text for the first time should be able to understand what the agent is supposed to do, in what order, under what conditions, and with what expected effects.

SAE is therefore not optimized for the smallest grammar or the most compact formal notation. It is optimized for readable, disciplined English that can later receive precise semantics. SAE is a design exercise: no parser, compiler, or executor is planned. The specification itself is the language definition, so internal consistency is the quality bar.

**Heritage.** SAE's ancestry is Attempto Controlled English 6.7 (see [ace.md](ace.md)) and its former fork AIL (see [ail.md](ail.md)). SAE is **not** an extension of either: it deliberately abandons ACE's formal machinery (punctuation-as-semantics, determiner grammar, hyphenation, anaphora rules) in favor of disciplined ordinary English. The migration from AIL is mapped in [ail.md](ail.md).

## 1. Design principles

A SAE text should read as ordinary technical English.

- Every construct should explain itself through normal English wording.
- Headings should reveal the role of a block without requiring prior training.
- Order should be shown by numbering and layout, not by hidden punctuation rules.
- Conditions should be written with ordinary `If` clauses.
- Repetition should be written with ordinary phrases such as `For each` and `While`.
- Failure behavior should be stated explicitly, with a safe default when it is not.
- Important state changes should be stated in English, not hidden behind a verb name.

## 2. Blocks and modes

A SAE text is a **free sequence of blocks**. No block kind is required, ordered, or unique: a text may contain any blocks in any order, several of the same kind, or none of them. A block's kind is carried by its own heading or by its layout — never by a document skeleton.

Exactly **two modes** carry semantics. Everything else is labeling:

| Mode | Form | Meaning |
|---|---|---|
| Ordered steps | numbered lists | the flow to execute, in written order |
| Unordered statements | everything unnumbered at top level | knowledge: facts, rules, definitions — order-free |

A top-level line that is not numbered is knowledge, wherever it appears. To make the agent act, give the line a number.

**Resumptive numbering.** A numbered list continues as long as its numbers increase. An unnumbered line between steps is inert knowledge; the list resumes around it. A list that restarts at `1.` opens a new flow.

```text
1. The agent opens the inbox.
2. The agent reads each ticket.

Facts:
- Ticket T-14 is open.

3. The agent closes the inbox.
```

Steps `1.`–`3.` form one flow; the `Facts:` block sits inside it as knowledge.

**Two-axis rule.** Numbering gives order; indentation gives flow membership. Lines indented under a step belong to that step: the consequences of an `If`, the body of a `For each` or `While`, or lettered substeps (`a.`, `b.`, `c.`). An indented declarative sentence is an **assertion** — a state change performed at that point of execution. A top-level declarative is knowledge; an indented one is an effect.

```text
2. If the code is correct:
   the card is valid.
```

`the card is valid.` is an assertion inside step 2's flow: when the condition holds, the card *becomes* valid.

### Recommended labels

The draft vocabulary of content kinds is a **recommended labeling convention, not a contract**. Authors use these English headings because they orient the reader; the language promises nothing about them beyond the two modes. A profile may pin specific labels if it wants to.

- `Facts:` — what exists and what is true.
- `Rules:` — what must hold when certain conditions hold.
- `Actions:` — what a named action means, including effects and failure conditions.
- `Task:` / `Tasks:` — ordered instructions.
- `Scenario:` / `Scenarios:` — examples or tests of expected behavior.
- `Purpose:` — why the text exists.
- `Starting facts:` — the initial world of a scenario.
- `Expected results:` — what must hold afterwards. **Normative exception:** inside a Scenario block, an explicit `Expected results:` section is verified after the task steps; see [§11 Scenarios](#11-scenarios).
- `Failure behavior:` — standing failure rules; see [§8 Failure behavior](#8-failure-behavior).

Unrecognized headings are inert English. A short prompt may be nothing but a numbered list.

## 3. Facts and rules

Facts and rules are unordered statements — knowledge. The distinction is didactic, not semantic: facts are ground statements, rules are conditionals. Both may appear anywhere, in any order, any number of times.

```text
Facts:

- Every ticket has a title.
- Every ticket has a status.
- A ticket is either open or closed.
- Ticket T-14 is open.

Rules:

- If a ticket mentions a security problem, the ticket has critical priority.
- If a ticket is closed, the ticket has a resolution.
- No ticket is both open and closed.
```

A rule may be a single sentence or a block:

```text
If a ticket is closed, the ticket has a resolution.
```

```text
If a ticket is closed:
  the ticket has a resolution.
```

## 4. Actions

An action definition explains what a named action means. This matters because verbs such as `accept`, `classify`, `save`, or `escalate` often hide crucial effects. Action definitions are knowledge — unordered statements — conventionally gathered under an `Actions:` label.

```text
Actions:

Action: Accept a card.

- The agent may accept a card only if the card is valid.
- When the agent accepts a card:
  - the card becomes accepted;
  - the card becomes not rejected;
  - the system records the acceptance.
- If the card is not valid, the action fails.
```

Recommended parts: name, preconditions, effects, failure conditions, optional outputs. A more explicit format is also fine:

```text
Action: Save a ticket.

Preconditions:
- The ticket exists.

Effects:
- The system stores the latest version of the ticket.
- The ticket becomes saved.

Failure conditions:
- If the storage service is unavailable, the action fails.
```

## 5. Tasks

A task is ordered instructions: a numbered flow, conventionally introduced by a `Task:` heading with a title. The order of execution is the written order of numbered steps and nested substeps.

```text
Task: Process every open ticket.

1. The agent finds every ticket whose status is open.
2. For each open ticket:
   a. The agent reads the ticket.
   b. If the ticket mentions a security problem:
      the agent assigns critical priority.
   c. If the ticket does not mention a security problem:
      the agent assigns priority according to the priority rules.
   d. The agent saves the ticket.
3. The agent reports the number of processed tickets.
```

A step may contain: a plain action sentence; a conditional block; a repetition block; a nested lettered substep sequence. Whether two separated flows are "the same task" is not a semantic notion — each numbered flow is its own ordered unit, and a `Task:` label is annotation.

## 6. Conditions

Conditions are written with ordinary `If` clauses.

Inline form:

```text
If the card is valid, the agent accepts the card.
```

Block form:

```text
If the card is valid:
  the agent accepts the card.
```

The explicit negative form is preferred when clarity matters:

```text
If the card is not valid:
  the agent rejects the card.
```

### `Otherwise`

`Otherwise` is ordinary English, not a reserved keyword. The two-axis rule does the pairing: an `Otherwise:` line at the same indentation as its `If`, immediately following it, pairs with that `If` and means the complementary case.

```text
If the card is valid:
  the agent accepts the card.
Otherwise:
  the agent rejects the card.
```

Chains are possible — `Otherwise, if ...` — but stacked alternatives deserve explicit conditions or a new numbered flow.

### Evaluation

Conditions are evaluated **open-world**, as a tri-state:

- a condition the agent knows to be true takes its branch;
- a condition the agent knows to be false takes the complementary branch;
- a condition the agent **cannot determine** (unknown entity, missing fact) makes the step **fail**, which rides the failure behavior of [§8](#8-failure-behavior).

Uncertainty never silently resolves to a branch. Authors may override in plain English ("If you cannot determine whether C, continue as though C is false."). A profile may opt into closed-world evaluation where a domain genuinely guarantees complete knowledge.

## 7. Repetition

### `For each`

`For each` iterates over a known collection or selected set. The collection is **fixed when the loop starts** — a snapshot at entry: entities introduced or changed by the body do not alter the iteration.

```text
For each open ticket:
  the agent reads the ticket.
```

When precision matters, bind a named entity:

```text
For each ticket T whose status is open:
  the agent reads ticket T.
```

When the author wants to pin a collection across several loops, or to freeze it at a moment other than loop entry, the snapshot becomes an explicit, communicative step:

```text
The agent takes a snapshot of the open tickets.
For each ticket T in that snapshot:
  the agent reads ticket T.
```

### `While`

`While` is the live construct: the condition is re-evaluated before each pass.

```text
While the queue is not empty:
  the agent removes one card from the queue.
```

Termination is the author's responsibility — the language defines no effects, so it cannot guarantee that a body changes the world. Termination conditions should be obvious from the text; if they are not obvious, state them explicitly.

## 8. Failure behavior

When a step fails and nothing is written about it, the default applies: **the agent stops and reports**. A report is a plain-English report to the issuing channel, stating the failed step and the observed condition. This default is what an ordinary reader already assumes — a subordinate asked to do a thing who cannot do it comes back and says so.

Failure clauses read as **deltas on that baseline**, in a three-layer cascade:

1. an indented `If ... fails:` override attached to the step;
2. any applicable standing failure rules (top-level conditional knowledge, conventionally under a `Failure behavior:` label);
3. the default: stop and report.

```text
Failure behavior:

- If the agent cannot read the card, the agent reports "unreadable card" and stops.
- If the agent cannot save a ticket, the agent retries once.
- If the retry fails, the agent reports the failure and continues with the next ticket.
```

A local clause overrides per step:

```text
2. The agent saves the ticket.
   If saving fails:
   a. the agent retries once.
   b. If the retry fails:
      the agent reports the ticket and continues with the next ticket.
```

After the override's retry fails, everything the override did not mention falls back to the default: stop and report.

Failure outcomes — `stop`, `retry`, `continue`, `report`, `escalate` — are ordinary English, not a pinned vocabulary. Precision lives in the surrounding sentences ("retries once", "escalates to the billing team"). A bare "retries" means the agent retries some number of times and then the default applies. A profile may tighten any of this.

## 9. State changes

When an action changes the world in an important way, the change should be stated explicitly. Inside a flow, declarative statements are assertions — they make the world match the sentence at that point.

Preferred forms:

```text
As a result, the ticket becomes closed.
As a result, the card is accepted.
As a result, the queue no longer contains the card.
```

This avoids hiding important semantics inside a single verb.

## 10. Procedures

A reusable task is introduced with a `To ...` title and a numbered body:

```text
To validate a card:

1. The agent reads the code on the card.
2. If the code is correct:
   the card is valid.
3. If the code is not correct:
   the card is invalid.
```

A `To`-block is top-level knowledge — globally visible, executed only when invoked.

**Invocation binds by ordinary-English understanding.** When a step says the agent does what a procedure's title describes, with the title's subjects and objects supplied, that procedure's steps are followed at that point. Matching is at the linguistic level, not the string level: `To validate a card` is invoked by `the agent validates the card`, in any voice.

```text
Task: Process the queue.

1. For each card in the queue:
   the agent validates the card.
```

**Parameters.** Indefinite noun phrases in the title are parameter slots, filled in order of first appearance by the invocation's corresponding noun phrases; definite noun phrases in a title denote context, not slots. Inside the body, `the card` refers to the bound argument. Repeated same-role noun phrases bind by first-occurrence order — prefer role-distinguishing wording instead of relying on that.

**No match is not an error.** An invocation phrase that matches no `To`-title is an ordinary action, performed under the executor's native understanding, subject to the normal failure behavior. Procedures are additive definitions, not a registry.

**Recursion is allowed**; termination is the author's responsibility. State the base case visibly and name a smaller instance in each recursive step.

A stricter profile may map `To validate a card` to an internal name such as `validate-card`, require exact quoting, or error on unmatched invocations — the surface form should remain readable as English.

## 11. Scenarios

A scenario describes an example of expected behavior — useful as tests, demonstrations, and documentation.

```text
Scenario: A valid card is accepted.

Starting facts:
- Card C exists.
- The code on card C is correct.

Task:
1. The agent validates card C.

Expected results:
- Card C is valid.
- Card C is accepted.
- Card C is not rejected.
```

The `Scenario:` label itself carries no contract. The one normative exception: an explicit `Expected results:` section inside a scenario block is **verified** after the task steps complete. An expectation that is false — or that the agent cannot verify — is a failed outcome following [§8](#8-failure-behavior), with the report stating expected versus actual in plain English. An illustrative scenario simply omits the section.

## 12. Style

SAE uses ordinary English sentences, but with discipline.

- Use simple present tense.
- Use active voice.
- Use explicit subjects such as `the agent`, `the system`, `the reviewer`, or a named entity.
- Repeat nouns when necessary instead of relying on unclear pronouns.
- Prefer short sentences over compact but ambiguous wording.
- Prefer explicit complementary conditions over a distant or ambiguous `Otherwise` — especially when text may be copied or reformatted.
- Prefer headings over hidden modes; numbered steps over punctuation-driven sequencing; visible effect statements over unexplained action verbs.

Good:

```text
If the ticket describes a security problem:
  the agent assigns critical priority.

If the ticket does not describe a security problem:
  the agent assigns priority according to the priority rules.
```

Less preferred (allowed when the pairing is visually obvious):

```text
If the ticket describes a security problem:
  assign critical priority.
Otherwise:
  assign priority according to the priority rules.
```

A text that is formally valid but difficult for an ordinary reader is poor SAE style.

## 13. Profiles

SAE leaves strictness to **profiles** — declared execution policies that may tighten the base language where a domain needs determinism:

- pin label vocabulary and semantics;
- require exact or quoted procedure invocations;
- opt into closed-world condition evaluation;
- tighten the failure default or define report channels;
- limit recursion or loop budgets.

A profile's trade-off is declared, not smuggled into the base. The base language's promise is readability: the reader's understanding of the surface English is the canonical semantics.

## 14. Minimal example

```text
Facts:
- Every card has a code.

Rules:
- If the code on a card is correct, the card is valid.

Task: Validate a card.

1. The agent reads the code on the card.
2. If the code is correct:
   the card is valid.
3. If the code is not correct:
   the card is invalid.
4. If the card is valid:
   the agent accepts the card.
5. If the card is not valid:
   the agent rejects the card.

Failure behavior:
- If the agent cannot read the code, the agent reports "unreadable code" and stops.
```

## 15. Authoring guidance

When writing SAE:

- Start with facts and rules.
- Define important actions when their effects are not obvious.
- Write tasks as numbered instructions.
- Use plain English control words: `If`, `For each`, `While`, `As a result`, `If ... fails`.
- Make stopping, retrying, and continuation explicit — or rely on the safe default, knowingly.
- Write for an untrained reader first, and only then for a strict profile.

## 16. Non-goals

SAE does not try to be:

- maximally compact;
- symbol-heavy;
- dependent on special punctuation for meaning;
- readable only after memorizing a reference manual.

The language is successful only if the intended behavior is visible in the surface English itself.
