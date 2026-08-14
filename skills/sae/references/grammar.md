---
type: reference
title: "Grammar of Agent Instruction Texts"
description: "Grammar of the language: blocks and modes, numbering, indentation, conditions, repetition, procedures, scenarios, failure behavior"
tags: [sae]
created: "2026-08-08"
updated: "2026-08-14"
---

# Grammar

## Blocks and modes

A text is a free sequence of blocks.
No block kind of a text is required, ordered, or unique.
Exactly two modes carry the meaning of a text.
A numbered list is an ordered flow.
Every unnumbered top-level line is knowledge.
The knowledge of a text has no order.
A knowledge line sits between the steps of a flow without breaking the flow.

## Numbering

A numbered list continues while its numbers increase.
An unnumbered line between two steps is inert knowledge.
A numbered list that restarts at 1 opens a new flow.
The order of the execution of a text is the written order of its numbered steps and its nested substeps.
A nested substep has a letter.

```text
1. The agent opens the inbox.
2. The agent reads each ticket.

Facts:
- Ticket T-14 is open.

3. The agent closes the inbox.
```

## Indentation

Numbering gives the order of a flow.
Indentation gives the membership of a flow.
A line that is indented under a step belongs to the step.
The indented lines of a step are the consequences of an If-block, the body of a loop, or the lettered substeps of the step.
An indented declarative sentence is an assertion.
An assertion is a state change at that point of the flow.
A top-level declarative sentence is knowledge.
An indented declarative sentence is an effect.

```text
2. If the code is correct:
   the card is valid.
```

## Conditions

A condition has the values known-true, known-false, and undecidable.
A condition that the agent knows to be true takes its branch.
A condition that the agent knows to be false takes the complementary branch.
A step with an undecidable condition fails.
An undecidable condition never silently takes a branch.
An author may override the tri-state in plain English.
A profile may opt into closed-world evaluation.

An If-block has two forms.
The inline form is "If C, the agent does X."
The block form is an If-line and an indented consequence:

```text
If the card is valid:
  the agent accepts the card.
```

An Otherwise-line pairs with the If-line that it immediately follows at the same indentation.
An Otherwise-line means the complementary case.
The explicit negative form is preferred when clarity matters.

## Repetition

A For-each loop fixes its collection at the entry of the loop.
The body of a For-each loop never changes the collection of the loop.
A snapshot step is an explicit step that freezes a collection.

```text
The agent takes a snapshot of the open tickets.
For each ticket T in that snapshot:
  the agent reads ticket T.
```

A While-loop re-evaluates its condition before every pass.
A While-loop is the live construct.
The author of a While-loop is responsible for the termination of the loop.

## Procedures

A procedure has a To-title and a numbered body.
A To-block is top-level knowledge.
A To-block executes only when an invocation binds to its title.
An invocation binds by ordinary-English understanding.
The infinitive of a To-title matches the finite verb of an invocation in any voice.
An indefinite noun phrase of a To-title is a parameter slot.
The slots of a To-title bind in the order of first appearance.
A definite noun phrase of a To-title denotes context, not a slot.
An invocation that matches no To-title is an ordinary action.
A procedure can invoke itself.
The author of a recursive procedure is responsible for its termination.

```text
To validate a card:

1. The agent reads the code on the card.
2. If the code is correct:
   the card is valid.
3. If the code is not correct:
   the card is invalid.
```

## Scenarios

A scenario has a Scenario-label, starting facts, a numbered task, and an expected-results section.
An explicit Expected-results section inside a scenario block is verified after the steps of the task.
An expectation that is false is a failed outcome.
An expectation that the agent cannot verify is a failed outcome.
A scenario without an Expected-results section is illustrative.

## Failure behavior

A step that fails stops the flow and reports the failure.
A report is a plain-English report to the issuing channel.
A report states the failed step and the observed condition.
A failure clause is a delta on the default.
An indented If-fails override under a step beats every other rule.
A standing failure rule is top-level conditional knowledge.
The default applies when no clause applies.
The failure outcomes are ordinary English words.
The surrounding sentences carry the precision of an outcome.
