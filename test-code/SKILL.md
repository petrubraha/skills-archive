---
name: test-code
description: Workflow for writing, running, and fixing unit tests, with mocks, test scope, and coverage. Use when code needs tests, when tests fail, or when asked to run tests or report coverage.
metadata:
  version: "0.0.1"
---

# Test Code

This skill defines the standard workflow and best practices for writing, executing, and fixing unit tests.

## Workflow

When assigned a testing task, follow this strict loop until all tests pass and coverage goals are met:

1. **Write tests:** implement the initial unit tests.
2. **Run tests:** run the tests in scope (see **Test Scope** below) and observe the results.
3. **Check for errors:**
   - If tests fail because the _test code is incorrect_ (e.g. wrong mock, bad assertion), fix the test.
   - If tests fail because the _source code is incorrect_ (e.g. bug, unexpected behavior), fix the source code.
4. **Rerun:** execute the tests again.
5. **Repeat:** loop through steps 2 to 4 until there are no errors.
6. **Report coverage:** generate a test coverage report and ensure the coverage goals are met. If they are not met, return to step 1 and write additional tests.

## Proper Isolation (Mocks, Patches, and Fake Databases)

Tests must be fast, deterministic, and fully isolated from the main environment.

- **No main database:** never create or modify records in the main production or development database.
- **Fake database:** use in-memory databases or dedicated test databases whenever possible.
- **Mock dependencies:** mock external dependencies, e.g. payment providers, email services, SMS gateways, etc.
- **Mock models:** when a database interaction is not the focus of the test, mock the database models to avoid hitting any database.

## Test Scope

Run only the tests that cover the change: the test modules for the code you touched, plus any tests that import, mock, or patch it.

Run the full suite when the user asks for it, or when the change has a wide blast radius, that is, code that much of the project depends on implicitly. Typical cases:

- Data schema or persistence layer (models, migrations, ORM mappings).
- Global configuration (settings, environment loading, dependency injection wiring).
- Cross-cutting hooks that run on every request or event (middleware, interceptors, event listeners).
- Shared modules that re-export or are imported almost everywhere (barrel or index files, common utilities, base classes, etc.).
- Moving or renaming a symbol that is imported across many modules.

Check the stack's reference file for its concrete wide-reach paths.

## Dependencies

Before running tests or gathering coverage, verify that the required testing and coverage tools are installed in the current environment (e.g., `requirements.txt`, `package.json`, etc.).
If they are missing, install them using the appropriate package manager.

## Test Commands

Always execute tests using the standard test runner for the specific technology stack. Ensure you are running it within the correct isolated environment (e.g., virtualenv, Docker container) if available.

## Coverage Commands

Test coverage measures how much of the source code is executed by the tests. Always generate a coverage report after the tests pass to ensure your coverage goals (e.g., 80%) are met.

## Technology-Specific References

For specific command examples, mock patterns, and dependency information, refer to the files in the `references/` directory depending on your current stack.

## Related Skills

- `implement-feature`: the end-to-end workflow that calls this skill for the test step.
- `write-spec`: where the spec sets the test kinds and coverage thresholds this skill enforces.
