# skills-archive

A collection of [Agent Skills](https://github.com/agentskills/agentskills) that encode coding, writing, and workflow conventions for AI coding agents.

Each skill is a folder with a `SKILL.md` file (frontmatter with `name` and `description`, followed by instructions) and optional `references/`.

## Skills

- **annotate-types**: Type annotation rules. Use when writing code in optionally typed languages like Python or TypeScript.
- **commit-changes**: Git branch and commit message naming. Use when creating a branch or commit.
- **design-code**: Core design rules (modularity, DRY, magic numbers, etc.). Use when writing or reviewing code.
- **implement-feature**: End-to-end coding workflow and definition of done. Use at the start of any coding task.
- **localize-text**: Language, translation, and timezone rules. Use for user-facing text or dates and times.
- **name-identifiers**: Naming rules for variables, functions, and classes. Use when declaring or renaming one.
- **organize-files**: File length, exports, and script placement rules. Use when creating or splitting files.
- **refactor-code**: When and how far to refactor. Use when changing existing code or facing technical debt.
- **review-changes**: Static self-review with git status and git diff. Use when asked to review your own work.
- **sort-imports**: Import grouping, ordering, and path rules. Use when adding or reordering imports.
- **structure-classes**: Class size and design rules. Use when writing or changing a class or class hierarchy.
- **structure-functions**: Function size and signature limits. Use when writing or changing a function or method.
- **test-code**: Unit testing workflow with mocks, test scope, and coverage. Use when code needs tests or tests fail.
- **write-comments**: Rules for comments and docstrings. Use when adding or editing them.
- **write-errors**: Error message style. Use when raising an error or returning an error message.
- **write-logs**: Log message style and sensitive data. Use when adding or changing a log statement.
- **write-prose**: Punctuation and style for human-readable text. Use when writing comments, docs, etc.
- **write-spec**: Rules for implementation specs. Use when asked to write or update a spec or implementation plan.

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
