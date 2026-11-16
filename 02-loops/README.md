# Practice Challenge 2 – Python Loops

## Overview

This challenge focuses on Python loops, testing your understanding of iteration, loop structures, and problem-solving.

## Getting Started

Pip install requirements.txt before you start.


## Instructions

1. Open `challenge.py` and complete the coding task.
2. Use the attached `cheatsheet.pdf` as a reference if needed.
3. Run the automated tests to validate your solution using pytest.

```bash
pytest -v
```

## Files

- `practice.py` – Coding practice challenge.
- `test_pratice.py` – Automated tests using pytest.
- `CHEATSHEET.pdf` – Python loops reference guide.


### Task: Number Analysis

Write a function `def analyse_numbers(numbers)` that takes a list of integers and returns a dictionary containing:

- `even_numbers`: All even numbers.
- `odd_numbers`: All odd numbers.
- `positive_sum`: Sum of all positive numbers.
- `negative_count`: Number of negative values.
- `largest_number`: Largest number in the list.

### Example

**Input:**
```python
[4, -3, 7, 10, -2, 5, 0]
```

**Expected output:**
```python
{
    "even_numbers": [4, 10, -2, 0],
    "odd_numbers": [-3, 7, 5],
    "positive_sum": 26,
    "negative_count": 2,
    "largest_number": 10
}
```

### Requirements

- Use `for` or `while` loops and conditional statements.
- Do not use list comprehensions, `sum()` or `max()`.
- Handle empty input appropriately.
- Write a separate set of automated tests using `pytest` to validate your function, including edge cases.

**Good luck!**