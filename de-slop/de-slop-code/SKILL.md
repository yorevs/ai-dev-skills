---
name: de-slop-code
description: Use when refactoring oversized, duplicated, tightly coupled, or poorly organized production code. Split code into cohesive, feature-oriented components while preserving behavior. Do not use for test-only restructuring; use de-slop-tests instead.
---

# De-Slop Skill

The goal of this skill is to continuously improve the architecture of the codebase by reducing complexity, increasing cohesion, and making future changes easier.

Refactoring is **not** about moving code into more files. It is about improving the structure of the system while preserving behavior.

See:

- `references/solid-python.md`
- `references/solid-java.md`

Use the examples as guidance only. Apply SOLID principles when they improve the design; do not introduce abstractions mechanically.
Do not copy the examples verbatim. Apply the underlying principles to the current codebase while following the repository's existing architecture and coding style.


## Core Objectives

* Keep components focused and cohesive.
* Prefer feature-oriented organization over technical-layer organization.
* Reduce coupling and increase cohesion.
* Eliminate duplication when it represents the same business concept.
* Preserve existing behavior unless explicitly requested otherwise.

### File Size

Aim to keep source files under **~1000 lines of code**.

This is a guideline—not a hard rule.

Do **not** split cohesive code solely to satisfy a line count. A slightly larger cohesive file is preferable to several fragmented files with unclear responsibilities.

---

# SOLID Principles

Apply SOLID principles whenever they improve maintainability, readability, or extensibility.

## Single Responsibility Principle (SRP)

A component should have **one reason to change**.

Each file, class, or module should represent one cohesive concept.

## Open/Closed Principle (OCP)

Components should be open for extension but closed for modification.

New behavior should preferably be added by composing or extending existing code rather than modifying stable implementations.

## Liskov Substitution Principle (LSP)

Derived implementations must honor the contract of their abstractions.

Substituting one implementation for another should never change the correctness of the system.

## Interface Segregation Principle (ISP)

Prefer multiple small, focused interfaces over large, general-purpose ones.

Do not force consumers to depend on functionality they do not use.

## Dependency Inversion Principle (DIP)

High-level modules should depend on abstractions rather than concrete implementations.

Infrastructure should depend on domain logic—not the other way around.

---

# Design Principles

## Simplicity First

Avoid introducing abstractions until there is a demonstrated need.

Do **not** create:

* Interfaces with only one implementation
* Factories that construct a single class
* Strategies with only one strategy
* Services that simply forward calls

Unless, they clearly improve the architecture.

The simplest solution that remains maintainable is usually the best one.

---

## Patterns Are Tools

Design patterns exist to solve problems.

Do **not** introduce a design pattern simply because one exists.

When a simpler solution adequately solves the problem, prefer the simpler solution.

---

## Vertical Feature Organization

Prefer organizing code by feature (domain) rather than by technical layer.

Prefer:

```
aliases/
    renderer
    runner
    presenter
```

instead of:

```
renderers/
runners/
presenters/
```

Feature-oriented organization improves discoverability, extensibility, and cohesion.

---

## Cohesion Over Extraction

Before extracting code into a new component, verify that it represents a cohesive responsibility rather than simply reducing file size.

Extraction should improve:

* Readability
* Reuse
* Ownership
* Maintainability

If it merely moves code elsewhere, do not extract it.

---

## Avoid Premature Reuse

Only extract shared components when they represent the same business concept.

Similar-looking code is **not** necessarily duplicate code.

Avoid creating abstractions based solely on implementation similarity.

---

## Stop Extracting When Appropriate

Stop decomposing once components have:

* A clear responsibility
* Reasonable size
* Good readability
* Low coupling

Further decomposition should provide clear architectural value.

Do not split components indefinitely.

---

# Refactoring Workflow

When analyzing a large file:

## First Pass

Study the file.

Identify logical sections grouped by responsibility.

Produce a list of methods grouped by existing functionality.

---

## Second Pass

Identify opportunities to extract cohesive components.

For each extraction explain:

* Responsibility
* Dependencies
* Expected public interface
* Expected reuse

---

## Third Pass

Group the extracted components into higher-level features.

Favor vertical slices over technical layers.

---

## Fourth Pass

Verify:

* Dependencies flow in one direction
* No circular imports
* Responsibilities remain cohesive
* Duplication has been reduced
* Readability has improved

---

# Dependency Rules

Avoid circular dependencies.

Prefer solving dependency issues through:

* Better dependency direction
* Dependency injection
* Shared abstractions
* Composition
* Event-driven communication (when appropriate)

Event-driven architecture is **one** solution—not the default solution.

---

# Error Handling

Prefer explicit failures over silent fallbacks.

Raise exceptions when invariants are violated.

Only introduce fallbacks when they represent intentional business requirements.

If a fallback changes system behavior or hides an error, ask the user before implementing it.

Never silently ignore failures.

---

# Legacy Code

Do **not** introduce:

* Backward compatibility layers
* Legacy wrappers
* Transitional code
* Deprecated APIs

Unless explicitly requested.

If preserving legacy behavior appears necessary, explain why and ask the user before proceeding.

---

# New Code

When writing new code:

* Follow the existing project style.
* If a formatting or checkstyle configuration exists, treat it as the source of truth.
* Follow SOLID principles where they improve the design.
* Keep components cohesive.
* Prefer composition over inheritance.
* Favor readability over cleverness.

---

# Naming

Names should describe business concepts rather than implementation details.

Prefer:

* AliasRepository
* SettingsImporter
* ConfigValidator

Avoid generic names like:

* Utils
* Helpers
* Common
* Shared
* Misc
* Manager2
* BaseThing

Every component should communicate its purpose through its name.

---

# Grouping Directives

## Poor Grouping

Given:

* render_aliases_table

* render_settings_table

* render_configs_table

* run_aliases_proc

* run_settings_proc

* run_configs_proc

* display_aliases_results

* display_settings_results

* display_configs_results

Grouping by implementation:

```
Renderers
Runners
Displays
```

This creates unnecessary coupling because adding a new feature requires modifying several unrelated files.

---

## Preferred Grouping

Instead, organize by feature:

```
Aliases
    render
    run
    display

Settings
    render
    run
    display

Configs
    render
    run
    display
```

Each feature owns its complete workflow.

Adding a new capability should primarily involve adding or modifying code within that feature rather than touching multiple unrelated modules.

---

# Extraction Checklist

Before creating a new component, verify:

* Does it have one clear responsibility?
* Can it be described with a single meaningful name?
* Does extraction improve readability?
* Does extraction reduce coupling?
* Does extraction improve cohesion?
* Is it likely to be reused?
* Does it avoid circular dependencies?

If most answers are **No**, do not extract it.

---

# Troubleshooting

When debugging:

* Narrow the possible causes until you are at least **95–100%** confident in the root cause.
* Do not stop at the first plausible explanation.
* Consider hidden interactions, recent changes, and indirect dependencies.
* If previous approaches failed, investigate alternative hypotheses.
* Use Git history to identify regressions when appropriate.

Avoid guessing.

---

# Testing

Tests should verify behavior—not implementation details.

Prefer:

* business logic
* observable behavior
* integration between components
* edge cases
* failure scenarios

Avoid:

* Asserting hardcoded strings that have no behavioral significance
* Testing private implementation details
* Tests tightly coupled to internal structure

When refactoring:

* Existing behavior must remain unchanged.
* Existing tests should continue to pass.
* New components should remain covered by existing tests or by new tests where appropriate.

A successful refactor improves architecture without changing externally observable behavior.

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
