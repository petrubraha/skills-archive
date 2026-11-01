---
name: implement-feature
description: End-to-end workflow for adding or changing code in any repository - read the project docs, plan, implement, run static analysis, test, and update docs - plus the engineering stance, the definition of done, and how to match the surrounding code style. Use at the start of any coding task that changes source files.
metadata:
  version: "0.0.1"
---

# Implement Feature

This skill defines the workflow for any code change. The rules are project, language, and framework agnostic. When the project's own instructions set a different convention, the project wins.

## Stance

- **Live product:** assume the code runs in production, with real users and data, and that a merge may deploy automatically. Behave accordingly.
- **Next maintainer:** optimize for whoever maintains the code next, not for finishing fast.
- **Honest uncertainty:** if you haven't verified something, say so. Never present a guess as a fact, and never claim a test passed unless you ran it and read the output.

```text
# Wrong behaviour.
"Done, all tests pass." (Only the edited module's tests ran.)

# Correct behaviour.
"The 12 notification tests pass. I didn't run the full suite."
```

- **Push back:** when a request conflicts with a business rule or a security constraint, state the conflict in a sentence or two, propose the alternative, then proceed with what was asked unless it is genuinely unsafe.
- **Stay in scope:** do what was asked. Note adjacent problems instead of silently fixing them (see the `refactor-code` skill).

## Workflow

1. **Read docs first:** before planning, read the repository's agent instruction files (`CLAUDE.md`, `AGENTS.md`) to understand the architecture, guidelines, and existing API contracts.
2. **Plan:** gather the requirements and plan the change with testability in mind.
3. **Implement:** write the code, applying the coding skills listed under **Related Skills** below.
4. **Static analysis:** check code validity with the stack's dedicated tools (e.g. Pylance or `pyright` for Python, `eslint` or `tsc` for TypeScript, `flutter analyze` for Flutter) and fix what they report.
5. **Test:** create tests, run them, and fix errors until all tests pass (see the `test-code` skill).
6. **Documentation:** check whether the new code should be referenced in the docs, or whether it contradicts them. If so, add or change the feature details. If an API contract or architectural decision changes, update `CLAUDE.md` and `AGENTS.md` immediately after implementing.

## Definition of Done

Finished code meets every rule below.

- **No placeholders:** no stubs, `FIXME`s, `TODO`s, or placeholder bodies.

```python
# Wrong behaviour.
def cancel_booking(booking: Booking) -> None:
    # TODO: notify the guide.
    booking.status = BookingStatus.CANCELLED
    booking.save()

# Correct behaviour.
def cancel_booking(booking: Booking) -> None:
    booking.status = BookingStatus.CANCELLED
    booking.save()
    notify_guide(booking)
```

- **No exposed secrets:** never commit `.env` or other secret files; never log or return raw tokens, passwords, or API keys.

```python
# Wrong behaviour.
return Response({"status": "linked", "access_token": access_token})

# Correct behaviour.
return Response({"status": "linked"})
```

- **Security intact:** never bypass or remove security mechanisms (middleware, permission checks, rate limits, honeypot routes).
- **Contracts kept:** never break a public contract (response shapes, field casing, routes) that existing clients depend on, especially clients you can't redeploy on demand, such as mobile apps. Change a contract only when the task asks for it, and keep legacy aliases.

## Context

- **Indentation:** use the surrounding code's indentation style.
- **Casing:** use the surrounding code's casing.
- **Debt exception:** don't copy existing style that suffers from technical debt. Write new code with best practices in mind and never lower your standards. Consider refactoring when appropriate (see the `refactor-code` skill).

```python
# Wrong behaviour (the module uses 4-space indentation and snake_case).
def getTotal(items):
  return sum(item.price for item in items)

# Correct behaviour.
def get_total(items):
    return sum(item.price for item in items)
```

## Related Skills

Apply these while implementing:

- `design-code`: modularity, single responsibility, DRY, one step per line, constants.
- `name-identifiers`: descriptive names, no abbreviations.
- `structure-functions`: parameter count, boolean parameters, function length.
- `structure-classes`: class length, one class per file, no type switches.
- `organize-files`: file length, package exports, whitespace, scripts.
- `sort-imports`: import grouping, order, and paths.
- `annotate-types`: type annotations.
- `write-comments`, `write-logs`, `write-errors`: message and comment style.
- `write-prose`: punctuation in any human-readable text.
- `localize-text`: languages, translation catalogs, and timezone.
- `refactor-code`: when and how far to refactor.
- `commit-changes`: branch names and commit messages.
- `review-changes`: re-review the finished change when asked.
