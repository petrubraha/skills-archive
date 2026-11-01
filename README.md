# skills-archive

A collection of [Agent Skills](https://github.com/agentskills/agentskills) that encode coding, writing, and workflow conventions for AI coding agents.

Each skill is a folder with a `SKILL.md` file (frontmatter with `name` and `description`, followed by instructions) and optional `references/`.

## Skills

- **annotate-types**: Rules for type annotations and gradual typing migration. Use when writing or changing code in an optionally typed language, such as Python, JavaScript/TypeScript, PHP, etc.
- **commit-changes**: Naming rules for git branches and commit messages, with shared type prefixes. Use whenever creating a branch or writing a commit message.
- **design-code**: Core code design rules (modularity, DRY, magic numbers, etc.). Use whenever writing or reviewing source code.
- **implement-feature**: End-to-end workflow (plan, implement, test, etc.) and definition of done for any code change. Use at the start of any coding task that changes source files.
- **localize-text**: Language, translation, and timezone rules for a codebase. Use whenever writing user-facing text (errors, API responses, UI) or handling dates and times.
- **name-identifiers**: Naming rules for variables, functions, and classes. Use whenever declaring or renaming an identifier.
- **organize-files**: File-level rules: length, package exports, developer scripts, etc. Use when creating or splitting files, editing package entry files, or writing scripts.
- **refactor-code**: Rules for when and how far to refactor existing code. Use when a change requires touching existing code, when facing technical debt, or when asked to refactor.
- **review-changes**: Static self-review of a finished change using git status and git diff, then an honest summary. Use when asked to review or re-review your own work.
- **sort-imports**: Import grouping, ordering, and path rules. Use whenever adding, moving, or reordering imports, or resolving circular imports.
- **structure-classes**: Size and design rules for classes, including polymorphism over type switches. Use whenever writing or changing a class or class hierarchy.
- **structure-functions**: Size and signature limits for functions and methods (parameters, length, etc.). Use whenever writing or changing a function or method.
- **test-code**: Workflow for writing, running, and fixing unit tests, with mocks, test scope, and coverage. Use when code needs tests, when tests fail, or when asked to run tests or report coverage.
- **write-comments**: Rules for code comments and docstrings. Use whenever adding, editing, or reviewing comments, docstrings, or doc comments.
- **write-errors**: Style rules for error messages. Use whenever raising or throwing an error, or writing an error message returned to a caller.
- **write-logs**: Style and sensitive-data rules for log messages. Use whenever adding or changing a log statement.
- **write-prose**: Punctuation and style rules for any human-readable text. Use whenever writing comments, docs, commit messages, etc.
- **write-spec**: Rules for writing an implementation spec, a step-by-step plan followed commit by commit. Use when asked to write or update a spec, implementation plan, or design doc.

## Workflow

Every skill is developed on its own branch named `feat/<skill-name>` and merged into `main` through a dedicated pull request.

## Validation

The [agentskills](https://github.com/agentskills/agentskills) repository is included as a submodule and provides the `skills-ref` validator.

```bash
git clone --recurse-submodules https://github.com/petrubraha/skills-archive.git
# or, in an existing clone
git submodule update --init

cd agentskills/skills-ref
python -m venv .venv
.venv/Scripts/activate   # Windows; use .venv/bin/activate on macOS and Linux
pip install -e .

skills-ref validate ../../<skill-name>
```
