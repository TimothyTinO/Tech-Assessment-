# Python Sorting & Searching Cheatsheet

Sorting is the process of arranging data in a particular order. Searching is the process of finding a value, its position or the elements that satisfy a condition.

Python provides built-in methods for both, along with techniques for handling more complex problems.

## Sorting Basics

### Using `sorted()`

`sorted()` returns a **new sorted list** without modifying the original collection.

```python
numbers = [5, 2, 8, 1, 3]

result = sorted(numbers)
# [1, 2, 3, 5, 8]

print(numbers)
# [5, 2, 8, 1, 3]
```

Descending order:

```python
sorted(numbers, reverse=True)
# [8, 5, 3, 2, 1]
```

### Using `.sort()`

`.sort()` modifies the original list.

```python
numbers = [5, 2, 8, 1, 3]

numbers.sort()
# [1, 2, 3, 5, 8]
```

Descending order:

```python
numbers.sort(reverse=True)
# [8, 5, 3, 2, 1]
```

### `sorted()` vs `.sort()`

| Feature | `sorted()` | `.sort()` |
|---|---|---|
| Returns a new list | Yes | No |
| Modifies original list | No | Yes |
| Works on tuples | Yes | No |
| Works on strings | Yes | No |
| Supports `key` | Yes | Yes |
| Supports `reverse` | Yes | Yes |

**Important:** `.sort()` returns `None`, not the sorted list.

---

## Sorting Numbers

### Ascending Order

```python
numbers = [10, 5, 20, 15]

sorted(numbers)
# [5, 10, 15, 20]
```

### Descending Order

```python
sorted(numbers, reverse=True)
# [20, 15, 10, 5]
```

### Negative Numbers

```python
numbers = [-5, 10, -20, 3]

sorted(numbers)
# [-20, -5, 3, 10]
```

### Removing Duplicates and Sorting

```python
numbers = [5, 2, 2, 8, 1, 5]

sorted(set(numbers))
# [1, 2, 5, 8]
```

### Getting the Smallest or Largest Value

```python
numbers = [10, 50, 20, 40]

min(numbers)    # 10
max(numbers)    # 50
```

---

## Sorting Strings

### Alphabetical Sorting

```python
names = ["Charlie", "Alex", "Ben"]

sorted(names)
# ['Alex', 'Ben', 'Charlie']
```

### Reverse Alphabetical Order

```python
sorted(names, reverse=True)
# ['Charlie', 'Ben', 'Alex']
```

### Case-Sensitive Sorting

```python
names = ["alex", "Sam", "ben", "Alex"]

sorted(names)
# ['Alex', 'Sam', 'alex', 'ben']
```

By default, uppercase letters are ordered before lowercase letters in standard English text.

### Case-Insensitive Sorting

```python
names = ["alex", "Sam", "ben", "Alex"]

sorted(names, key=str.lower)
# ['alex', 'Alex', 'ben', 'Sam']
```

You can also use `str.casefold` for more general case-insensitive comparisons.

### Sorting Characters in a String

```python
sorted("python")
# ['h', 'n', 'o', 'p', 't', 'y']
```

To return a string instead of a list:

```python
"".join(sorted("python"))
# 'hnopty'
```

---

## Sorting With `key`

The `key` parameter determines which value Python uses when sorting.

### Sorting by String Length

```python
words = ["python", "is", "awesome", "fun"]

sorted(words, key=len)
# ['is', 'fun', 'python', 'awesome']
```

Longest first:

```python
sorted(words, key=len, reverse=True)
# ['awesome', 'python', 'fun', 'is']
```

### Lambda Functions

A lambda is a small anonymous function.

```python
double = lambda x: x * 2

double(5)
# 10
```

A lambda is often useful when specifying a sorting rule.

```python
numbers = [-10, 5, -3, 2]

sorted(numbers, key=lambda x: abs(x))
# [2, -3, 5, -10]
```

This sorts numbers by their absolute values.

### Sorting by Multiple Conditions

```python
records = [
    ("Sam", 20),
    ("Alex", 20),
    ("Jo", 30)
]
```

Sort by score descending, then name ascending:

```python
sorted(records, key=lambda item: (-item[1], item[0]))

# [
#     ('Jo', 30),
#     ('Alex', 20),
#     ('Sam', 20)
# ]
```

Explanation:

- `item[1]` represents the score.
- `-item[1]` makes higher scores come first.
- `item[0]` sorts tied scores alphabetically.

---

## Sorting Lists of Tuples

### Default Tuple Sorting

```python
pairs = [(2, 5), (1, 9), (2, 3)]

sorted(pairs)
# [(1, 9), (2, 3), (2, 5)]
```

Python compares the first element, then the second if needed.

### Sorting by the Second Element

```python
scores = [
    ("Alex", 10),
    ("Sam", 30),
    ("Jo", 20)
]

sorted(scores, key=lambda item: item[1])

# [
#     ('Alex', 10),
#     ('Jo', 20),
#     ('Sam', 30)
# ]
```

### Sorting by Score Descending

```python
sorted(scores, key=lambda item: item[1], reverse=True)

# [
#     ('Sam', 30),
#     ('Jo', 20),
#     ('Alex', 10)
# ]
```

---

## Sorting Dictionaries

### Sorting Dictionary Keys

```python
scores = {
    "Sam": 20,
    "Alex": 30,
    "Jo": 10
}

sorted(scores)
# ['Alex', 'Jo', 'Sam']
```

By default, sorting a dictionary sorts its keys.

### Sorting by Values

```python
sorted(scores.items(), key=lambda item: item[1])

# [
#     ('Jo', 10),
#     ('Sam', 20),
#     ('Alex', 30)
# ]
```

### Sorting by Values Descending

```python
sorted(
    scores.items(),
    key=lambda item: item[1],
    reverse=True
)

# [
#     ('Alex', 30),
#     ('Sam', 20),
#     ('Jo', 10)
# ]
```

### Sorting by Value Then Key

```python
scores = {
    "Sam": 20,
    "Alex": 20,
    "Jo": 30
}

sorted(scores.items(), key=lambda item: (-item[1], item[0]))

# [
#     ('Jo', 30),
#     ('Alex', 20),
#     ('Sam', 20)
# ]
```

### Creating a Sorted Dictionary

```python
scores = {"Sam": 20, "Alex": 30, "Jo": 10}

ordered = dict(sorted(scores.items()))

# {'Alex': 30, 'Jo': 10, 'Sam': 20}
```

Dictionaries preserve insertion order in modern Python.

---

## Stable Sorting

Python's sorting is **stable**.

This means elements with equal sorting keys preserve their original relative order.

```python
records = [
    ("Sam", 20),
    ("Alex", 20),
    ("Jo", 30)
]

sorted(records, key=lambda item: item[1], reverse=True)

# [
#     ('Jo', 30),
#     ('Sam', 20),
#     ('Alex', 20)
# ]
```

Sam appears before Alex because both have the same score, and Sam appeared first in the original list.

---

## Searching Basics

### Checking Membership

```python
numbers = [10, 20, 30]

20 in numbers       # True
50 in numbers       # False
```

```python
names = ["Alex", "Sam", "Jo"]

"Sam" in names      # True
"Ben" not in names  # True
```

### Finding an Index

```python
numbers = [10, 20, 30, 20]

numbers.index(20)
# 1
```

`.index()` returns the position of the first occurrence.

If the value does not exist, it raises `ValueError`.

### Finding All Matching Indexes

```python
numbers = [10, 20, 30, 20]

positions = []

for i, value in enumerate(numbers):
    if value == 20:
        positions.append(i)

# [1, 3]
```

This is useful when a value appears multiple times.

### Using `enumerate()`

```python
names = ["Alex", "Sam", "Jo"]

for index, name in enumerate(names):
    print(index, name)

# 0 Alex
# 1 Sam
# 2 Jo
```

`enumerate()` provides both the index and value during iteration.

---

## Linear Search

Linear search checks elements one at a time until the target is found.

```python
def linear_search(numbers: list[int], target: int) -> int:
    for i, value in enumerate(numbers):
        if value == target:
            return i

    return -1
```

**Examples:**

```python
linear_search([10, 20, 30], 20)
# 1

linear_search([10, 20, 30], 50)
# -1
```

**Characteristics:**

- Works on sorted and unsorted lists.
- Checks each element until a match is found.
- Returns `-1` if the target is missing.
- Worst-case time complexity: `O(n)`.

---

## Searching Strings

### Finding a Substring

```python
text = "hello world"

text.find("world")     # 6
text.find("hello")     # 0
text.find("python")    # -1
```

### Finding the Last Occurrence

```python
text = "banana"

text.rfind("ana")      # 3
```

### Using `.index()`

```python
text = "hello world"

text.index("world")    # 6
```

Unlike `.find()`, `.index()` raises `ValueError` when no match exists.

### Counting Occurrences

```python
text = "banana"

text.count("a")        # 3
text.count("ana")      # 1
```

**Important:** `.count()` counts non-overlapping substring matches.

### Searching With Slicing

```python
text = "banana"

text[1:4]             # 'ana'
text[3:6]             # 'ana'
```

Slicing is useful when comparing fixed-length patterns at different positions.

### Searching With Conditions

```python
words = ["hello", "world", "python"]

matches = [word for word in words if "o" in word]
# ['hello', 'world', 'python']
```

---

## Searching Dictionaries and Sets

### Dictionary Key Search

```python
scores = {"Alex": 10, "Sam": 20}

"Alex" in scores      # True
"Jo" in scores        # False
```

### Dictionary Value Search

```python
20 in scores.values()
# True
```

### Safe Dictionary Lookup

```python
scores.get("Alex")       # 10
scores.get("Jo")         # None
scores.get("Jo", 0)      # 0
```

### Set Search

```python
numbers = {10, 20, 30}

20 in numbers       # True
50 in numbers       # False
```

Dictionary-key and set membership checks are typically faster than list searches for larger collections.

---

## Binary Search

Binary search finds a target by repeatedly dividing the search range in half.

**Important:** The input must already be sorted in ascending order.

### How Binary Search Works

Consider:

```python
numbers = [10, 20, 30, 40, 50]
```

Searching for `40`:

1. Check the middle element, `30`.
2. Since `40` is greater than `30`, search the right half.
3. Check `40` and return its index.

### Binary Search Implementation

```python
def binary_search(numbers: list[int], target: int) -> int:
    left = 0
    right = len(numbers) - 1

    while left <= right:
        middle = (left + right) // 2

        if numbers[middle] == target:
            return middle

        elif numbers[middle] < target:
            left = middle + 1

        else:
            right = middle - 1

    return -1
```

**Examples:**

```python
binary_search([10, 20, 30, 40, 50], 40)
# 3

binary_search([10, 20, 30, 40, 50], 15)
# -1

binary_search([], 10)
# -1
```

This implementation returns an index containing the target. If duplicates exist, it does not guarantee the first occurrence.

**Time complexity:** `O(log n)`.

---

## Using `bisect`

Python's `bisect` module helps search for insertion positions in sorted lists.

```python
import bisect

numbers = [1, 2, 2, 4, 5]
```

### `bisect_left()`

Returns the first position where a value could be inserted while maintaining sorted order.

```python
bisect.bisect_left(numbers, 2)
# 1
```

### `bisect_right()`

Returns the position after any existing copies of that value.

```python
bisect.bisect_right(numbers, 2)
# 3
```

### Inserting in Sorted Order

```python
numbers = [1, 3, 5]

bisect.insort(numbers, 4)

# [1, 3, 4, 5]
```

`bisect` finds insertion positions efficiently, but insertion into a list may still require shifting elements.

---

## Finding Minimum and Maximum Values

### Basic Usage

```python
numbers = [10, 50, 20, 40]

min(numbers)    # 10
max(numbers)    # 50
```

### Finding the Longest Word

```python
words = ["cat", "elephant", "dog"]

max(words, key=len)
# 'elephant'
```

### Finding the Highest Score

```python
scores = {
    "Alex": 10,
    "Sam": 30,
    "Jo": 20
}

max(scores, key=scores.get)
# 'Sam'
```

### Avoiding Errors With Empty Collections

```python
max([], default=None)
# None
```

Without `default`, calling `max()` or `min()` on an empty collection raises `ValueError`.

---

## Finding the Top N Results

```python
scores = [
    ("Alex", 10),
    ("Sam", 30),
    ("Jo", 20),
    ("Ben", 40)
]

ordered = sorted(scores, key=lambda item: item[1], reverse=True)

top_two = ordered[:2]

# [('Ben', 40), ('Sam', 30)]
```

### Finding the Three Largest Numbers

```python
numbers = [10, 50, 20, 40, 30]

sorted(numbers, reverse=True)[:3]
# [50, 40, 30]
```

---

## Searching With `any()` and `all()`

### `any()`

Returns `True` when at least one element satisfies a condition.

```python
numbers = [1, 3, 5, 8]

any(n % 2 == 0 for n in numbers)
# True
```

### `all()`

Returns `True` when every element satisfies a condition.

```python
numbers = [2, 4, 6]

all(n % 2 == 0 for n in numbers)
# True
```

### Difference

```python
any([False, False, True])    # True
all([True, True, False])     # False
```

---

## Sorting and Searching Complexity

Big O describes how the time required by an operation grows as the input becomes larger.

| Operation | Typical Time Complexity |
|---|---|
| Access list element by index | `O(1)` |
| Search unsorted list | `O(n)` |
| Find item using `list.index()` | `O(n)` |
| Search set or dictionary key | `O(1)` average |
| Sort using `sorted()` | `O(n log n)` |
| Sort using `.sort()` | `O(n log n)` |
| Binary search | `O(log n)` |
| Find minimum or maximum | `O(n)` |
| Binary search insertion into a list | `O(n)` overall |

`n` represents the number of elements.

---

## Common Gotchas

### 1. `.sort()` Returns `None`

```python
numbers = [3, 1, 2]

result = numbers.sort()

print(result)    # None
print(numbers)   # [1, 2, 3]
```

Use `sorted(numbers)` if you need a new sorted list.

### 2. Strings Are Sorted Case-Sensitively

```python
sorted(["apple", "Banana", "cherry"])
# ['Banana', 'apple', 'cherry']
```

Use `key=str.lower` for case-insensitive sorting.

### 3. `.index()` Raises an Error if Missing

```python
numbers = [1, 2, 3]

# numbers.index(5)  # ValueError
```

Check membership first if the element might be missing.

### 4. Binary Search Requires Sorted Data

```python
numbers = [30, 10, 50, 20]
```

Binary search cannot be relied upon to work correctly on this unsorted list.

### 5. Sorting Numeric Strings

```python
numbers = ["10", "2", "30"]

sorted(numbers)
# ['10', '2', '30']
```

This sorts the values as strings.

To sort them numerically:

```python
sorted(numbers, key=int)
# ['2', '10', '30']
```

### 6. `reverse=True` Reverses the Entire Sort Order

```python
records = [("Alex", 20), ("Sam", 20)]

sorted(records, reverse=True)
# [('Sam', 20), ('Alex', 20)]
```

For score descending and name ascending, use a suitable `key` instead.

---

## Common Recipes

### Find All Occurrences of a Value

```python
numbers = [1, 2, 3, 2, 4]

indexes = [i for i, n in enumerate(numbers) if n == 2]
# [1, 3]
```

### Sort Numbers Without Changing the Original

```python
numbers = [5, 1, 3]

ordered = sorted(numbers)
# [1, 3, 5]
```

### Sort Tuples by Their Second Value

```python
records = [("Alex", 10), ("Sam", 30)]

sorted(records, key=lambda item: item[1])
# [('Alex', 10), ('Sam', 30)]
```

### Sort by Two Conditions

```python
records = [("Sam", 20), ("Alex", 20), ("Jo", 30)]

sorted(records, key=lambda item: (-item[1], item[0]))
# [('Jo', 30), ('Alex', 20), ('Sam', 20)]
```

### Find the First Matching Value

```python
numbers = [1, 3, 6, 9]

result = next((n for n in numbers if n > 5), None)
# 6
```

### Check Whether Two Lists Share an Element

```python
a = [1, 2, 3]
b = [3, 4, 5]

bool(set(a) & set(b))
# True
```

### Check if a List Is Already Sorted

```python
numbers = [1, 2, 3, 4]

numbers == sorted(numbers)
# True
```

### Find the Second Largest Distinct Value

```python
numbers = [10, 30, 20, 30]

unique = sorted(set(numbers), reverse=True)

unique[1]
# 20
```

This assumes there are at least two distinct values.

---

## Quick Reference

| Task | Method / Function |
|---|---|
| Sort without modifying original | `sorted()` |
| Sort list in place | `.sort()` |
| Sort descending | `reverse=True` |
| Sort by custom rule | `key=` |
| Sort by second tuple element | `key=lambda x: x[1]` |
| Find first occurrence | `.index()` |
| Search substring | `.find()` |
| Find last substring occurrence | `.rfind()` |
| Check membership | `in` |
| Get index and value | `enumerate()` |
| Find largest value | `max()` |
| Find smallest value | `min()` |
| Find first matching element | `next()` |
| Check if any element matches | `any()` |
| Check if all elements match | `all()` |
| Binary search insertion position | `bisect_left()` |
| Find top N values | `sorted(..., reverse=True)[:n]` |

**Key idea:** Understand the difference between sorting and searching, how to choose the correct technique and when to use Python's built-in functions rather than implementing an algorithm manually.
