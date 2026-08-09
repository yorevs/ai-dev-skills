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
* Do not amend commits unless explicitly requested. Never commit code if not direct asked for (don't use the history for that. Committing is always a new prompt I send).
* Treat unexpected files and working-tree changes as user-owned. Do not revert unrelated changes, remove untracked files, or clean unstaged changes without permission.


---


## Strict Scope Restriction

Every feature, fix, update, or task must be executed **strictly according to the description and requirements provided by the user**.

### Define the Scope First

Before analyzing the implementation or modifying any code, files, configuration, or system behavior, your **first reasoning activity must be to clearly define the scope of the task**.

Only consider something in scope when it has been **explicitly requested by the user**.

Do not expand the scope based on assumptions, inferred intent, best practices, personal preferences, improvement opportunities, or conclusions about what "should probably" be changed.

### Execute Strictly Within Scope

Implement only the changes required to satisfy the explicit requirements of the task.

Do not independently perform:

* Unrequested refactoring;
* Architectural improvements;
* Style or organizational changes;
* Optimizations;
* Unrequested behavioral changes;
* Fixes for adjacent or unrelated issues;
* Renaming;
* Code or file restructuring;
* Dependency updates;
* Changes to interfaces, contracts, or APIs;
* Any other modification that is not required to fulfill the defined scope.

The fact that a change appears "better", "cleaner", "more correct", "more modern", or "recommended" **does not make it part of the scope**.


### Out-of-Scope Changes

If, during execution, you determine that an out-of-scope change is genuinely required to complete the task correctly:

1. **Do not make the change immediately.**
2. Clearly inform the user about the additional change that would be required.
3. Explain objectively why it is necessary and how it relates to the original task.
4. Wait for the user's explicit authorization before making that change.

Out-of-scope changes must never be performed silently.


### Decision Rule

Whenever there is uncertainty about a modification:

**If it was not explicitly requested and is not strictly required to fulfill the described requirement, do not make it.**

The priority is to **preserve everything outside the task's scope**, modifying only the minimum necessary to satisfy exactly what the user requested.


---


# Execution Workflow

1. **Do not manufacture issues:** If something is good, accept it as good. If it is flawed, report it. For borderline issues, report them according to their actual severity.
2. **Define the scope:** Define the scope for the new feature or update strictly.
3. **Confidence Level:** Reasoning until you have > 95% confidence about the change, specially fixing BUGs or issues to avoid re-working on the same issue over and over. If the cause has multiple possibilities, narrow them down, until you have the confidence required of > 95%.
4. Always notify the User when changes require any of the following:
  * Restarting the web application
  * Restarting the backend service
  * Regenerating the database
  * Clearing the cache
  * Any other required post-deployment actions
