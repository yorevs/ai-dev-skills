## Example 4: Internal Microservice

### System Context

* Internal service
* Runs inside a private Kubernetes cluster
* Communicates with other services
* No direct browser access
* Uses mutual TLS
* Uses Redis
* Does not use SQL
* No public endpoint

### Applicable Controls

* Service-to-service authentication
* Workload identity
* Network policies
* Least-privilege service accounts
* Redis command and access restrictions
* Secret management
* Container scanning
* Kubernetes security policies
* Request validation
* Timeouts and circuit breakers

### Ignored Controls

* **CORS Configuration — Not Applicable**
  Browsers do not access the service directly.

* **CSRF Protection — Not Applicable**
  The service does not use browser sessions or cookies.

* **SQL Injection Protection — Not Applicable**
  The system does not use a SQL database.

* **Content Security Policy — Not Applicable**
  The service does not render HTML.

### Example Kubernetes Recommendation

Unsafe:

```yaml
securityContext:
  privileged: true
```

Safer:

```yaml
securityContext:
  runAsNonRoot: true
  allowPrivilegeEscalation: false
  readOnlyRootFilesystem: true
  capabilities:
    drop:
      - ALL
```

### Example Report

```text
Risk: Kubernetes workload runs with privileged access
Severity: Critical

Description:
A successful compromise of the container may allow access to the host operating system.

Recommendation:
- Disable privileged mode.
- Run as a non-root user.
- Drop all unnecessary Linux capabilities.
- Use a read-only root filesystem.
- Apply restrictive network policies.

Ignored controls:
- CORS: Not applicable because the service is not called by browsers.
- SQL injection: Not applicable because Redis is used instead of SQL.
```