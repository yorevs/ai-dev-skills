# SOLID Examples

These examples are intentionally small. Apply SOLID principles only when they improve the design. Do not introduce abstractions mechanically.

## S — Single Responsibility Principle

### Before

```java
class UserService {

    void create(User user) {
        validate(user);
        repository.save(user);
        emailService.sendWelcome(user);
    }
}
```

### After

```java
class UserService {

    private final UserRepository repository;
    private final NotificationService notifier;

    UserService(UserRepository repository,
                NotificationService notifier) {
        this.repository = repository;
        this.notifier = notifier;
    }

    void create(User user) {
        validate(user);
        repository.save(user);
        notifier.sendWelcome(user);
    }
}
```

---

## O — Open/Closed Principle

### Before

```java
class DiscountService {

    int discount(Customer customer) {
        switch (customer.type()) {
            case REGULAR: return 0;
            case PREMIUM: return 20;
        }
        return 0;
    }
}
```

### After

```java
interface DiscountPolicy {
    int discount();
}

class PremiumDiscount implements DiscountPolicy {
    public int discount() { return 20; }
}

class RegularDiscount implements DiscountPolicy {
    public int discount() { return 0; }
}
```

---

## L — Liskov Substitution Principle

### Before

```java
class Bird {
    void fly() {}
}

class Penguin extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException();
    }
}
```

### After

```java
class Bird {}

interface Flying {
    void fly();
}

class Eagle extends Bird implements Flying {
    public void fly() {}
}

class Penguin extends Bird {}
```

---

## I — Interface Segregation Principle

### Before

```java
interface Worker {
    void work();
    void drive();
}
```

### After

```java
interface Worker {
    void work();
}

interface Driver {
    void drive();
}
```

---

## D — Dependency Inversion Principle

### Before

```java
class OrderService {

    private final SqlOrderRepository repository =
        new SqlOrderRepository();
}
```

### After

```java
interface OrderRepository {
    void save(Order order);
}

class OrderService {

    private final OrderRepository repository;

    OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
```
