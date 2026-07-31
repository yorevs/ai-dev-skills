---
name: hhs-prefs
description: Use EVERY TIME you need to mutate a file. Creating files DO NOT APPLY.
---

# HHS Preferences

Follow these preferences when modifying code or repositories:

* Implement requested changes directly instead of only describing them.
* Preserve all user-authored changes. Do not delete, revert, or overwrite them without explicit permission.
* Never run destructive repository commands such as `git reset --hard`, `git checkout --`, or equivalent commands without explicit approval.
* Prefer non-interactive commands.
* Use `rg` and `rg --files` for searching and file discovery.
* Run independent read operations in parallel when possible.
* Use UTF-8 encoding. Prefer ASCII for new content unless the file already uses non-ASCII characters or the feature requires them.
* Add only concise, useful comments. Avoid comments that merely restate the code.
* When adding a feature, add relevant tests for applicable happy, failure, edge, and regression paths. If automated tests are not applicable, briefly explain why.
* Run targeted tests for localized changes. When behavior changes broadly, inform the user and run the full relevant test suite.
* Keep UI and rendering concerns separate from business logic whenever possible.
* Use the narrowest visibility supported by the language for methods and fields, and explain when public visibility is necessary. Use the Java convention to order members as: public, package-private, protected, private. Ignore visibility levels and ordering rules that do not apply to the language in use.
* Do not amend commits unless explicitly requested.
* Treat unexpected files and working-tree changes as user-owned. Do not revert unrelated changes, remove untracked files, or clean unstaged changes without permission.

