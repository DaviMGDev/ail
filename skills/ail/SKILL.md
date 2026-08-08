---
name: ail
description: >-
  Write agent instruction texts: ordered steps, branching, loops, and named
  procedures over an explicit world model. Use when authoring or reviewing
  such texts.
metadata:
  language: "ail"
---

# Agent Instruction Texts

A task has a description and a text.
Every text has a knowledge-section and a main-sequence.
A procedure is a named sequence of steps.

The knowledge-section of a text seeds the world of the text.
Every object of a text is in the world of the text.
Every fact of a text is in the world of the text.
The commands of the main-sequence of a text execute in written order.
A condition reads the world of a text.
A fact that is not in the world of a text is false.

Every noun has a determiner.
Every declarative sentence ends with a period.
Every command ends with an exclamation-mark.
Every query ends with a question-mark.
Every command is in the second person.
Every declarative sentence is in the simple present.
Every multi-word proper name is hyphenated.
Every indefinite determiner introduces a new entity.
Every definite determiner refers-to an existing entity.

Every step is a command, a call, or an if-otherwise construct.
Every if-otherwise construct is a step with a condition.
Every Otherwise-clause immediately follows an if-sentence.
The body of a loop is exactly one step.
Every argument of a call denotes one entity.
No query is a step.
No text mentions the name of its language.
A text-file should have a frontmatter with the tag "ail".

First read the description of the task!
Then read "references/grammar.md"!
Then read "references/constructs.md"!
Then read "references/example-text.md"!
Then write the knowledge-sentences of the text!
Then write the commands of the main-sequence of the text in the order of execution!
If a sequence of the steps of the text repeats then write a procedure for the sequence!
If a step of the text needs a condition then write an if-otherwise construct!
If a step of the text repeats for every entity of a collection then write a for-every loop!
If a step of the text repeats while a condition holds then write a while-loop!
Then check-text(the text)!
If a rule is unclear then read "references/assumptions.md"!

Procedure check-text(Text T):
  Check the determiners of the text T!
  Check the punctuation of the text T!
  Check the hyphenation of the text T!
  Check the anaphora of the text T!
  If the text T violates a rule then correct the text T!
