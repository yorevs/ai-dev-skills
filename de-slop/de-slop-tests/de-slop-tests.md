# Test De-Slop Skill

You are working within the target repository.

Your goal is to improve the maintainability of oversized test suites by splitting them into cohesive, feature-focused test files while preserving all existing behavior.

Refactoring tests is **not** about creating more files—it is about making tests easier to understand, navigate, and extend.

---

# Scope

Focus only on:

* the oversized test suite
* the production feature or module that the test suite covers

---

# Hard Rules

Do **not** modify production or application code.

Only the following may be changed:

* test files
* test helper files
* test fixtures (only if the repository already uses fixtures)

Production behavior must remain unchanged.

---

# Forbidden

Never:

* add `skip`
* add `ignore`
* disable assertions
* weaken tests simply to make them pass
* delete behavioral coverage
* modify production code
* introduce temporary workarounds
* add snapshots unless the repository already uses snapshot testing
* silently change expected behavior

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

* focused test filters
* CI workflows
* IDE navigation
* historical debugging

Rename tests only when doing so significantly improves clarity.

---

## Prefer Shared Helpers Carefully

Extract repeated setup only when it genuinely reduces duplication.

Do **not** create helper functions that hide important behavior.

Good helpers:

* object builders
* common fixtures
* repeated environment setup
* repeated assertions that represent a single concept

Avoid extracting one-line helpers or helpers that make tests harder to read.

Tests should remain explicit.

---

## Avoid Testing Implementation Details

Prefer testing:

* observable behavior
* public APIs
* business rules
* integration between components

Avoid testing:

* private methods
* internal implementation details
* temporary variable values
* incidental implementation structure

---

## Strengthen Tests When Appropriate

If brittle assertions exist, replace them only when the replacement is stronger.

Prefer:

* behavioral assertions
* state verification
* integration verification

Avoid asserting hardcoded strings unless the string itself is part of the intended behavior.

---

# Refactoring Workflow

## First Pass

Inspect the current test architecture.

Identify:

* feature groups
* repeated setup
* duplicated helpers
* common fixtures

---

## Second Pass

Group tests by cohesive behavior.

Examples:

* configuration
* validation
* rendering
* parsing
* authentication
* API behavior

Use the project's domain rather than generic categories whenever possible.

---

## Third Pass

Extract shared helpers only when they clearly improve readability and reduce duplication.

Helper names should be:

* descriptive
* boring
* obvious

Avoid generic names like:

* utils
* common
* helpers
* misc

Prefer names that describe exactly what they build or verify.

---

## Fourth Pass

Verify:

* every test still exists
* no assertions were weakened
* no behavioral coverage was lost
* no unnecessary abstraction was introduced
* every new file has a clear responsibility

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

* all affected tests pass
* no production files were modified
* no skips or ignores were introduced
* no TODO workarounds were added
* all extracted test files remain reasonably sized

Report:

* the exact commands executed
* the result of each command
* any remaining known limitations

---

# Existing Changes

If production files were already modified before you started, leave them untouched.

Do not revert unrelated work.

Only modify and report changes related to the test refactoring.

---

# Success Criteria

A successful refactor should:

* preserve behavior
* improve readability
* improve discoverability
* reduce duplication
* reduce file size where appropriate
* maintain stable test names whenever practical
* make future additions easier without increasing coupling

The best test architecture is one where each file clearly owns a single feature, helpers remain minimal, and the intent of every test is immediately obvious.
