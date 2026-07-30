## Example 2: Traditional Web Application

### System Context

* Server-rendered web application
* Authentication using session cookies
* HTML forms
* MySQL database
* Users can upload profile pictures
* Application is accessed through browsers

### Applicable Controls

* CSRF protection
* Secure session cookies
* Output encoding
* Content Security Policy
* SQL injection prevention
* File upload validation
* Session expiration
* Authentication rate limiting
* XSS prevention

### Ignored Controls

* **JWT Validation — Not Applicable**
  The application uses server-side sessions instead of JWT tokens.

* **Prompt Injection Protection — Not Applicable**
  The application does not use an LLM.

### Example Secure Cookie Configuration

```http
Set-Cookie: session=<value>; Secure; HttpOnly; SameSite=Lax; Path=/
```

### Example SQL Recommendation

Unsafe:

```javascript
const query = `SELECT * FROM users WHERE email = '${email}'`;
```

Safer:

```javascript
const result = await db.query(
  "SELECT id, email, password_hash FROM users WHERE email = $1",
  [email]
);
```

### Example File Upload Report

```text
Risk: Uploaded files are stored using their original filename
Severity: High

Description:
An attacker may upload a file with a malicious name, overwrite an existing file, or attempt path traversal.

Recommendation:
- Generate a random server-side filename.
- Validate the actual file content.
- Restrict accepted MIME types.
- Enforce a maximum file size.
- Store files outside the public web root.
- Serve files through a controlled download endpoint.

Ignored controls:
- JWT validation: Not applicable because the system uses server-side sessions.
```