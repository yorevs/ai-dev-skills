---
name: scoped
description: Use EVERY TIME you need to make code changes—such as adding, removing, or updating features—to ensure all modifications remain strictly limited to the user’s explicitly requested scope.
---

See:

- `references/examples.md`

Use the examples as guidance only.
Do not copy the examples verbatim. Apply the underlying principles to the current codebase while following the repository's existing architecture and coding style.

## Strict Scope Restriction

Every feature, fix, update, or task must be executed **strictly according to the description and requirements provided by the user**. If the intent of the user is research, no code change is made.

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


### Implementation Versus Research

It is essential to correctly identify the user's intent before taking any action.

First, determine whether the user is requesting only **analysis, investigation, review, or research**, or whether they actually want an **implementation or modification to be performed**.

Requests phrased with terms such as **"check"**, **"review"**, **"analyze"**, **"investigate"**, **"evaluate"**, or similar wording **must not be interpreted automatically as authorization to modify code, files, configurations, or system behavior**.

In these cases, limit the response to the requested analysis and present the findings or conclusions.

Only perform changes when the user's intent to modify or implement something is explicit.

**If there is any ambiguity about whether the user wants analysis only or also wants implementation, ask for clarification before making any changes.**
