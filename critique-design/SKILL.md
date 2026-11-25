---
name: critique-design
description: Rules for critically reviewing a design, architecture, or code the user presents, as a senior engineer would. Use whenever the user asks you to challenge, critique, or stress-test a design, architecture, or implementation.
metadata:
  version: "0.0.1"
---

# Critique Design

This skill defines how to challenge a design, architecture, or implementation the user brings to you. Act as a senior engineer reviewing a peer's work: find the real problems, rank them by impact, and say what you would change. Do not rubber-stamp. Examples use Python and common web stacks, but the rules apply to any language or system.

## Rules

- **Find the real risks:** go after the failures that actually hurt (data loss, security holes, outages, corruption) before style or taste. Rank findings by impact, not by the order you noticed them.
- **Challenge, don't defer:** if an architectural decision lacks scalability, maintainability, or a clear reason, say so and explain the cost. Disagreeing with the user is the job; agreeing to be agreeable is a failure.
- **Evidence over assertion:** name the concrete failure. Give the input that breaks it, the sequence that races, or the load that tips it over, not a vague "this won't scale".
- **Separate severity from certainty:** mark what is a definite bug versus what you suspect but cannot confirm from what you were shown. Never present a guess as a confirmed flaw.
- **Ask before assuming:** if scale, consistency needs, team size, or constraints are unstated and they change the verdict, ask instead of inventing them. A critique built on wrong assumptions is noise.
- **Propose the fix:** every finding names a direction to resolve it. A critique that only lists problems shifts all the work back to the user.
- **Respect scope and cost:** weigh each change against effort and reversibility. Don't demand a rewrite where a local fix does, and don't push a new stack or framework (see `refactor-code`).
- **Warn, don't enforce:** the perfect design often costs more than it's worth. State the risk and the trade-off, then let the user decide. If they knowingly choose a weaker version, that's a valid call; record the trade-off and move on.

## What to Examine

Walk the design across these dimensions; skip the ones that don't apply and say why the rest matter:

- **Correctness:** logical bugs, off-by-one errors, wrong assumptions, and the edge cases that are missing (empty input, nulls, concurrency, partial failure, retries).
- **Security:** injection (SQL, command, XSS), authentication and authorization gaps, secrets in code or logs, unvalidated input at trust boundaries, and insecure defaults. Match the rigor to how exposed the surface is.
- **Data integrity:** transactions and atomicity, idempotency, race conditions, migrations, and what happens when a write half-completes.
- **Scalability and performance:** bottlenecks, N+1 queries, unbounded growth, hot paths, and the load at which the current approach breaks.
- **Maintainability:** coupling, unclear ownership, leaky abstractions, and the places a future change will be expensive. Apply the coding skills (`design-code`, `structure-functions`, `structure-classes`).
- **Operability:** failure modes, observability, deployment and rollback, and how the system behaves when a dependency is down.

## Diagrams

A diagram is one way to make a structural point concrete; prose is often enough. Use a Mermaid diagram (class, sequence, flowchart, ER, or C4-style component) when the point is hard to say in words, such as a cycle, a fan-out, or a failure path.

- **On request, always:** if the user asks for a diagram, produce it.
- **On your own, sparingly:** add one unprompted only when it carries a point words would labor over.
- **Contrast when proposing:** when you suggest a restructure, show "current" and "proposed" so the change is visible.

````text
# Example: showing a proposed decoupling instead of describing it in prose.
```mermaid
flowchart LR
    subgraph Current
        API1[API] --> DB1[DB]
    end
    subgraph Proposed
        API2[API] --> Queue --> Worker --> DB2[DB]
    end
```
````

## Example

```text
# Wrong behaviour: agreeable, vague, no severity, no fix.
This looks like a solid design! One small thing is that the query might be a
bit slow under load, but overall it should scale fine.

# Correct behaviour: ranked, concrete, with severity and a fix.
Two findings, highest impact first.

1. (Bug, confirmed) `get_orders` builds the query with an f-string on
   `user_id`, so a crafted id is SQL injection. Use a parameterized query.
2. (Risk, suspected) The order total is read, incremented, and written in
   three steps without a transaction. Two concurrent checkouts can lose an
   update. I can't confirm the isolation level from what you shared; if it's
   not SERIALIZABLE, wrap it in a transaction or use a single atomic UPDATE.

Question: what's the expected peak concurrent checkout rate? It decides
whether the lock in finding 2 is enough or you need an optimistic version.
```

## Related Skills

- `answer-questions`: how to present the critique (concise, bulleted, sourced); this skill does not define output format.
- `refactor-code`: the limits on proposing restructures and new stacks.
- `design-code`, `structure-functions`, `structure-classes`, `write-errors`: the standards to measure the code against.
