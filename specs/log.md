---
type: log
title: "specs/ log"
description: "Activity log for the specs/ directory"
created: "2026-08-08"
updated: "2026-08-14"
---

# specs/ log

## 2026-08-14

- Cleaned `log.md` — dropped references to records that are no longer part of the repository: the pre-reframing `discussions/` snapshots (removed) and the `.pi/` state (plans, decision records — no longer tracked). Reason: internal references must resolve; design rationale now lives outside the repository.
- Cleaned `ace.md` — the heritage note no longer points to the removed reframing record (`.pi/discussions/sae-reframing/`). Reason: internal references must resolve.
- Cleaned `ail.md` — the retired note no longer points to the removed reframing record or the deleted `discussions/specs-directory/snapshots/` records. Reason: internal references must resolve.
- Cleaned `SPEC.md` — the heritage paragraph and the reframing decision no longer cite the removed reframing record. Reason: internal references must resolve.

- Updated `index.md` — registry and reading order now reflect the SAE reframing: SPEC.md (SAE spec), LANGUAGE.md (SAE reference), ace.md (ACE heritage), ail.md (AIL migration note). Reason: registry follows the file set; the reframing added ace.md and replaced the contents of LANGUAGE.md, ail.md, SPEC.md.
- Rewrote `SPEC.md` — subject is now SAE (Structured Agent English): context (readability goal, two-mode core, heritage), users (authors, readers, executors, profile authors), conformance (EARS criteria for the normative core), decisions (reframing + locked core decisions). Sections unchanged: [context, users, conformance, decisions]. Reason: the accepted SAE reframing.
- Replaced `ail.md` — the AIL extension reference is retired; the file is now a heritage and migration note: what AIL was, why SAE replaced it, and the construct mapping (procedures → `To`-blocks, calls → English invocation, `Stop!` → the stop-and-report default, closed world → open-world tri-state, etc.). Reason: the accepted SAE reframing; the old extension reference is superseded by the SAE reference in `LANGUAGE.md`.
- Added `ace.md` — the ACE 6.7 syntax and practical reference, preserved unchanged as a heritage document with a preamble stating the formal break. Reason: the accepted reframing keeps ACE as ancestry, not as a base; the content formerly lived in `LANGUAGE.md`, which is now the SAE reference.
- Rewrote `LANGUAGE.md` — it is now the Structured Agent English (SAE) language reference: two layout modes (ordered steps / unordered statements), the block model, resumptive numbering, the two-axis rule, open-world tri-state conditions, `For each` snapshot / `While` live, stop-and-report failure default with cascade, `To`-title procedures with English-phrase binding, the `Expected results:` verification exception, profiles. Reason: the SAE reframing was accepted; the old content (ACE 6.7 reference) moves to `ace.md` as heritage.

## 2026-08-08

- Initialized `specs/` — ACE (Attempto Controlled English), status draft.
- Added `LANGUAGE.md` — full ACE 6.7 syntax and practical reference (golden rules, noun/verb phrases, sentence forms, queries, commands, semantics, cheat sheet) — this is the primary artifact; SPEC.md kept intentionally light.
- Reframed `SPEC.md` — subject is now ACE / ACL: the spec documents ACE 6.7 and its fork ACL (Agent Controlled Language). Added US-002 (write ACL procedures), ACL decisions, naming note. Reason: the project's purpose evolved from documenting ACE to designing ACL.
- Added `acl.md` — ACL extension reference (superset guarantee, world model, control contexts, steps, `Otherwise`, `For every`, `While`, procedures, `Stop!`, failure semantics, fiat rulings, compatibility annex, deliberately omitted constructs). Reason: ACL design discussion concluded; the extension needed its own citizen file, one concern per file.
- Updated `index.md` — registry and reading order now include `acl.md`. Reason: new citizen.
- Renamed the extension: AIL (Agent Instruction Language); `ail.md` replaces `acl.md`; SPEC.md, index.md, AGENTS.md updated. Reason: avoid the FIPA ACL homonym; clean rename.
- Migrated `SPEC.md` to the v4 spec-md contract: added `sections: [context, users, conformance, decisions]` frontmatter, removed the `## Must contain` checklist, dropped enforced-only template sections (`architecture`, `stack`, `ops`, `api`) and reworked `user-stories` + `api` content into `conformance`. Reason: v4 contract — the frontmatter declaration is the contract and the body must match it exactly; terminal "not applicable" sections are no longer declared. Also updated the SPEC.md one-liner in `index.md`.
