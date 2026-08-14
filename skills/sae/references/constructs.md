---
type: reference
title: "Constructs of Agent Instruction Texts"
description: "Construct catalog: text structure, the two modes, steps, branching, loops, procedures, invocations, failure semantics, profiles"
tags: [sae]
created: "2026-08-08"
updated: "2026-08-14"
---

# Constructs

## Text structure

A text is a free sequence of blocks.
A block of a text is an ordered flow or knowledge.
A numbered list is an ordered flow.
An unnumbered top-level line is knowledge.
No block kind is required, ordered, or unique.
A text may be only a numbered list.
A label of a text is an English heading.
A label is not a contract.
The recommended labels are Facts, Rules, Actions, Task, Tasks, Scenario, Scenarios, Purpose, Starting facts, Expected results, and Failure behavior.
An unrecognized label is inert English.

## The two modes

An ordered flow is a numbered list.
The steps of a flow execute in written order.
Knowledge is everything unnumbered at top level.
The knowledge of a text seeds the world of the text.
A command changes the world of the text.
A condition reads the world of the text.

## Steps

A step is an action sentence, an If-block, a For-each loop, a While-loop, or an invocation of a procedure.
A step may contain a nested lettered substep sequence.
The order of execution is the written order of numbered steps and nested substeps.

```text
Task: Process every open ticket.

1. The agent finds every ticket whose status is open.
2. For each open ticket:
   a. The agent reads the ticket.
   b. If the ticket mentions a security problem:
      the agent assigns critical priority.
   d. The agent saves the ticket.
3. The agent reports the number of processed tickets.
```

## Branching

An If-block is a step with a condition.
An If-block has an indented consequence.
An Otherwise-line pairs with the If-line that it immediately follows at the same indentation.
An Otherwise-line means the complementary case.
A chain has the form "Otherwise, if ...".
Stacked alternatives deserve explicit conditions or a new numbered flow.

```text
If the card is valid:
  the agent accepts the card.
Otherwise:
  the agent rejects the card.
```

A condition has the values known-true, known-false, and undecidable.
A step with an undecidable condition fails.

## Loops

A For-each loop has the form "For each <noun phrase>:" with an indented body.
A For-each loop fixes its collection at the entry of the loop.
A For-each loop never visits an entity that the loop introduces.
A While-loop has the form "While <condition>:" with an indented body.
A While-loop re-evaluates its condition before every pass.
A While-loop reads the world at every pass.
The author of a While-loop is responsible for its termination.

An example of a For-each loop is:

```text
For each card in the queue Q:
  the agent validates the card.
```

An example of a While-loop is:

```text
While the queue is not empty:
  the agent removes one card from the queue.
```

## Procedures

A procedure has a To-title and a numbered body.
A To-block is top-level knowledge.
A To-block executes only when an invocation binds to its title.
An invocation binds by ordinary-English understanding.
The title of a procedure carries the verb and the noun phrases of the procedure.
An indefinite noun phrase of a To-title is a parameter slot.
The slots of a To-title bind in the order of first appearance.
The namespace of the procedures is flat and global.
A near-duplicate To-title is a hazard.
A procedure can invoke itself.
Each invocation of a procedure is a fresh activation.
The non-termination of a procedure is the error of the author.

```text
To validate a card:

1. The agent reads the code on the card.
2. If the code is correct:
   the card is valid.
3. If the code is not correct:
   the card is invalid.
```

## Invocations

An invocation is a step whose action phrase matches a To-title.
The infinitive of a To-title matches the finite verb of an invocation in any voice.
The noun phrases of an invocation fill the parameter slots of the title.
An invocation that matches no To-title is an ordinary action.
An ordinary action runs under the understanding of the executor.
An ordinary action is subject to the failure behavior of the text.
A strict profile may require exact quoting of an invocation.

The step "the agent validates the card" invokes the procedure "To validate a card".

## Failure semantics

A step that fails stops the flow and reports the failure.
A report is a plain-English report to the issuing channel.
A report states the failed step and the observed condition.
The failure cascade has three layers.
The first layer is an indented If-fails override under the step.
The second layer is a standing failure rule.
The third layer is the default.
A failure clause is a delta on the default.
The side effects of the steps before the failing step persist.
The failure outcomes are ordinary English words.
A profile may tighten the failure behavior.

```text
2. The agent saves the ticket.
   If saving fails:
   a. the agent retries once.
   b. If the retry fails:
      the agent reports the ticket and continues with the next ticket.
```

## Profiles

A profile is a declared execution policy.
A profile may pin labels.
A profile may require exact invocations.
A profile may opt into closed-world evaluation.
A profile may tighten the failure default.
A profile may limit recursion or loop budgets.
The trade-off of a profile is declared.
The base language promises readability.
