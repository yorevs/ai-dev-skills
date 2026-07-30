## Example 1: Stateless REST API

### System Context

* Backend REST API
* Authentication using OAuth 2.0 Bearer tokens
* No browser sessions
* No cookies
* PostgreSQL database
* Public internet exposure
* No file uploads
* No LLM integration

### Applicable Controls

* Authorization validation on every endpoint
* OAuth token validation
* SQL injection prevention
* Rate limiting
* Input validation
* Secure error handling
* TLS
* Security logging
* Dependency scanning
* Secret management

### Ignored Controls

* **CSRF Protection — Not Applicable**
  The API does not use browser cookies or implicit session credentials.

* **Secure Cookie Configuration — Not Applicable**
  The application does not use cookies.

* **File Upload Validation — Not Applicable**
  The API does not accept file uploads.

* **Prompt Injection Protection — Not Applicable**
  The system does not contain LLM or generative AI components.

### Example Report

```text
Risk: Missing authorization validation on resource endpoints
Severity: High

Description:
Authenticated users can request resources belonging to other users by modifying the resource identifier.

Recommendation:
Validate resource ownership or authorization policy on every request.

Applicable controls:
- Object-level authorization
- Audit logging
- Automated authorization tests

Ignored controls:
- CSRF protection: Not applicable because authentication uses Bearer tokens instead of browser cookies.
- File upload security: Not applicable because the system does not accept uploaded files.
```
