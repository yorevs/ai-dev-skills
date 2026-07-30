## Example 3: Command-Line Tool

### System Context

* Local command-line application
* No web server
* No database
* No remote authentication
* Reads local YAML configuration files
* Calls an external HTTPS API

### Applicable Controls

* Secure configuration parsing
* Input validation
* File permission validation
* TLS certificate validation
* Secret protection
* Request timeouts
* Secure error handling

### Ignored Controls

* **CSRF Protection — Not Applicable**
  The application does not run in a browser.

* **CORS Configuration — Not Applicable**
  The application does not expose a browser-accessible API.

* **Rate Limiting — Not Applicable at Application Ingress**
  The tool does not receive remote requests. However, it should respect rate limits imposed by external APIs.

* **Content Security Policy — Not Applicable**
  The application does not render HTML.

* **Secure Cookies — Not Applicable**
  The application does not use cookies.

### Example Report

```text
Risk: API token stored in a world-readable configuration file
Severity: High

Description:
Other users on the same operating system may be able to read the API token.

Recommendation:
- Store the token in the operating system credential manager when available.
- Otherwise, require restrictive file permissions.
- Reject configuration files readable by unauthorized users.
- Never print the token in logs or error messages.

Ignored controls:
- CSRF: Not applicable because the application is a local CLI.
- CSP: Not applicable because no HTML is rendered.
- SQL injection: Not applicable because the application does not use a SQL database.
```