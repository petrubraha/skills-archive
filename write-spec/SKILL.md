---
name: write-spec
description: Rules for writing an implementation spec, a step-by-step plan followed commit by commit. Use when asked to write or update a spec, implementation plan, or design doc.
metadata:
  version: "0.0.1"
---

# Write Spec

This skill defines how to write an implementation spec. When the project's own instructions (e.g. `CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md`) set a different convention, the project wins.

## Location

- **Own file:** every spec is an independent Markdown file in the project's spec folder. If the project has none, use `.specs/`.
- **Working rules:** if earlier specs exist, copy their "Working Rules" and "Definition of Done" chapters, then adapt them to the topic. Otherwise, write both chapters from scratch.

## Content

- **Small commits:** split the work into numbered steps; one step = one commit; sub-steps (2, 2.1) are separate commits.
- **Fill gaps:** add every missing detail; name each decision you made and why.
- **Spec notes:** text inside "( )" in a request is for the spec writer, not for the spec.
- **Per-step goals:** when the goal is a quality (e.g. intuitiveness), every step gets its own subsection with concrete practices for that quality.
- **Degraded modes:** when the product can run without a network or a dependency (e.g. a mobile or desktop client offline), say what each feature does in that state and how the UI explains what is disabled.
- **Keep what works:** list the good mechanisms already in the codebase that the work must move and reuse, not rewrite.
- **Modular design:** design new code to be decoupled and reusable by other features; name the extension points and the one-way import rules.
- **Docs updates:** a step that adds or changes a feature also updates the project docs that describe it (agent instruction files, READMEs, architecture notes) in the same commit.

## Format

- **Chapters:** organize with `##`, `###`, `####`.
- **Bullet points:** prefer bullets; avoid large blocks of text.
- **Short statements:** simple, descriptive sentences.
- **Bullet summaries:** every bullet starts with a bold two-word summary, e.g. `- **Oven timer:** …`.

## Data and API Design

Apply this chapter when the work adds or changes persisted data or an API.

- **4NF models:** new data models must be in fourth normal form; include a short check in the spec.
- **Split decision:** when related settings or records could live in one model or several (e.g. one per feature or per channel), say which and why.
- **Field names:** boolean facts read `<query verb>_<feature>_<noun>`, e.g. `saw_menu_tutorial`, `finished_checkout_tour`.
- **Idempotent writes:** preference and settings endpoints set explicit values (e.g. `PATCH` with the target state); never toggle; repeating a request never reverts it.
- **Resource nesting:** user-scoped APIs nest under the user, e.g. `/api/users/<user_id>/addresses`, unless the project already uses another scheme.
- **Owner only:** user-scoped data is reachable through the public API only by its owner (`403` for everyone else, privileged users included); admins use a separate admin interface. The spec states the permission check and its tests.
- **Legacy aliases:** a renamed route keeps its old path as an alias until no supported client version calls it.

## Hand-over

- **Suggestions:** after writing the spec, reply with implementation suggestions as short bullets, each with a two-word summary.
- **Answers:** answer questions about the spec in 1–3 sentences.

## Related Skills

- `write-prose`: punctuation rules for the text itself (no em dash).
