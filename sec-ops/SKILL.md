---
name: sec-ops
description: Use when designing, implementing, reviewing, refactoring, or maintaining software in any programming language where security is a requirement. Apply secure-by-design principles, identify vulnerabilities, and recommend industry best practices throughout the software development lifecycle.
---

# Security Operations (SecOps)

## Objective

Produce software that is secure by design, secure by default, and resilient against known attack vectors.

Always prioritize:

- Confidentiality
- Integrity
- Availability
- Authentication
- Authorization
- Accountability
- Privacy
- Defense in Depth
- Zero Trust

Never trade security for convenience without explicitly explaining the associated risks.

See:

- `references/background-worker.md`
- `references/cli-tool.md`
- `references/internal-microservice.md`
- `references/llm-app-with-access.md`
- `references/stateless-rest-api.md`
- `references/static-website.md`
- `references/traditional-webapp.md`

---

# Core Knowledge

The assistant should understand and correctly apply concepts including, but not limited to:

## Authentication & Authorization

- Authentication
- Authorization
- RBAC
- ABAC
- Least Privilege
- Zero Trust
- Multi-Factor Authentication (MFA)
- OAuth 2.0
- OpenID Connect
- JWT
- Session Management

---

## Cryptography

Understand when and how to use:

- Hashing
- Salting
- Key Stretching
- Encryption
- Digital Signatures
- TLS
- Public Key Infrastructure (PKI)
- Certificate Validation
- Key Rotation
- Secure Secret Management

Never:

- Implement custom cryptography
- Invent encryption algorithms
- Store secrets in source code
- Hardcode API keys
- Hardcode passwords
- Hardcode certificates

Always prefer proven cryptographic libraries.

---

## Data Protection

Know how to securely protect:

- Personally Identifiable Information (PII)
- Credentials
- Secrets
- Tokens
- Session identifiers
- API Keys
- Encryption Keys

Use:

- Encryption at Rest
- Encryption in Transit
- Secure Storage
- Secure Secret Managers

---

## Secure Serialization

Understand risks involving:

- Deserialization attacks
- Object Injection
- Reflection abuse
- Type confusion

Never deserialize untrusted data without validation.

---

## Secure Input Handling

Validate every external input.

Protect against:

- SQL Injection
- NoSQL Injection
- Command Injection
- LDAP Injection
- XPath Injection
- XML Injection
- Prompt Injection

Prefer:

- Allow-lists
- Parameterized Queries
- Prepared Statements
- Strong typing

Never trust client input.

---

## Output Encoding

Encode output according to context:

- HTML
- JSON
- XML
- URL
- JavaScript
- CSS

Never confuse validation with encoding.

---

# OWASP Security

Always consider:

- OWASP Top 10
- OWASP API Security Top 10
- OWASP ASVS
- OWASP Cheat Sheet Series
- OWASP Proactive Controls

When reviewing code, actively search for vulnerabilities from these references.

---

# AI Security

When software includes LLMs or AI systems, evaluate:

- Prompt Injection
- Tool Injection
- Context Poisoning
- Data Exfiltration
- Jailbreak attempts
- Unsafe Tool Calls
- Hallucinated Permissions

Never assume model output is trustworthy.

Always validate AI-generated output before execution.

---

# Secure Design Principles

## 1. Secure by Design

Security begins during architecture.

Always:

- Perform threat modeling
- Reduce trust boundaries
- Minimize exposed interfaces
- Validate assumptions

---

## 2. Secure by Default

Applications should start in their safest configuration.

Examples:

- Authentication enabled
- HTTPS enforced
- Least privilege enabled
- Logging enabled
- Security headers enabled

Never rely on users to secure the application.

---

## 3. Least Privilege

Grant only the permissions strictly required.

Apply to:

- Users
- Services
- APIs
- Databases
- Containers
- Cloud resources

---

## 4. Defense in Depth

Never rely on a single security control.

Use multiple independent layers including:

- Authentication
- Authorization
- Validation
- Logging
- Monitoring
- Network controls
- Encryption

---

## 5. Complete Mediation

Every access request must be verified.

Never trust cached permissions.

---

## 6. Fail Securely

On failure:

- Deny access
- Roll back safely
- Avoid information disclosure
- Log securely

Never expose:

- Stack traces
- Secrets
- Internal paths
- SQL statements

---

## 7. Separation of Duties

Separate critical responsibilities.

Avoid allowing one actor to control:

- Deployment
- Infrastructure
- Secrets
- Production approval

---

## 8. Minimize Attack Surface

Remove:

- Dead code
- Unused APIs
- Unused ports
- Unused packages
- Unused services

Every dependency increases risk.

---

# Secure Coding Rules

Always:

- Validate all input.
- Encode all output.
- Use parameterized queries.
- Use prepared statements.
- Sanitize uploaded files.
- Validate MIME types.
- Validate file extensions.
- Validate file size.
- Validate authorization on every request.
- Implement rate limiting.
- Use CSRF protection when applicable.
- Use secure cookies.
- Set HttpOnly cookies.
- Set Secure cookies.
- Set SameSite cookies.
- Use HTTPS exclusively.
- Apply Content Security Policy (CSP).
- Validate redirects.
- Set security headers.
- Implement request timeouts.
- Close resources properly.
- Rotate credentials.
- Rotate secrets.
- Use immutable infrastructure whenever possible.

Never:

- Concatenate SQL.
- Execute user input as commands.
- Trust client-side validation.
- Log passwords.
- Log tokens.
- Log API keys.
- Log secrets.
- Disable TLS verification.
- Store passwords in plain text.
- Store secrets in configuration files.
- Use deprecated cryptographic algorithms.
- Ignore exceptions silently.
- Expose sensitive error messages.

---

# API Security

Review:

- Authentication
- Authorization
- Rate limiting
- Pagination
- Idempotency
- Replay attacks
- JWT validation
- Token expiration
- Token revocation
- CORS configuration
- CSRF protection
- API versioning

---

# Dependency Security

Always:

- Maintain an inventory of dependencies.
- Keep dependencies updated.
- Remove unused packages.
- Verify package integrity.
- Scan for known vulnerabilities.

Prefer:

- SBOM
- Dependency pinning
- Signed artifacts

---

# DevSecOps

Security should be automated.

Encourage:

- SAST
- DAST
- SCA
- Secret Scanning
- Container Scanning
- IaC Scanning
- CI/CD security gates
- Security regression testing

---

# Logging & Monitoring

Logs should:

- Be immutable
- Be centralized
- Protect confidentiality
- Avoid sensitive information
- Support auditing

Monitor:

- Failed authentication
- Privilege escalation
- Unexpected exceptions
- Suspicious traffic
- Configuration changes

---

# Threat Modeling

Before implementing features, evaluate:

- Assets
- Trust boundaries
- Entry points
- Threat actors
- Attack vectors
- Abuse cases

Recommended methodologies:

- STRIDE
- PASTA
- Attack Trees

---

# Incident Response

Design software to support:

- Detection
- Containment
- Eradication
- Recovery
- Forensics

Security events should be traceable.

---

# Compliance

When applicable, consider:

- NIST SSDF
- ISO 27001
- SOC 2
- PCI DSS
- GDPR
- LGPD

---

# Code Review Checklist

When reviewing code, verify:

- [ ] Authentication is correct.
- [ ] Authorization is enforced.
- [ ] Least privilege is respected.
- [ ] Input validation exists.
- [ ] Output encoding is correct.
- [ ] SQL is parameterized.
- [ ] Secrets are protected.
- [ ] Cryptography uses standard libraries.
- [ ] Error handling is secure.
- [ ] Logging avoids sensitive information.
- [ ] Security headers are configured.
- [ ] Dependencies are up to date.
- [ ] APIs enforce rate limiting.
- [ ] Business logic prevents abuse.
- [ ] AI interactions are protected against prompt injection.
- [ ] No obvious OWASP Top 10 vulnerabilities exist.

---

# Response Guidelines

When generating, reviewing, refactoring, or auditing software:

1. Evaluate which security controls are applicable to the current system, architecture, and technology stack before making recommendations.
2. Apply only the security practices that are relevant to the context.
3. If a security control is **not applicable**, explicitly omit it instead of forcing its implementation.
4. For every omitted control, briefly explain **why it does not apply**.
5. Explain all identified security risks.
6. Classify each risk using one of the following severities:
   * Low
   * Medium
   * High
   * Critical
7. Recommend practical mitigations for every identified risk.
8. Prefer secure, well-maintained, industry-standard libraries and frameworks over custom implementations.
9. Preserve the intended functionality while improving the application's security posture.
10. Explain any trade-offs between security, usability, performance, and maintainability.
11. Never recommend insecure shortcuts without explicitly stating their associated risks.

## Applicability Assessment

Before presenting recommendations, determine whether each security practice is applicable.

Possible outcomes:

* **Applicable** – The control should be implemented.
* **Already Implemented** – The control already exists and appears correctly implemented.
* **Not Applicable** – The control does not apply to the current system.
* **Insufficient Information** – There is not enough information to determine applicability.

Whenever a control is marked as **Not Applicable**, provide a short justification.

Examples:

* CSRF protection → Not Applicable (Stateless REST API using Authorization Bearer tokens.)
* Secure Cookies → Not Applicable (Application does not use browser cookies.)
* CSP Headers → Not Applicable (Backend service with no HTML rendering.)
* SQL Injection → Not Applicable (Application does not use a SQL database.)
* JWT Validation → Not Applicable (Application uses server-side sessions.)
* File Upload Validation → Not Applicable (System does not accept file uploads.)
* Prompt Injection Protection → Not Applicable (No LLM or generative AI components.)
* CORS Configuration → Not Applicable (Service is not exposed to browsers.)

The final report should clearly distinguish between implemented controls, recommended controls, omitted controls, and the justification for every omitted recommendation.
