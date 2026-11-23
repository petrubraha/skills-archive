---
name: write-spec
description: Rules for writing an implementation spec, a step-by-step plan followed commit by commit. Use when asked to write or update a spec, implementation plan, or design doc.
metadata:
  version: "0.0.1"
---

# Write Spec

This skill defines how to write an implementation spec. When the project's own instructions (e.g. `CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md`) set a different convention, the project wins.

## Format

- **Single file:** every spec is an independent Markdown file in the project's spec folder. If the project has none, use `.specs/`.
- **Chapters:** organize with `##`, `###`, `####`.
- **Bullet points:** prefer bullets; avoid large blocks of text.
- **Short statements:** simple, descriptive sentences.
- **Bullet summaries:** every bullet starts with a bold two-word summary, e.g. `- **Oven timer:** …`.
- **No artifacts:** keep diagrams, matrices, big tables out of the spec; link to a separate Markdown file that holds them.
- **Class diagram:** when the system needs many classes, put a class diagram in its own Markdown file and link it.

## Content

- **Three chapters:** every spec has goals, requirements, and precise implementation steps.
  - **Goals chapter:** state the high-level outcomes the work must reach.
  - **Requirements chapter:** spell out the unambiguous work needed to reach those goals.
  - **Steps chapter:** break the requirements into modular steps, each one pull request.
    - **Numbered steps:** number the implementation steps from 0 to n; one step is one pull request.
    - **Roman grouping:** past 15 steps, group them under Roman numerals (I, II, III, etc.); keep the inner steps numbered.
    - **No decimal steps:** never write a step like 2.3; split it into its own numbered step instead.
- **Stay concise:** state each step in the fewest words that remain precise.
- **Fill gaps:** add every missing detail; name each decision you made and why.
- **Degraded modes:** when the product can run without a network or a dependency (e.g. a mobile or desktop client offline), say what each feature does in that state and how the UI explains what is disabled.
- **Keep what works:** list the good mechanisms already in the codebase that the work must move and reuse, not rewrite.

## Design Targets

- **Modular system:** the target is always a modularized system; single responsibility is a strict rule.
- **Best code:** optimize in strict priority order, execution speed first, then readability, then documentation.

## Testing and Boundaries

- **Test plan:** state how the work is tested, naming the kinds of tests each step needs (e.g. unit, integration, end to end).
- **Publish gate:** state the boundaries that block a pull request, e.g. coverage thresholds, passing suites, etc.
- **Clear thresholds:** give concrete numbers for each gate so the author knows when the work is done.

## Data and API Design

These are design guidelines for the spec author, not text to copy into the spec. Apply them while designing persisted data or an API, so the spec presents a solution that already follows them. Name a choice only where it is not obvious (e.g. note that a model is in 4NF), never restate the rule itself.

- **4NF models:** design new data models in fourth normal form.
- **Split decision:** when related settings or records could live in one model or several (e.g. one per feature or per channel), choose one and say why.
- **Field names:** name boolean facts `<query verb>_<feature>_<noun>`, e.g. `saw_menu_tutorial`, `finished_checkout_tour`.
- **Idempotent writes:** design preference and settings endpoints to set explicit values (e.g. `PATCH` with the target state); never toggle; repeating a request never reverts it.
- **Resource nesting:** nest user-scoped APIs under the user, e.g. `/api/users/<user_id>/addresses`, unless the project already uses another scheme.
- **Owner only:** reach user-scoped data through the public API only as its owner (`403` for everyone else, privileged users included); put admin access in a separate admin interface. State the permission check and its tests.
- **Legacy aliases:** keep a renamed route's old path as an alias until no supported client version calls it.

## Related Skills

- `implement-spec`: how the numbered steps are executed, one pull request per step.
- `design-code`: modularity, single responsibility, and DRY in the code the spec plans.
- `write-prose`: punctuation rules for the text itself (no em dash).
