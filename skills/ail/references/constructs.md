---
type: reference
title: "Constructs of Agent Instruction Texts"
description: "Construct catalog: text structure, world model, control contexts, steps, branching, loops, procedures, calls, Stop!, failure semantics, fiat rulings"
tags: [ail]
created: "2026-08-08"
updated: "2026-08-08"
---

# Constructs

## Text structure

A text has a knowledge-section and a main-sequence.
A procedure is a named sequence of steps.
A declarative sentence outside a procedure-body is in the knowledge-section of its text.
The declarative sentences of the knowledge-section have no order.
The knowledge-section of a text seeds the world of the text.
An imperative sentence outside a procedure-body is in the main-sequence of its text.
The commands of the main-sequence execute in written order.
A query is valid at the top level of a text.
No query is a step.
A text with no commands has an empty main-sequence.

## World model

Every object of a text is in the world of the text.
Every fact of a text is in the world of the text.
A command changes the world of the text.
A condition reads the world of the text.
A fact that is not in the world of the text is false.
A declarative sentence in a procedure-body asserts a fact.
An assertion adds an object or a fact to the world of the text.
The executor of a command determines the effects of the command.

## Control contexts

A control-context is the main-sequence or a procedure-body.
The sentences of a control-context execute in written order.
A command in a control-context can omit the addressee.

## Steps

A step is a command, a call, or an if-otherwise construct.
An if-otherwise construct has a then-arm and an optional otherwise-arm.
Every arm of an if-otherwise construct is a single step.
An if-otherwise construct cannot contain an if-otherwise construct.
The body of a loop is exactly one step.
A multi-step iteration calls a procedure.
A command that matches a defined procedure name is a call.
Any other command is an ordinary command.

## Branching

An if-otherwise construct is a step with a condition.
An Otherwise-clause immediately follows an if-sentence.
No other step intervenes between an if-sentence and the following Otherwise-clause.
An Otherwise-clause has the complementary case of the condition of the preceding if-sentence.
A chain of Otherwise-clauses has the form "Otherwise if B then Y!".
Every guard of a chain conjoins the negations of all earlier conditions.
The guards of a chain are disjoint and cover every case.
A bare Otherwise-clause with no preceding if-sentence is invalid.
A period marks a knowledge-context.
An exclamation-mark marks a control-context.

An example of a knowledge-context rule is "If a card is valid then the card is accepted. Otherwise the card is rejected.".
An example of a control-context step is "If the code of the card C is correct then accept the card C! Otherwise reject the card C!".

## Loops

A for-every loop iterates over the entities of a noun phrase.
A for-every loop has the form "For every <noun phrase>: <step>!".
A for-every loop snapshots its collection at the entry of the loop.
A for-every loop does not visit an entity that the loop introduces.
A while-loop has the form "While <condition>: <step>!".
A while-loop re-evaluates its condition before every pass.
An existential noun phrase in a condition introduces a fresh entity at every evaluation.
The anaphora of the body of a while-loop uses the witnesses of the current pass.
If at least 2 entities match then the choice of a while-loop is non-deterministic.
A procedure must not depend on the choice of a while-loop.
A while-loop reads the world at every pass.
A writer is responsible for the termination of a while-loop.

An example of a for-every loop is "For every card in the queue Q: check-card(the card)!".
An example of a while-loop is "While there is a card in the queue Q: remove a card from the queue Q!".

## Procedures

A procedure has a hyphenated name.
A procedure definition has a header and a body.
A header has the form "Procedure <name>(<parameter>):".
A parameter is a typed apposition variable.
The type of a parameter is a constraint on the arguments of the calls.
A call with an argument outside the type of a parameter is invalid.
The body of a procedure is a sequence of steps.
Every step of a body is indented by at least one space.
The body of a procedure ends at the first line that is not indented.
The namespace of the procedures is flat and global.
A nested procedure definition is invalid.
A redefinition of a procedure name is invalid.
A procedure can call itself.
Each call of a procedure is a fresh activation.
The non-termination of a procedure is the error of the writer.

```
Procedure check-card(Card C):
  Check the code of the card C!
  If the code of the card C is correct then accept the card C! Otherwise reject the card C!
```

## Calls

A call has a procedure name and an argument list.
A call has the form "<name>(<arguments>)!" in command position.
An argument is an entity-denoting noun phrase.
A definite argument must have an accessible antecedent.
An indefinite argument introduces a fresh entity.
The fresh entity of an argument remains accessible after the call.
A proper name is a valid argument.
A variable is a valid argument.
A quantified argument is invalid.
A coordinated argument is invalid.
The parameter of a call denotes the referent of the argument during the call.
The argument is the most recent entity at the entry of the call.
The anaphora inside the body follows the most recent antecedent.
A call is a step.
Execution continues with the next step after the call returns.

The calls "check-card(the card)!", "check-card(C)!" and "check-card(a card)!" are valid.

## Stop!

The command "Stop!" terminates the current procedure.
The command "Stop!" in the main-sequence ends the run.
The word "Stop!" is reserved in its bare imperative form.
The command "Stop acting!" is an ordinary command.
The command "Stop!" after the last step is harmless and redundant.

## Sequence markers

Each of the words "First", "Next", "Then" and "Finally" is an optional sentence-initial marker.
A sequence marker does not change the order of execution.

An example of the markers is "First check the code of the card! Then accept the card!".

## Failure semantics

Every condition has a truth value.
An impossible step aborts the whole run at the point of the step.
The impossible steps are a command that refers-to an entity with no accessible antecedent, a call to an undefined procedure, and a call with a mismatched argument.
The side effects of the steps before the failing step persist.
No recovery construct exists.

## Fiat rulings

A keyword is reserved only in its defined position.
The word "Otherwise" is reserved in the position after an if-sentence.
The word "Procedure" is reserved at the start of a procedure header.
The phrase "For every" and the word "While" are reserved at the start of a loop.
A keyword is an ordinary word in every other position.
The colon of a header is a semantic token.
The indentation is the delimiter of a procedure-body.
