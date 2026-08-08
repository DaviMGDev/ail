---
type: log
title: "specs/ log"
description: "Activity log for the specs/ directory"
created: "2026-08-08"
updated: "2026-08-08"
---

# specs/ log

## 2026-08-08

- Initialized `specs/` — ACE (Attempto Controlled English), status draft.
- Added `LANGUAGE.md` — full ACE 6.7 syntax and practical reference (golden rules, noun/verb phrases, sentence forms, queries, commands, semantics, cheat sheet) — this is the primary artifact; SPEC.md kept intentionally light.
- Reframed `SPEC.md` — subject is now ACE / ACL: the spec documents ACE 6.7 and its fork ACL (Agent Controlled Language). Added US-002 (write ACL procedures), ACL decisions, naming note. Reason: the project's purpose evolved from documenting ACE to designing ACL.
- Added `acl.md` — ACL extension reference (superset guarantee, world model, control contexts, steps, `Otherwise`, `For every`, `While`, procedures, `Stop!`, failure semantics, fiat rulings, compatibility annex, deliberately omitted constructs). Reason: ACL design discussion concluded (see `discussions/specs-directory/snapshots/`); the extension needed its own citizen file, one concern per file.
- Updated `index.md` — registry and reading order now include `acl.md`. Reason: new citizen.
- Renamed the extension: AIL (Agent Instruction Language); `ail.md` replaces `acl.md`; SPEC.md, index.md, AGENTS.md updated. Reason: avoid the FIPA ACL homonym; clean rename.
- Migrated `SPEC.md` to the v4 spec-md contract: added `sections: [context, users, conformance, decisions]` frontmatter, removed the `## Must contain` checklist, dropped enforced-only template sections (`architecture`, `stack`, `ops`, `api`) and reworked `user-stories` + `api` content into `conformance`. Reason: v4 contract — the frontmatter declaration is the contract and the body must match it exactly; terminal "not applicable" sections are no longer declared. Also updated the SPEC.md one-liner in `index.md`.
