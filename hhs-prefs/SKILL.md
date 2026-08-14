---
name: hhs-prefs
description: Use EVERY TIME you need to modify or delete an existing file, ensuring changes remain strictly limited to the user’s explicit scope. Does not apply when only creating new files.
---

# HHS Preferences

Follow these preferences when modifying code or repositories:

* Preserve all user-authored changes. Do not delete, revert, or overwrite them without explicit permission.
* Never run destructive commands such as `git reset --hard`, `git checkout --`, `rm -rf`, `mv -f`, or equivalent commands without explicit approval.
* Prefer non-interactive commands by using quiet flags.
* Use `fd` doe files and `rg` and for strings and file discoveries.
* Run independent read operations in parallel when possible.
* Use "UTF-8" encoding and en_Us locale. Prefer ASCII for new content unless the file already uses non-ASCII characters, Unicode, or when the feature requires them.
* Add only concise, useful comments. Avoid comments that merely restate the code.
* When adding a feature, add relevant tests for applicable happy, unhappy (failure), edge, and regression paths when the change impacts old behaviors. If automated tests are not applicable, briefly explain why.
* Run targeted tests for localized changes. When behavior changes broadly, inform the user and run the full relevant test suite.
* Keep UI and rendering concerns separate from business logic whenever possible (MVC pattern).
* Use the narrowest visibility supported by the language for methods and fields, and explain when public visibility is necessary. Use the Java convention to order members as: public, package-private, protected, private. Ignore visibility levels and ordering rules that do not apply to the language in use.
* Do not amend commits unless explicitly requested. Never commit code if not direct asked for (don't use the history for that. Committing is always a new prompt, specifically for that). When committing, check the last commit and follow the comment style.
* Treat unexpected files and working-tree changes as user-owned. Do not revert unrelated changes, remove untracked files, stash, or clean unstaged changes without asking permission for that.


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
