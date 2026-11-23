---
name: implement-spec
description: Rules for executing an implementation spec autonomously, step by step, commit by commit. Use when implementing a spec, implementation plan, or design doc.
metadata:
  version: "0.0.1"
---

# Implement Spec

This skill defines how to execute a spec written with the `write-spec` skill. When the project's own instructions (e.g. `CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md`) set a different convention, the project wins.

## Execution

- **Full autonomy:** solve problems yourself and carry the spec to completion without stopping to ask for the next step.
- **Allowed actions:** take the actions the work needs, e.g. fetch required data, create and run migrations, etc.
- **Machine guard:** before any action that could change a running machine (this PC or another), stop and double-check whether it affects machine state; never patch the operating system or alter machine configuration to force a fix. Log it as an unsolved issue for a human instead.
- **Obey the steps:** follow the numbered implementation steps in order.
- **Faulty design only:** change a step only when the design proves faulty; name the fault and the fix.

## Reporting

You are expected to find the optimal solution yourself most of the time. Keep a short living report throughout the active work (code, commit, push), with these three sections. Write at most one line per item.

- **Contradictions:** each contradicting topic and the fix you applied.
- **Uncertainty:** each point you were less than 70% sure about and the strategy you chose.
- **Unsolved issues:** each issue left for a human, with its temporary fix.

The human owns asking clarifying questions when something is underspecified.

## Pull Requests

- **PR per step:** each numbered step is its own pull request.
- **Single commit:** aim for one commit per pull request; add more only when the step genuinely needs them.
- **Open the PR:** after the step's commits land, push the branch and open a pull request for that step.
- **Production ready:** every commit builds and passes its tests; never commit a state that breaks the build.

## Size

- **Pull request:** keep a pull request under 2000 lines of code when possible.
- **Commit:** keep a commit under 500 lines of code when possible.

## Related Skills

- `write-spec`: the spec format and numbered steps this skill executes.
- `implement-feature`: the end-to-end workflow and definition of done for each commit.
- `commit-changes`: branch names, commit messages, and dedicated move or delete commits.
