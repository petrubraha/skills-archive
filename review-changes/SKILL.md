---
name: review-changes
description: Static self-review of a finished change using git status and git diff, then an honest summary. Use when asked to review or re-review your own work.
metadata:
  version: "0.0.1"
---

# Review Changes

This skill defines how to re-review your own change once the work is done (code written, tests run, tools called). The review is static: read the change, don't re-run the work.

## Gather the Change

Build the review from deterministic tools, never from memory of what you think you changed:

- **Changed files:** `git status` lists every changed file, including untracked ones.
- **Unstaged diff:** `git diff` shows unstaged edits.
- **Staged diff:** `git diff --staged` shows staged edits.
- **Untracked files:** read each new file in full; `git diff` doesn't show them.
- **Size check:** `git diff --stat` spots files you didn't mean to touch.

```text
# Wrong behaviour.
"I changed the serializer and its test, so the review is done."

# Correct behaviour.
Run `git status` and `git diff`, notice an untracked debug script and an
unrelated whitespace change in another module, then remove both.
```

## Review the Change

Read the diff as if reviewing someone else's pull request. Look for:

- **Leftovers:** debugging code, commented-out code, temporary files, etc.
- **Unrelated edits:** changes outside the scope of the request.
- **Secrets:** keys, tokens, `.env` content, etc.
- **Broken references:** missing or broken imports, a symbol you forgot to export, renamed names still used elsewhere.
- **Rule violations:** the coding skills (`design-code`, `structure-functions`, `write-prose`, etc.) applied to the changed lines.

## Summarize

Then summarize honestly:

- **Changed:** what you changed.
- **Verified:** what you verified, and how.
- **Not verified:** what you did **not** verify.
- **Decisions:** anything the user should decide.
