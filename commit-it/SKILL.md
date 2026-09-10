---
name: commit-it
description: Use when committing code using git or svn.
---

# Commit it

The goal of this skill is to follow commit conventions.

# Conventional Commits — mini guide

A convention for commit messages that are readable by both humans and tools, aligned with [SemVer](https://semver.org).

```text
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

## Main types

| Type              | Usage                                                               | SemVer             |
| ----------------- | ------------------------------------------------------------------- | ------------------ |
| `feat`            | new feature                                                         | MINOR              |
| `fix`             | bug fix                                                             | PATCH              |
| `BREAKING CHANGE` | API-breaking change (in the body or footer)                         | MAJOR              |
| others            | `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `improvement` | no implicit effect |

Optional scope in parentheses: `feat(parser): add arrays`.

Use `!` before the colon to highlight a breaking change: `chore!: remove Node 6`.

## Quick rules

1. **Required** prefix: `type` + optional scope + `: ` + description.
2. Description: short summary after the space.
3. Body: after a blank line.
4. Footer: after another blank line (tickets, reviewers, breaking changes).
5. Breaking change: append `!` before the colon in the type/scope prefix, or add a `BREAKING CHANGE: <description>` footer. The footer may be omitted when `!` is used.
6. Types (except `BREAKING CHANGE`) are case-insensitive.

## Examples

```text
feat: allow config to extend other configs

BREAKING CHANGE: the `extends` key now points to another file
```

```text
chore!: remove Node 6 from the test matrix

BREAKING CHANGE: Node 6 has reached end of life
```

```text
docs: correct CHANGELOG spelling
```

```text
feat(lang): add Brazilian Portuguese translation
```

```text
fix: correct typos

see the ticket for details
closes issue #12
```

## Why use it

* Automatic CHANGELOG generation
* Automatic version bumps (`fix` → PATCH, `feat` → MINOR, breaking → MAJOR)
* Clearer history for the team
* Builds/deployments triggered by commit type

**Tip:** if a commit mixes multiple types, prefer splitting it into multiple commits. Consistency in type casing matters more than uppercase vs. lowercase.
