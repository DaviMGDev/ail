---
type: reference
title: "Base Grammar of Agent Instruction Texts"
description: "Grammar of the base language: golden rules, vocabulary, noun phrases, verb phrases, sentences, queries, commands"
tags: [ail]
created: "2026-08-08"
updated: "2026-08-08"
---

# Base Grammar

## Golden rules

Every noun has a determiner.
The sentence "Women are human." is invalid.
Every declarative sentence is in the simple present.
Every command is in the second person.
Every multi-word proper name is hyphenated.
Every phrasal verb is hyphenated.
A preposition that is part of a phrasal verb or an adjective is hyphenated.
Every passive sentence contains a by-phrase.
The sentence "A card is entered." is invalid.
Every declarative sentence ends with a period.
Every query ends with a question-mark.
Every command ends with an exclamation-mark.
No sentence contains the word "whom".
The sentence "The man whom John sees waits." is invalid.
Every indefinite determiner introduces a new entity.
Every definite determiner refers-to an existing entity.
A pronoun refers-to the most recent compatible entity.

## Vocabulary

A function word is a determiner, a quantifier, a coordinator, a negation word, a pronoun, a query word, a modal verb, a copula, or a genitive particle.
The function words form a closed set.
A content word is a noun, a verb, an adjective, an adverb, or a preposition.
A writer can introduce a new content word at all times.
A new content word is a simple word or a hyphenated compound.

## Noun phrases

The forms of a noun phrase are a determiner with a common noun, a proper name, a pronoun, a number, a string, a set, a list, a measurement, and a variable.
A proper name, a pronoun, a number, a string, a set, a list, a measurement, and a variable have no determiner.
The determiner "a" introduces a new entity.
The determiner "the" refers-to an existing entity.
The determiner "every" and the determiner "each" quantify over all entities.
The determiner "no" negates the existence of an entity.
The determiner "some" occurs with a plural noun or a mass noun.
The determiner "all" has the same meaning as the determiner "every" for a plural noun.
A generalized quantifier has the form "at least 2", "at most 2", "more than 10", "less than 3", or "exactly 3".
A number is an integer or a decimal.
The arithmetic operators are "+", "-", "/", "*" and "^".
A string is a sequence of characters in double quotes.
A set is a sequence of noun phrases in braces.
A list is a sequence of noun phrases in brackets.
A measurement noun phrase contains a number and a unit.
A variable consists of an uppercase letter and an optional integer.
A proper name is a simple word or a hyphenated sequence of words.
A genitive noun phrase contains the particle "'s" or the word "of".
An adjective modifies a noun.
A superlative adjective takes the determiner "the".
The sentence "A richest customer waits." is invalid.
A comparative adjective can take every determiner.
A noun phrase can contain a relative clause with the word "who", the word "which", or the word "that".
A noun phrase can contain a variable in apposition.
A noun phrase can contain a prepositional phrase.

## Verb phrases

A verb is intransitive, transitive, or ditransitive.
A transitive verb takes an object.
A ditransitive verb takes an object and a recipient.
The verb "be" is the copula.
The copula connects a subject to a noun phrase, an adjective phrase, or a prepositional phrase.
Every active sentence has a passive counterpart with a by-phrase.
Every negated verb phrase contains the word "not".
The modal verbs are "can", "cannot", "must", "have to", "should", "should not", "may" and "may not".
The word "and" coordinates two phrases.
The word "or" coordinates two phrases.
The word "and" binds stronger than the word "or".
An adverb modifies a verb phrase.
A prepositional phrase modifies a verb phrase.
Two adverbs conjoin with the word "and".
A verb phrase can contain a sequence of prepositional phrases.

## Sentences

A text is a sequence of sentences.
A sentence has a subject and a verb.
A sentence can contain a complement and an adjunct.
A sentence with the phrase "there is" introduces an entity.
A sentence can contain a comparison operator.
The comparison operators are "=", "\=", ">", ">=", "<" and "=<".
A sentence with the determiner "every" has the meaning of a conditional sentence.
A quantifier phrase at the start of a sentence has the whole sentence in its scope.
The word "if" introduces a condition.
The phrase "it is false that" negates a sentence.
The phrase "it is not provable that" negates a sentence by failure.
The phrase "it is possible that" adds a modality to a sentence.
A propositional verb takes a subordinate sentence with the word "that".
The verb "wants" takes a subordinate verb phrase with the word "to".

## Queries and commands

A yes-no query contains the verb "does" or the verb "is".
The query words are "who", "whose", "what", "which", "how", "where" and "when".
A command with an explicit addressee contains an addressee, a comma, and a verb phrase.
A command without an addressee addresses the executor.
A command without an addressee is valid in a control-context.
