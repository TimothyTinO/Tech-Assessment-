# Receipt Calculator

You're writing the till software for _Corner Store Ltd._ It needs to add up shopping baskets, apply discount codes and print receipts.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Basket Total

A basket is a list of `(name, price, quantity)` tuples.

Write `calculate_total(items)` that returns the total cost, rounded to 2 decimal places.

Raise a `ValueError` if any price is negative or any quantity is less than 1.

**Examples:**
```python
calculate_total([("Apple", 0.5, 4), ("Bread", 2.25, 1)])
# Returns: 4.25

calculate_total([])
# Returns: 0.0

calculate_total([("Milk", -1.0, 1)])
# Raises ValueError
```

## Step 2: Discount Codes

Write `apply_discount(total, code)` that returns the new total, rounded to 2 decimal places.

Codes (not case-sensitive):

- `"SAVE10"`: 10% off
- `"FLAT5"`: 5.00 off, but the total can never go below `0`
- Any other code: no change

**Examples:**
```python
apply_discount(100, "SAVE10")   # 90.0
apply_discount(100, "save10")   # 90.0
apply_discount(3, "FLAT5")      # 0.0
apply_discount(50, "BOGUS")     # 50.0
apply_discount(50, None)        # 50.0
```

## Step 3: Print the Receipt

Write `format_receipt(items, code=None)` that returns the receipt as a single string.

- One line per item: `Name xQTY @ PRICE = LINETOTAL`
- If a valid code is used, add a `SUBTOTAL` line and a `DISCOUNT` line before the total.
- An invalid or missing code is treated as no discount, with no extra lines.
- Every line ends with a newline (`\n`).
- All money values show exactly 2 decimal places.

**Examples:**
```python
format_receipt([("Pen", 1.5, 2), ("Book", 7.0, 1)])
# Returns:
# "Pen x2 @ 1.50 = 3.00\n"
# "Book x1 @ 7.00 = 7.00\n"
# "TOTAL: 10.00\n"

format_receipt([("Pen", 1.5, 2), ("Book", 7.0, 1)], "SAVE10")
# Returns:
# "Pen x2 @ 1.50 = 3.00\n"
# "Book x1 @ 7.00 = 7.00\n"
# "SUBTOTAL: 10.00\n"
# "DISCOUNT (SAVE10): -1.00\n"
# "TOTAL: 9.00\n"
```

## 💡 Hints

1. Each tuple can be unpacked in a loop: `for name, price, qty in items:`.
2. Use `round(value, 2)` for rounding.
3. `f"{value:.2f}"` formats a number with exactly 2 decimal places (so `9` becomes `"9.00"`).
4. For Step 3, reuse `calculate_total` and `apply_discount` rather than redoing the maths.
5. The discount amount is just `subtotal - new_total`.
