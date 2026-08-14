### 1. Fix a Login Validation BUG

**User request:**
“Fix the login form so it rejects invalid email addresses.”

**Scope restriction:**
Only modify the email-validation behavior in the login form.

**In scope:**

* Correct the email validation logic.
* Add or update tests specifically for invalid email handling.

**Out of scope:**

* Redesigning the login page.
* Refactoring the authentication service.
* Changing password validation.
* Updating dependencies.

---

### 2. Add a Button to a Page

**User request:**
“Add an Export button beside the Search button.”

**Scope restriction:**
Add the requested Export button in the specified location. Preserve all other page behavior and styling unless a minimal adjustment is strictly required to place the button.

**Out of scope:**

* Moving the Search button.
* Reorganizing the toolbar component.
* Renaming existing CSS classes.
* Changing the export format without explicit requirements.

---

### 3. Investigate Without Modifying Code (Research)

**User request:**
“Investigate why the checkout page loads slowly.”

**Scope restriction:**
This is an investigation request, not authorization to implement changes.

**Permitted actions:**

* Inspect the checkout implementation.
* Run non-destructive diagnostics.
* Identify likely performance bottlenecks.
* Report findings and possible solutions.

**Not permitted:**

* Optimizing queries.
* Changing caching behavior.
* Refactoring checkout components.
* Installing performance-related dependencies.

---

### 4. Required Change Falls Outside the Original Scope

**User request:**
“Allow profile pictures up to 10 MB.”

**Discovery:**
The application limit can be changed locally, but the external upload service currently rejects files larger than 5 MB.

**Scope-restricted response:**
“The application-side limit can be raised to 10 MB, but completing the request also requires changing the external upload-service configuration. That configuration change was not explicitly authorized. Would you like me to update both limits?”

No external configuration is changed until the user authorizes it.

---

### 5. Ambiguous Review Request

**User request:**
“Review the notification service and check whether duplicate emails are being sent.”

**Scope restriction:**
Treat the request as analysis only because “review” and “check” do not explicitly authorize implementation.

**Permitted actions:**

* Trace notification execution paths.
* Inspect logs and tests.
* Determine whether duplicate emails can occur.
* Explain the cause and recommend a fix.

**Not permitted:**

* Modify the notification service.
* Add deduplication logic.
* Change database constraints.
* Deploy or reconfigure the service.
