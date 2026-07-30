## Example 6: Static Website

### System Context

* Static HTML, CSS, and JavaScript
* Hosted through a CDN
* No backend
* No authentication
* No database
* Contact form handled by a third-party service

### Applicable Controls

* Content Security Policy
* Subresource Integrity
* Dependency security
* Secure third-party integrations
* XSS prevention
* HTTPS
* Security headers
* Privacy review
* Protection against malicious redirects

### Ignored Controls

* **SQL Injection Protection — Not Applicable**
  The website does not use a database.

* **Server-Side Authorization — Not Applicable**
  The website does not have authenticated server-side functionality.

* **Password Storage — Not Applicable**
  The website does not process passwords.

* **Secure Cookies — Not Applicable**
  The website does not create authentication or session cookies.

### Example Security Headers

```http
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; base-uri 'self'
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

### Example Report

```text
Risk: JavaScript dependency loaded from a third-party CDN without integrity validation
Severity: Medium

Description:
If the third-party CDN or package is compromised, malicious JavaScript may execute in users' browsers.

Recommendation:
- Host the dependency locally, or
- Use Subresource Integrity with a pinned version.
- Restrict script sources using Content Security Policy.

Ignored controls:
- SQL injection: Not applicable because the website has no database.
- Password security: Not applicable because the website does not authenticate users.
```