---
name: sae
description: >-
  Write agent instruction texts: ordered steps, branching, loops, and named
  procedures over an explicit world model. Use when authoring or reviewing
  such texts.
metadata:
  language: "sae"
---

# Agent Instruction Texts

A task has a description and a text.
A text is a free sequence of blocks.
No block kind of a text is required.
A numbered line of a text is a step of the flow of the text.
An unnumbered top-level line of a text is knowledge.
The knowledge of a text has no order.
A numbered list of a text continues while its numbers increase.
A numbered list of a text that restarts at 1 opens a new flow.
A line that is indented under a step belongs to the step.
An indented declarative sentence is an assertion at that point of the flow.
A step is an action sentence, an If-block, a For-each loop, a While-loop, or an invocation of a procedure.
An If-block has a condition and an indented consequence.
An Otherwise-line pairs with the If-line that it immediately follows at the same indentation.
A condition has the values known-true, known-false, and undecidable.
A step with an undecidable condition fails.
A step that fails stops the flow and reports the failure.
A For-each loop fixes its collection at the entry of the loop.
A While-loop re-evaluates its condition before every pass.
A procedure has a To-title and a numbered body.
A title of a procedure has a verb and the noun phrases of the procedure.
An invocation of a procedure is a step whose action matches a To-title in ordinary English.
An indefinite noun phrase of a To-title is a parameter slot of the procedure.
An invocation that matches no To-title is an ordinary action.
A scenario with an explicit Expected-results section verifies the expectations after its steps.
No text mentions the name of its language.
A text-file should have a frontmatter with the tag "sae".

1. Read the description of the task.
2. Read "references/grammar.md".
3. Read "references/constructs.md".
4. Read "references/example-text.md".
5. Write the knowledge of the text.
6. Write the steps of the text as a numbered flow.
7. If a sequence of the steps of the text repeats:
   write a procedure with a To-title for the sequence.
8. If a step of the text needs a condition:
   write an If-block.
9. If a step of the text repeats for every item of a collection:
   write a For-each loop.
10. If a step of the text repeats while a condition holds:
    write a While-loop.
11. Check the text.
12. If a rule is unclear:
    read "references/assumptions.md".

To check a text:

1. Check the layout of the text.
2. Check the numbering of the text.
3. Check the indentation of the text.
4. If a step of the text can fail:
   check the failure behavior of the step.
5. If the text violates a rule:
   correct the text.
