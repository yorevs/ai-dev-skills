---
name: de-slop-tests
description: Use when reorganizing or splitting oversized test suites. Refactor tests into cohesive, feature-focused files, preserve all behavioral coverage and assertions, and never modify production code.
---

# Test De-Slop Skill

You are working within the target repository.

Your goal is to improve the maintainability of oversized test suites by splitting them into cohesive, feature-focused test files while preserving all existing behavior.

Refactoring tests is **not** about creating more files—it is about making tests easier to understand, navigate, and extend.

See:

- `references/examples.md`

Use the examples as guidance only.
Do not copy the examples verbatim. Apply the underlying principles to the current codebase while following the repository's existing architecture and coding style.

---

# Scope

Focus only on:

* The oversized test suite
* The production feature or module that the test suite covers

---

# Hard Rules

Do **not** modify production or application code.

Only the following may be changed:

* Test files
* Test helper files
* Test fixtures (only if the repository already uses fixtures)

Production behavior must remain unchanged.

---

# Forbidden

Never:

* Add `skip`
* Add `ignore`
* Disable assertions
* Weaken tests simply to make them pass
* Delete behavioral coverage
* Modify production code
* Introduce temporary workarounds
* Add snapshots unless the repository already uses snapshot testing
* Silently change expected behavior

---

# Core Principles

## Preserve Behavior

The refactoring should improve structure—not functionality.

Every passing test before the refactor should continue to pass afterward.

---

## Feature-Oriented Organization

Split tests by feature or business behavior—not by technical category.

Prefer:

```text
auth/
api/
search/
config/
plugin/
theme/
tables/
integration/
```

Adapt the names to the domain being tested.

If the repository already has an established organization, follow that convention.

---

## Cohesion Over Splitting

Do not split tests simply because a file is large.

Each extracted test file should represent one cohesive feature.

A larger cohesive file is preferable to multiple fragmented files with unclear ownership.

Aim to keep files below **~1000 lines**, but treat this as a guideline rather than a strict limit.

---

## Preserve Test Intent

Keep existing test names whenever practical.

This preserves:

* Focused test filters
* CI workflows
* IDE navigation
* Historical debugging

Rename tests only when doing so significantly improves clarity.

---

## Prefer Shared Helpers Carefully

Extract repeated setup only when it genuinely reduces duplication.

Do **not** create helper functions that hide important behavior.

Good helpers:

* Object builders
* Common fixtures
* Repeated environment setup
* Repeated assertions that represent a single concept

Avoid extracting one-line helpers or helpers that make tests harder to read.

Tests should remain explicit.

---

## Avoid Testing Implementation Details

Prefer testing:

* Observable behavior
* Public APIs
* Business rules
* Integration between components

Avoid testing:

* Private methods
* Internal implementation details
* Temporary variable values
* Incidental implementation structure

---

## Strengthen Tests When Appropriate

If brittle assertions exist, replace them only when the replacement is stronger.

Prefer:

* Behavioral assertions
* State verification
* Integration verification

Avoid asserting hardcoded strings unless the string itself is part of the intended behavior.

---

# Refactoring Workflow

## First Pass

Inspect the current test architecture.

Identify:

* Feature groups
* Repeated setup
* Duplicated helpers
* Common fixtures

---

## Second Pass

Group tests by cohesive behavior.

Examples:

* Configuration
* Validation
* Rendering
* Parsing
* Authentication
* API behavior

Use the project's domain rather than generic categories whenever possible.

---

## Third Pass

Extract shared helpers only when they clearly improve readability and reduce duplication.

Helper names should be:

* Descriptive
* Boring
* Obvious

Avoid generic names like:

* Utils
* Common
* Helpers
* Misc

Prefer names that describe exactly what they build or verify.

---

## Fourth Pass

Verify:

* Every test still exists
* No assertions were weakened
* No behavioral coverage was lost
* No unnecessary abstraction was introduced
* Every new file has a clear responsibility

---

# File Size

Aim for files under **~1000 lines**.

If one cohesive feature would exceed this size, split it by atomic sub-feature.

Do not split files purely to satisfy the line-count guideline.

---

# Verification

Before finishing:

1. Run focused tests first.
2. Run the affected feature suite.
3. Run the project's documented top-level test command when practical.
4. Run formatting or linting if the repository normally requires it.

Confirm:

* All affected tests pass
* No production files were modified
* No skips or ignores were introduced
* No to-do workarounds were added
* All extracted test files remain reasonably sized

Report:

* The exact commands executed
* The result of each command
* Any remaining known limitations

---

# Existing Changes

If production files were already modified before you started, leave them untouched.

Do not revert unrelated work.

Only modify and report changes related to the test refactoring.

---

# Success Criteria

A successful refactor should:

* Preserve behavior
* Improve readability
* Improve discoverability
* Reduce duplication
* Reduce file size where appropriate
* Maintain stable test names whenever practical
* Make future additions easier without increasing coupling

The best test architecture is one where each file clearly owns a single feature, helpers remain minimal, and the intent of every test is immediately obvious.

---

# Repository Conventions

## Follow Existing Style Rules

Before modifying any files, inspect the repository for project style and formatting configuration.

Examples include:

- `checkstyle.xml`
- `checkstyle/**/*.xml`
- `.editorconfig`
- `.clang-format`
- `.prettierrc`
- `pyproject.toml`
- `.eslintrc*`
- Any language-specific formatting or lint configuration

Use the repository's existing conventions as the source of truth.

When a Checkstyle configuration exists, treat it as authoritative for the files it governs.
