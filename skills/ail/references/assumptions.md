---
type: reference
title: "Assumptions for Writing Agent Instruction Texts"
description: "Documented assumptions and judgment calls where the definition of the language is silent"
tags: [ail]
created: "2026-08-08"
updated: "2026-08-08"
---

# Assumptions

## Containers

A file contains a text and a container.
The definition of the language does not define a file format.
The frontmatter of a file is not part of the text.
A heading of a file is not part of the text.
A code fence contains a separate text.

## Markers

A reference file declares the tag "ail" in its frontmatter.
The skill specification does not allow the tags field in a skill file.
The marker of a skill file lives in the metadata field.
A date in the frontmatter has the form "YYYY-MM-DD".

## Style

A rule about all texts uses the determiner "every".
A rule in a reference file is a universal statement.
An invalid sentence appears in quotes.
A sentence with the word "invalid" is a counterexample.
A file reference in a command is a relative path.
A hyphenated compound is a new content word.
An example in a reference file is illustrative.

## Readings

A conditional step without an Otherwise-clause is valid.
A loop is not an arm of an if-otherwise construct.
No text names its language.
A generic term like "a text" or "the language" is not a self-reference.
A bare plural is valid after the word "of" or the word "but".
A noun phrase of the form "the X of a Y" has an accessible antecedent in its complement.
