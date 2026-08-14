---
type: language-reference
title: "ACE 6.7 — Heritage Reference"
description: "Historical reference for Attempto Controlled English 6.7, SAE's ancestor: golden rules, noun/verb phrases, sentences, queries, commands, semantics. Not the base of SAE — kept for ancestry and comparison."
created: "2026-08-08"
updated: "2026-08-14"
---

# ACE 6.7 — Heritage Reference

> **Heritage note.** This document was the base language reference when this
> repository documented the ACE / AIL fork. Since the 2026-08-14 reframing
> (see `.pi/discussions/sae-reframing/`), the primary language of this
> repository is **Structured Agent English (SAE)** — see [LANGUAGE.md](LANGUAGE.md).
> SAE is a **formal break** from ACE, not an extension: it deliberately drops
> ACE's punctuation-as-semantics, determiner grammar, hyphenation, and
> anaphora rules. This reference is kept unchanged (except for this note) as
> the record of SAE's ancestry. The AIL → SAE migration is mapped in
> [ail.md](ail.md).

Attempto Controlled English (ACE) is a controlled natural language from the University of Zurich (since 1995, current version **6.7**). It is a strict subset of English with restricted syntax and semantics: every valid ACE text is correct English and translates **unambiguously** into first-order logic (via Discourse Representation Structures, DRS). It is a formal language that happens to read like English.

Sentences marked with `*` are **not** valid ACE — they serve as counterexamples.

## Golden rules

1. **Every noun needs a determiner.** `*Women are human.` is invalid → `Every woman is a human.`
2. **Verbs are 3rd person simple present** in declaratives/interrogatives; **2nd person** in commands. No tenses, no aspect.
3. **Hyphenate** multiword proper names (`United-Nations`), phrasal verbs (`fills-in`), and prepositions attached to transitive verbs/adjectives (`interested-in`).
4. **Passives require a `by` phrase**: `A card is entered by John.`
5. **Punctuation is semantic**: declaratives end with `.`, queries with `?`, commands with `!`.
6. **No `whom`** — use `who`.
7. **Anaphora rules**: `a`/`some` introduce new entities, `the` refers back to an already-introduced entity, pronouns resolve to the most recent compatible antecedent.

## Vocabulary

- **Function words** (predefined, not user-extensible): determiners, quantifiers, coordinators, negation words, pronouns, query words, modal auxiliaries, copula `be`, Saxon genitive `'s`.
- **Fixed phrases**: `there is/are …`, `it is false that …`, `it is possible that …`, `it is not provable that …`
- **Content words** (user-defined): nouns, verbs, adjectives, adverbs, prepositions. Simple (`code`) or hyphenated compounds (`check-code`).

## Noun phrases

### Determiners (singular countable)

| Form | Meaning |
|---|---|
| `a card` / `1 card` / `one card` | existential (interchangeable) |
| `the card` | anaphoric (already introduced) |
| `every card` / `each card` | universal (interchangeable) |
| `not every card` / `not each card` | negated universal |
| `no card` | negated existential |
| `all cards` | sugar for `every card` |
| `no cards` | sugar for `no card` |

### Plural & mass nouns

- Collective: `the cards`, `some cards`, `3 cards`, `three cards`
- Distributive: `each of the cards`, `each of some cards`, `each of 3 cards`
- Mass: `some water`, `no water`, `all water`, `not all water`
- Integers ≤ 12 can be written as words (`twelve cats`); larger ones must be digits.

### Generalized quantifiers

`at least 2 cards`, `at most 2 cards`, `more than 10 cards`, `less than 3 cards`, `exactly 3 cards` — and distributive `each of at least 2 cards`, etc.

### Other noun phrase forms

- **Proper names**: `John`, `Mr-Miller`, `the United-Nations` (multiwords hyphenated; singular or plural; with or without `the`)
- **Numbers**: integers `0`, `12`, `-2`; reals `3.141`, `-2.718` (no `+` prefix)
- **Arithmetic**: `1 + 2 / X * 4`, `2 ^ (3 ^ 4)` — precedence applies, APE does not evaluate
- **Strings**: `"abc"`, escaping with `\"` and `\\`, concatenation `"abc" & "123"`
- **Sets/lists**: `{3, 6, [1,2]}`, `[3, 4, 5, "ab", John, 1+2]`; e.g. `X is an element of [3, 4, 5]`
- **Measurement nouns**: `2 m`, `31.2°C`, `1.4 l of water`, `3 kg of apples` (singular or plural verb)
- **Variables**: single uppercase letter + optional integer, introduced as apposition — `A man X sleeps. X is young.`; bare variables allowed — `X weighs 300 kg.`
- **Pronouns**: `he/she/it/they`, `him/her/them`; reflexive `himself/herself/itself/themselves`; `you/yourself/yourselves` (commands only); indefinite `someone/somebody`, `no one/nobody`, `everything`, `not everyone`
- **Genitives**: `John's customer`, `a customer of John`, `everybody's customer`, `X's dog`, `his customer`, `his own customer`
- **`nobody but` / `nothing but` / `no … but`**: `nothing but apples`, `nobody but John`, `no man but John` (bare plurals, mass nouns, proper names)

### Modifying nouns

- **Adjectives** (positive/comparative/superlative, conjoinable): `a rich customer`, `a rich and satisfied customer`, `a richer customer`, `a richest customer`
- **Relative clauses** with `who`/`which`/`that`, coordinate with `and`/`or`: `a customer who is rich and who is well-known`, `everything which is important`, `John who waits`
- **Apposition variables**: `a customer X`, `the customer C1`

## Verb phrases

- **Verb types**: intransitive (`wait`), transitive (`enter something`), ditransitive (`give something to somebody` / `give somebody something`)
- **Active ↔ passive**: `John enters a card.` = `A card is entered by John.`; `John gives a card to a customer.` = `A card is given to a customer by John.`
- **Copula `be`** + noun phrase / adjective phrase / prepositional phrases: `John is a rich customer.`, `John is rich.`, `John is in the garden on the hill.`, `John is who?`
- **Comparison**: `as rich as Mary`, `richer than Mary`, `as fond-of Mary as Bill`, `more fond-of Mary than of Sue`
- **Negation**: `John does not enter a code.`, `The men do not wait.`, `Some water is not drinkable.`
- **Negation as failure**: `John does not provably wait.`, `The men are not provably admitted.`
- **Modals**: possibility `can / cannot / can not / can't`; necessity `must / have to / does not have to`; recommendation `should / should not / shouldn't`; admissibility `may / may not`
- **Coordination**: `John waits and eats a burger.`, `John is rich or earns his own income.`
- **Modifiers**: adverbs & prepositional phrases before or after the verb phrase — `A customer manually inserts a card into a slot.`; two+ adverbs conjoin with `and` (`carefully and manually`), two+ PPs concatenate (`in a bank in the morning`)

## Sentences

### Basic structure

```
subject + verb + complements + adjuncts
```

`A customer waits.` · `A customer inserts a card.` · `A customer gives a clerk a card.` · `A customer inserts a card manually into a slot.`

### `there is/are` sentences

Introduce (or deny) entities — no definite/universal NPs, proper names, numbers, strings, sets, or lists allowed after them:

`There is a customer.` · `There are a cat and 2 dogs.` · `There is no man who sleeps.` · `*There is a cat in a garden.` (→ `There is a cat that sleeps.`)

### Boolean formulas

Sentences built with comparison operators `=`, `\=`, `>`, `>=`, `<`, `=<`: `10 = 4 + 6.`, `X \= 2.`, `X >= 13.4 and X =< 20.` (APE does not evaluate)

### Coordination

- `and` / `or` between sentences, verb phrases, relative clauses, noun phrases
- **`and` binds stronger than `or`** (standard logic binding order); `,and` and `,or` override it
- `The screen blinks or John waits, and Mary enters a card.`
- Noun-phrase coordination forms a plural: `A man and at least 2 women wait. They are tired.`

### Quantification

- **Existential**: indefinite determiner (`a`, `some`) or `there is/are`
- **Universal**: `every`/`each`, or if-then: `Every man waits.` = `If there is a man X then the man X waits.`
- **Scope** extends to end of sentence (or coordinated clause)
- **Global quantification** (sentence-initial): `There is a code that every clerk enters.`, `For every code a clerk enters it.`, `For each of 3 men there is a bed.`, `For all water there is a container.`
- Scope control: `Every customer inserts a card.` (each may insert a different card) vs. `A card is inserted by every customer.` (same card)

### Subordination (five forms)

| Form | Example |
|---|---|
| Conditional (if-then) | `If a card is valid then a customer inserts it.` |
| Sentence negation | `It is false that a screen blinks.` / `It is not true that …`; repeat `that` in coordinations: `It is false that a screen blinks and that John enters a code.` |
| Negation as failure | `It is not provable that a screen blinks.` |
| Modality | `It is possible/not possible/necessary/not necessary/recommended/not recommended/admissible/not admissible that …` |
| Sentence subordination | `A clerk believes that a customer inserts a card.`; same-subject shortening: `John wants to insert a card.`; modifiers must precede the main verb: `John eagerly in the morning wants to insert a card.` |

## Queries (end with `?`)

- **Yes/no**: `Does John enter a card?`, `Is the card valid?`, `Is it true that a man waits?`
- **wh-queries** (`who`, `whose`, `what`, `which`, `how`, `where`, `when` — every element except the verb is queryable): `Who waits?`, `Which customer inserts a card?`, `What does a man not eat?`, `How does John enter a card?`, `Whose dog barks?` — most have alternative word orders: `John waits where?`
- **How much/many**: `How much water boils?`, `How many men have how many apples?`

## Commands (end with `!`)

Addressee (noun phrase) + comma + (negated, uncoordinated) verb phrase:

`John, go to your own bank!` · `John and Mary, clean yourselves!` · `Every dog, do not bark!` · `John's brother, return the book to Mary!`

## Texts & semantics (interpretation rules)

- An **ACE text** is a sequence of declarative/interrogative/imperative sentences; anaphora links them — `A man has a car. Does he see the car? John, identify the car!`
- `a`/`some` → **existential** ∃; `every`/`each` → **universal** ∀; `the`/pronouns → **anaphoric reference**
- DRS output can be translated to OWL, SWRL, AceRules, and first-order logic (for theorem proving, consistency checking, querying)

## Cheat sheet

| Want to say | Write |
|---|---|
| Existence | `A customer inserts a card.` |
| Universality | `Every customer inserts a card.` |
| Rule | `If a card is valid then a customer inserts it.` |
| No | `No customer inserts more than 2 cards.` |
| Not (verb) | `A customer does not insert a card.` |
| Not (sentence) | `It is false that a customer inserts a card.` |
| Modality | `A customer can/must insert a card.` / `It is possible that …` |
| Passive | `A card is inserted by a customer.` |
| Variable | `A customer X inserts a card. X is trusted.` |
| Global scope | `For every card there is a customer who inserts it.` |
| Ask | `Does a customer insert a card?` / `What does a customer insert?` |
| Command | `Customer, insert a card!` |

## Tools & resources

- **APE** (Attempto Parsing Engine) — reference parser; web demo at attempto.ifi.uzh.ch; outputs DRS / FOL / OWL / SWRL
- **AceWiki** — semantic wiki powered by ACE; **AceRules** — rule engines over ACE
- **ACE-in-GF** (github.com/Attempto/ACE-in-GF) — ACE 6.7 syntax ported to ~20 natural languages via Grammatical Framework
- **Official docs**: ACE 6.7 Construction Rules (syntax), Interpretation Rules (semantics), Troubleshooting Guide, Language Manual — attempto.ifi.uzh.ch
