---
name: implement-feature
description: End-to-end workflow (plan, implement, test, etc.) and definition of done for any code change. Use at the start of any coding task that changes source files.
metadata:
  version: "0.0.1"
---

# Implement Feature

This skill defines the workflow for any code change. When the project's own instructions set a different convention, the project wins.

## Stance

- **Live product:** assume the code runs in production, with real users and data, and that a merge may deploy automatically. Behave accordingly.
- **Next maintainer:** optimize for whoever maintains the code next, not for finishing fast.
- **Honest uncertainty:** if you haven't verified something, say so. Never present a guess as a fact, and never claim a test passed unless you ran it and read the output.
- **Keep moving:** when a request conflicts with a business rule or a security constraint, find the solution yourself and proceed; stop only when the work is genuinely unsafe. Record the conflict and your fix in the report (see the `implement-spec` skill) instead of pausing to ask.
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

- **No unfinished work:** fully implement the behavior this change owns; no stubs or fake return values standing in for it. A `TODO` or `FIXME` is allowed only for tracked, out-of-scope follow-up and must reference the issue.

```python
# Wrong behaviour (the refund is this change's job, not follow-up).
def cancel_order(order: Order) -> None:
    # TODO: refund the customer.
    order.status = OrderStatus.CANCELLED
    order.save()

# Correct behaviour.
def cancel_order(order: Order) -> None:
    order.status = OrderStatus.CANCELLED
    order.save()
    refund_customer(order)
```

- **No exposed secrets:** never commit `.env` or other secret files; never log or return raw tokens, passwords, or API keys.

```python
# Wrong behaviour.
return Response({"status": "paid", "payment_token": payment_token})

# Correct behaviour.
return Response({"status": "paid"})
```

- **Security intact:** never bypass or remove security mechanisms (middleware, permission checks, rate limits, etc.).
- **No production mocks:** keep mocks, fakes, and stubbed responses in tests; never ship them in production code paths.

```python
# Wrong behaviour (ships a fake in a production path).
def fetch_exchange_rate(currency: str) -> float:
    return 1.0  # mock until the rates API is ready

# Correct behaviour.
def fetch_exchange_rate(currency: str) -> float:
    return rates_client.get(currency)
```

- **Contracts kept:** never break a public contract (response shapes, field casing, routes) that existing clients depend on, especially clients you can't redeploy on demand, such as mobile apps. Change a contract only when the task asks for it, and keep legacy aliases.

## Context

- **Indentation:** use the surrounding code's indentation style.
- **Casing:** use the surrounding code's casing.
- **No esoteric code:** write for the next maintainer. Choose the plain, obvious construct over a clever one; avoid obscure language tricks, strange operators (e.g. `>>`, `~`, `^`, walrus `:=` for control flow), dense one-liners, and implicit behaviour that forces the reader to decode intent.

```python
# Wrong behaviour.
box_count = -(-len(order.pizzas) >> 1)
totals = {o.id: [p.price for p in o.pizzas] and sum(p.price for p in o.pizzas) or 0 for o in orders}

# Correct behaviour.
PIZZAS_PER_BOX = 2
box_count = math.ceil(len(order.pizzas) / PIZZAS_PER_BOX)
totals = {}
for order in orders:
    totals[order.id] = sum(pizza.price for pizza in order.pizzas)
```

- **Debt exception:** don't copy existing style that suffers from technical debt. Write new code with best practices in mind and never lower your standards. Consider refactoring when appropriate (see the `refactor-code` skill).

```python
# Wrong behaviour (the module uses 4-space indentation and snake_case).
def getOrderTotal(pizzas):
  return sum(pizza.price for pizza in pizzas)

# Correct behaviour.
def get_order_total(pizzas):
    return sum(pizza.price for pizza in pizzas)
```

## Related Skills

Apply these while implementing:

- `design-code`: modularity, single responsibility, DRY, etc.
- `name-identifiers`: descriptive names, no abbreviations.
- `structure-functions`: parameter count, boolean parameters, function length.
- `structure-classes`: class length, one class per file, no type switches.
- `organize-files`: file length, package exports, whitespace, etc.
- `sort-imports`: import grouping, order, and paths.
- `annotate-types`: type annotations.
- `write-comments`, `write-logs`, `write-errors`: message and comment style.
- `write-prose`: punctuation in any human-readable text.
- `localize-text`: languages, translation catalogs, and timezone.
- `refactor-code`: when and how far to refactor.
- `commit-changes`: branch names and commit messages.
- `review-changes`: re-review the finished change when asked.
