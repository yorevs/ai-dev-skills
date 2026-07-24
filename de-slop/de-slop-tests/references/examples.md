# Testing Examples

These examples illustrate the preferred direction when refactoring tests.

---

## Avoid Presentation Assertions

### ❌ Bad

```python
assert ui.title.text == "Settings"
assert ui.status.text == "Ready"
assert ui.button.text == "Save"
```

This verifies presentation rather than behavior. These tests are brittle because harmless UI changes break them.

### ✅ Good

```python
assert ui.is_ready()
assert ui.can_save()
```

Prefer asserting business behavior or application state instead of presentation details.

**Exception**

If the exact text is the behavior being tested, asserting the string is appropriate.

```python
assert response.message == "Authentication failed."
assert api.error.code == "USER_NOT_FOUND"
assert email.subject == "Reset your password"
```

---

## Prefer Features Over Strings

### ❌ Bad

```python
assert table.empty_label.text == "No Results"
```

### ✅ Good

```python
assert table.is_empty()
```

Only verify `"No Results"` if the wording itself is a contractual requirement.

---

## Prefer Domain Objects

### ❌ Bad

```python
assert table.rows[0][1] == "John"
```

### ✅ Good

```python
assert users[0].name == "John"
```

Verify the business object instead of its presentation.

---

## Avoid CSS/Layout Assertions

### ❌ Bad

```python
assert button.color == "blue"
assert panel.padding == 8
assert label.font_size == 14
```

### ✅ Good

```python
assert button.is_enabled()
assert panel.is_visible()
```

Visual properties should only be asserted when they are the intended behavior under test.

---

## Prefer Outcomes Over Interactions

### ❌ Bad

```python
repository.save.assert_called_once()
```

### ✅ Good

```python
assert repository.find(user.id) == user
```

Verify the observable result rather than the implementation.

---

## Extract Repeated Setup

### ❌ Bad

```python
repo = FakeRepository()
service = UserService(repo)
user = User("john")

service.create(user)
```

### ✅ Good

```python
service = create_user_service()

service.create(User("john"))
```

Extract repeated setup, not test logic.

---

## Preserve Test Names

Prefer keeping existing test names stable unless a rename significantly improves clarity.

```python
def test_create_user_without_email():
    ...
```
