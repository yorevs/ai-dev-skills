### 1. Localized Bugfix with Targeted Tests

**User request**

> Fix the validation bug in `src/email-validator.ts`. Do not change unrelated files.

**Expected behavior**

1. Inspect the target file and relevant tests.
2. Check the working tree for existing user changes.
3. Identify the root cause with high confidence.
4. Modify only the validator and applicable test file.
5. Add a regression test reproducing the bug.
6. Run the targeted validator tests.
7. Report the modified files and test results.
8. Do not commit.

**Successful outcome**

- The validation bug is fixed.
- Existing behavior remains intact.
- A regression test protects the fix.
- Unrelated changes are untouched.

---

### 2. Feature Addition Affecting Existing Behavior

**User request**

> Add support for disabling expired accounts during authentication.

**Expected behavior**

1. Define the scope around authentication and account-expiration behavior.
2. Inspect the authentication flow, domain logic, and existing tests.
3. Keep expiration logic separate from UI or rendering code.
4. Implement the smallest necessary change.
5. Add tests for:
   - Active account authentication.
   - Expired account rejection.
   - Missing expiration date.
   - Existing authentication behavior.
6. Run targeted authentication tests.
7. Run the broader relevant suite if the change affects multiple authentication paths.
8. Explain whether deployment requires a restart, migration, or cache clearing.

**Successful outcome**

- Expired accounts are rejected.
- Active accounts continue to authenticate.
- Existing behavior is protected by regression tests.
- Required operational steps are clearly stated.

---

### 3. Modifying a File That Already Contains User Changes

**Initial state**

`src/config.ts` contains uncommitted user changes unrelated to the requested task.

**User request**

> Update the retry count from three to five.

**Expected behavior**

1. Inspect the existing diff before editing.
2. Identify the exact retry-count setting.
3. Preserve all unrelated user modifications.
4. Change only the requested value.
5. Verify the resulting diff.
6. Run the narrowest applicable test or configuration check.
7. Inform the user that their existing changes were preserved.

**Successful outcome**

Only the retry-count value changes; the user’s other edits remain intact.

---

### 4. Explicitly Approved Deletion

**User request**

> Delete `src/legacy-parser.ts`. It is no longer used.

**Expected behavior**

1. Confirm the exact deletion target.
2. Search for imports, references, tests, and build configuration entries.
3. Determine whether deleting the file alone would break the project.
4. Delete the file because the user explicitly requested it.
5. Remove references only when they are necessarily part of the requested deletion.
6. Run targeted tests or builds.
7. Report everything removed.

**Successful outcome**

The obsolete file and necessary references are removed without touching unrelated files.

---

### 5. Creation-Only Request

**User request**

> Create a new `docs/api-example.md` containing a basic API example.

**Expected behavior**

The skill does not need to trigger because no existing file is being modified or deleted.

**Successful outcome**

The new file is created without unnecessary repository-wide inspection or modification.

---

### 6. User Explicitly Requests a Commit

**User request**

> Fix the parser regression and commit the change.

**Expected behavior**

1. Implement and test the requested fix.
2. Inspect the latest commit messages to determine the project’s style.
3. Review the exact files that will be committed.
4. Stage only the files belonging to the parser fix.
5. Create a new commit.
6. Do not amend an existing commit.
7. Report the new commit and test results.

**Successful outcome**

A new, narrowly scoped commit is created using the repository’s existing message style.

---

### 7. Public Visibility Required

**User request**

> Add an API that lets external modules register event handlers.

**Expected behavior**

1. Use narrow visibility for internal implementation details.
2. Make only the externally consumed registration API public.
3. Explain that public visibility is necessary because other modules must call it.
4. Follow the language’s member-ordering conventions when applicable.
5. Add API and behavior tests.

**Successful outcome**

The public surface is minimal and justified; implementation details remain private.

---

### 8. Post-Deployment Action Required

**User request**

> Change the backend configuration so uploaded files can be up to 50 MB.

**Expected behavior**

1. Modify only the relevant configuration and tests.
2. Verify that application and infrastructure limits remain compatible.
3. Run applicable configuration checks.
4. Tell the user that the backend service must be restarted if the configuration is loaded only at startup.

**Successful outcome**

The limit changes successfully, and the user receives clear restart instructions.

## Unhappy Paths

### 1. Reverting Unrelated User Changes

**User request**

> Fix the login timeout.

**Incorrect behavior**

The assistant runs:

```bash
git reset --hard
```
