# KISS Examples

```python
# Bad: unnecessary complexity
def can_access(user):
    if user is not None:
        if user.is_active:
            return True
    return False

# KISS: simple and direct
def can_access(user):
    return user is not None and user.is_active

# Bad: unnecessary sorting
def find_maximum(numbers):
    sorted_numbers = sorted(numbers)
    return sorted_numbers[-1]

# KISS: use the simplest available solution
def find_maximum(numbers):
    return max(numbers)
```


```java
// Bad: unnecessary complexity
boolean canAccess(User user) {
  if (user != null) {
    if (user.isActive()) {
      return true;
    }
  }
  return false;
}

// KISS: simple and direct
boolean canAccess(User user) {
  return user != null && user.isActive();
}

// Bad: unnecessary loop
int findMaximum(int[] numbers) {
  List<Integer> sorted = Arrays.stream(numbers)
      .boxed()
      .sorted()
      .toList();

  return sorted.get(sorted.size() - 1);
}

// KISS: calculate only what is needed
int findMaximum(int[] numbers) {
  return Arrays.stream(numbers).max().orElseThrow();
}
```