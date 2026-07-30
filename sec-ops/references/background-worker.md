## Example 7: Background Worker

### System Context

* Consumes messages from a queue
* Processes payment events
* No HTTP endpoints
* No browser access
* Connects to a database
* Calls a payment provider

### Applicable Controls

* Message authenticity
* Idempotency
* Replay protection
* Database injection prevention
* Secret management
* Transaction integrity
* Error handling
* Retry limits
* Dead-letter queues
* Audit logging
* Payment data protection

### Ignored Controls

* **CORS Configuration — Not Applicable**
  The worker does not expose an HTTP endpoint to browsers.

* **CSRF Protection — Not Applicable**
  The worker does not process browser requests.

* **Content Security Policy — Not Applicable**
  The worker does not render HTML.

### Example Idempotency Logic

```text
1. Receive event.
2. Validate event signature.
3. Check whether event ID was already processed.
4. Start database transaction.
5. Apply the operation.
6. Store event ID as processed.
7. Commit transaction.
```

### Example Report

```text
Risk: Payment events may be processed more than once
Severity: High

Description:
Queue retries or duplicated events may create duplicate charges or inconsistent financial records.

Recommendation:
- Require a unique event identifier.
- Implement idempotent processing.
- Store processed event identifiers transactionally.
- Validate the payment provider signature.
- Reject events outside an acceptable time window.

Ignored controls:
- CSRF: Not applicable because the worker does not accept browser requests.
- CORS: Not applicable because the worker has no browser-facing HTTP API.
```