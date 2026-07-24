## Test Splitting Rule

You are working in the target repository.

### Goal

Refactor and organize an oversized test suite by splitting it into smaller, feature-focused test files.

Focus only on the relevant test suite and the production file or feature area that the tests currently cover.

### Hard Rule

Do not modify production or application code.

Only test files, test helper files, and test fixtures may be changed.

### Allowed Edits

You may edit:

* The existing oversized test file
* New test files under the appropriate test directory
* New test helper files under the existing test helper location
* Existing test fixtures, only if the repository already treats them as fixtures

### Forbidden

Do not:

* Add skip directives
* Add ignore directives
* Disable assertions
* Weaken tests just to make them pass
* Delete behavioral coverage
* Modify production code
* Make unrelated formatting changes
* Add generated snapshots unless snapshots are already part of the test style

### Primary Strategy

Split tests by feature or behavior, not by generic test type.

Prefer names such as:

* `core`
* `config`
* `search`
* `theme`
* `plugin`
* `integration`
* `auth`
* `api`
* `ui`
* `tables`

Adapt names to the actual domain being tested.

If the repository already has a test organization convention, follow the existing convention instead.

### Implementation Rules

1. Inspect the current test architecture before editing.
2. Preserve every test’s behavior and assertions.
3. Only replace brittle hardcoded assertions when replacing them with stronger logic or integration checks.
4. Extract repeated setup into explicit test helper functions.
5. Keep helper names clear, boring, and descriptive.
6. Keep every test file below 1,000 lines.
7. If one feature file would exceed 1,000 lines, split it by atomic sub-feature.
8. Keep test names stable where possible so focused test filters remain useful.
9. Do not add skips, bypasses, conditional ignores, or temporary workarounds.
10. Do not touch application code to satisfy tests.

### Verification Required

Run targeted checks first, then all affected tests.

At minimum, run:

* The original test file, if it still exists
* The new split test directory or files
* Any documented top-level test command for this suite
* Focused test filters when useful for faster iteration

Before finishing:

* Run the repository’s diff or formatting sanity check, if available.
* Confirm no production files were changed.
* Confirm no skip, ignore, disable, TODO-to-fix-later, or equivalent bypass was added.
* Confirm all new test files are below 1,000 lines.
* Report the exact test commands run and their results.

### Important

If production files were already modified before starting, leave them untouched and do not revert them.

Only modify and report test-related changes.
