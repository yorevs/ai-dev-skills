# DRY Examples

```python
# Bad: duplicated code
def calculate_product_price(price):
    return price + (price * 0.10)

def calculate_service_price(price):
    return price + (price * 0.10)

# DRY: centralized logic
def add_tax(price, tax_rate=0.10):
    return price * (1 + tax_rate)

product = add_tax(100)
service = add_tax(200)
```

```java
// Bad: duplicated logic
double productPrice = 100 + (100 * 0.10);
double servicePrice = 200 + (200 * 0.10);

// DRY: reusable method
static double addTax(double price, double taxRate) {
  return price * (1 + taxRate);
}

double productPrice = addTax(100, 0.10);
double servicePrice = addTax(200, 0.10);
```