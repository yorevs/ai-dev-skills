# SOLID Examples

These examples are intentionally small. Apply SOLID principles only when they improve the design. Do not introduce abstractions mechanically.

## S — Single Responsibility Principle

### Before

```python
class UserService:
    def create(self, user: User) -> None:
        validate(user)
        repository.save(user)
        email.send_welcome(user)
```

### After

```python
class UserService:
    def __init__(
        self,
        repository: UserRepository,
        notifier: NotificationService,
    ) -> None:
        self._repository = repository
        self._notifier = notifier

    def create(self, user: User) -> None:
        validate(user)
        self._repository.save(user)
        self._notifier.send_welcome(user)
```

---

## O — Open/Closed Principle

### Before

```python
def discount(customer: Customer) -> int:
    if customer.type == "regular":
        return 0
    if customer.type == "premium":
        return 20
    return 0
```

### After

```python
from typing import Protocol


class DiscountPolicy(Protocol):
    def discount(self) -> int: ...


class PremiumDiscount:
    def discount(self) -> int:
        return 20
```

New behavior is added by implementing `DiscountPolicy` rather than modifying existing code.

---

## L — Liskov Substitution Principle

### Before

```python
class Bird:
    def fly(self) -> None:
        ...


class Penguin(Bird):
    def fly(self) -> None:
        raise NotImplementedError()
```

### After

```python
from typing import Protocol


class Flying(Protocol):
    def fly(self) -> None: ...


class Eagle(Flying):
    def fly(self) -> None:
        ...
```

Only flying birds implement the `Flying` contract.

---

## I — Interface Segregation Principle

### Before

```python
class Worker(Protocol):
    def work(self) -> None: ...
    def drive(self) -> None: ...
```

### After

```python
class Worker(Protocol):
    def work(self) -> None: ...


class Driver(Protocol):
    def drive(self) -> None: ...
```

Clients depend only on the behavior they require.

---

## D — Dependency Inversion Principle

### Before

```python
class OrderService:
    def __init__(self) -> None:
        self._repository = SqlOrderRepository()
```

### After

```python
from typing import Protocol


class OrderRepository(Protocol):
    def save(self, order: Order) -> None: ...


class OrderService:
    def __init__(self, repository: OrderRepository) -> None:
        self._repository = repository
```

The high-level service depends on an abstraction rather than a concrete implementation.
