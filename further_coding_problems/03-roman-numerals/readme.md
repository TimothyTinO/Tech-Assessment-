# Roman Numerals

You're helping _Caesar & Sons Clockmakers_ put Roman numerals on their watch faces and in their ledgers.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Integer to Roman

Write `to_roman(n)` that converts an integer from `1` to `3999` into a Roman numeral string using standard subtractive notation (`IV`, `IX`, `XL`, `XC`, `CD`, `CM`).

Return `None` if the number is outside that range.

**Examples:**
```python
to_roman(4)      # "IV"
to_roman(58)     # "LVIII"
to_roman(1994)   # "MCMXCIV"
to_roman(0)      # None
to_roman(4000)   # None
```

## Step 2: Roman to Integer

Write `from_roman(s)` that converts a Roman numeral back to an integer.

Return `None` if the string is **not a valid, canonical** Roman numeral. For example `"IIII"` is invalid because it should be `"IV"`.

**Examples:**
```python
from_roman("MCMXCIV")   # 1994
from_roman("LVIII")     # 58
from_roman("IIII")      # None
from_roman("IC")        # None  (99 is "XCIX")
from_roman("abc")       # None
from_roman("")          # None
```

## Step 3: Roman Arithmetic

Write `add_roman(a, b)` that takes two Roman numerals and returns their sum as a Roman numeral.

Return `None` if either input is invalid or if the sum is greater than `3999`.

**Examples:**
```python
add_roman("XIV", "LX")    # "LXXIV"
add_roman("MCM", "LXXX")  # "MMLXXX"
add_roman("MMM", "M")     # None  (4000 is too big)
add_roman("IIII", "I")    # None
```

## 💡 Hints

1. Make a list of `(value, symbol)` pairs ordered from largest to smallest, **including** the subtractive ones: `(900, "CM")`, `(400, "CD")`, `(90, "XC")`, and so on.
2. For `to_roman`, go through that list and subtract the value (appending the symbol) for as long as it fits.
3. A neat way to validate in `from_roman`: convert the number back with `to_roman` and check you get the exact same string.
4. When parsing, if a symbol is smaller than the one after it, subtract it; otherwise add it.
