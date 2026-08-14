---
type: reference
title: "Assumptions for Writing Agent Instruction Texts"
description: "Documented assumptions and judgment calls where the definition of the language is silent"
tags: [sae]
created: "2026-08-08"
updated: "2026-08-14"
---

# Assumptions

## Containers

A file contains a text and a container.
The definition of the language does not define a file format.
The frontmatter of a file is not part of the text.
A heading of a file is not part of the text.
A code fence contains a separate text.

## Markers

A reference file declares the tag "sae" in its frontmatter.
The skill specification does not allow the tags field in a skill file.
The marker of a skill file lives in the metadata field.
A date in the frontmatter has the form "YYYY-MM-DD".

## Style

A rule about all texts uses the determiner "every".
A rule in a reference file is a universal statement.
A knowledge line sits between the steps of a flow without breaking the flow.
An example of a step is a numbered line of a code fence.
A sentence inside a code fence is not a step of the reference file itself.

## Judgment calls

The language defines no effects.
The executor of a command determines the effects of the command.
The agent reports to the channel that issued the instruction.
A bare "retries" means a retry with no stated count.
After a bare retry fails, the default applies.
The agent stops and reports the failure.
A report states the failed step and the observed condition.
