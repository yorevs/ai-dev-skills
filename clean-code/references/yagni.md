# YAGNI Examples

```python
# Bad: unused flexibility for hypothetical future formats
def export_report(data, format_type="json", compression=None, encryption=None):
    if format_type == "json":
        return json.dumps(data)
    # CSV, XML, compression, and encryption are not currently required

# YAGNI: implement only the current requirement
def export_report(data):
    return json.dumps(data)
```

```java
// Bad: unnecessary abstraction for a single implementation
interface NotificationService {
  void send(String message);
}

class EmailNotificationService implements NotificationService {
  public void send(String message) {
    System.out.println(message);
  }
}

// YAGNI: implement only what is currently needed
class EmailNotificationService {
  void send(String message) {
    System.out.println(message);
  }
}
```