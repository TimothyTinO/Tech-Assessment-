# Python Collections Cheatsheet

Collections are used to store multiple values in a single variable. The four main built-in collection types in Python are **lists, tuples, dictionaries and sets**.

## Collection Types

| Type | Ordered | Mutable | Allows Duplicates |
|---|---|---|---|
| List | Yes | Yes | Yes |
| Tuple | Yes | No | Yes |
| Dictionary | Yes (insertion order) | Yes | Keys must be unique |
| Set | No guaranteed order | Yes | No |

**Mutable** means the collection can be changed after it has been created.

## Lists

### Creating Lists

```python
numbers = [1, 2, 3, 4]
names = ["Alex", "Sam", "Jo"]
mixed = [1, "hello", True]
empty = []

numbers = list((1, 2, 3))  # [1, 2, 3]
zeros = [0] * 4            # [0, 0, 0, 0]
sequence = list(range(5))  # [0, 1, 2, 3, 4]
```

Lists are ordered, mutable and allow duplicate values.

### Accessing Elements

```python
numbers = [10, 20, 30, 40, 50]

numbers[0]       # 10
numbers[2]       # 30
numbers[-1]      # 50 (last element)
numbers[-2]      # 40
len(numbers)      # 5
```

### List Slicing

```python
numbers = [10, 20, 30, 40, 50]

numbers[1:4]     # [20, 30, 40]
numbers[:3]      # [10, 20, 30]
numbers[2:]      # [30, 40, 50]
numbers[::2]     # [10, 30, 50]
numbers[::-1]    # [50, 40, 30, 20, 10]
numbers[:]       # Shallow copy of the list
```

Slicing follows the format `list[start:stop:step]`. The `stop` index is excluded.

### Adding Elements

```python
numbers = [1, 2, 3]

numbers.append(4)
# [1, 2, 3, 4]

numbers.extend([5, 6])
# [1, 2, 3, 4, 5, 6]

numbers.insert(1, 10)
# [1, 10, 2, 3, 4, 5, 6]
```

**Difference between `append()` and `extend()`:**

```python
a = [1, 2]
a.append([3, 4])
# [1, 2, [3, 4]]

b = [1, 2]
b.extend([3, 4])
# [1, 2, 3, 4]
```

`append()` adds one item, while `extend()` adds each element from an iterable.

### Removing Elements

```python
numbers = [10, 20, 30, 20]

numbers.remove(20)
# [10, 30, 20] (removes first occurrence)

numbers.pop()
# Returns 20, list becomes [10, 30]

numbers.pop(0)
# Returns 10, list becomes [30]

numbers.clear()
# []
```

```python
numbers = [10, 20, 30]

del numbers[1]
# [10, 30]
```

`remove()` raises `ValueError` if the value is missing. `pop()` raises `IndexError` if the index is invalid.

### Updating Values

```python
numbers = [10, 20, 30]

numbers[0] = 100
# [100, 20, 30]

numbers[1:3] = [5, 6]
# [100, 5, 6]
```

### Common List Methods

```python
numbers = [3, 1, 2, 1]

numbers.count(1)       # 2
numbers.index(2)       # 2
len(numbers)           # 4
sum(numbers)           # 7
min(numbers)           # 1
max(numbers)           # 3

numbers.sort()
# [1, 1, 2, 3]

numbers.reverse()
# [3, 2, 1, 1]
```

### Iterating Through Lists

```python
names = ["Alex", "Sam", "Jo"]

for name in names:
    print(name)
```

Using indexes:

```python
for i in range(len(names)):
    print(i, names[i])
```

Using `enumerate()`:

```python
for i, name in enumerate(names):
    print(i, name)

# 0 Alex
# 1 Sam
# 2 Jo
```

Starting from a different index:

```python
for i, name in enumerate(names, start=1):
    print(i, name)

# 1 Alex
# 2 Sam
# 3 Jo
```

### List Comprehensions

List comprehensions provide a shorter way of creating lists.

```python
numbers = [1, 2, 3, 4]

squares = [n * n for n in numbers]
# [1, 4, 9, 16]

evens = [n for n in numbers if n % 2 == 0]
# [2, 4]

doubled = [n * 2 for n in numbers]
# [2, 4, 6, 8]
```

Equivalent to:

```python
squares = []

for n in numbers:
    squares.append(n * n)
```

### Nested Lists

A nested list is a list containing other lists.

```python
grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

grid[0]       # [1, 2, 3]
grid[0][1]    # 2
grid[2][2]    # 9
```

Iterating through a nested list:

```python
for row in grid:
    for value in row:
        print(value)
```

Using row and column indexes:

```python
for row in range(len(grid)):
    for col in range(len(grid[row])):
        print(grid[row][col])
```

### Creating a Two-Dimensional List

```python
grid = [[0] * 3 for _ in range(3)]

# [
#     [0, 0, 0],
#     [0, 0, 0],
#     [0, 0, 0]
# ]
```

Avoid this when creating independently editable rows:

```python
grid = [[0] * 3] * 3
```

All three rows would reference the same inner list. Changing one row could unexpectedly change the others.

---

## Tuples

Tuples are ordered collections that cannot be modified after creation.

### Creating Tuples

```python
coordinates = (10, 20)
names = ("Alex", "Sam", "Jo")
empty = ()

single = (5,)       # One-element tuple
not_tuple = (5)     # Integer
```

### Accessing and Slicing

```python
values = (10, 20, 30, 40)

values[0]       # 10
values[-1]      # 40
values[1:3]     # (20, 30)
values[::-1]    # (40, 30, 20, 10)
```

### Tuple Methods

```python
numbers = (1, 2, 2, 3)

numbers.count(2)     # 2
numbers.index(3)     # 3
len(numbers)         # 4
```

### Tuple Unpacking

```python
person = ("Alex", 25)

name, age = person

name    # "Alex"
age     # 25
```

Swapping variables:

```python
a = 10
b = 20

a, b = b, a

# a = 20
# b = 10
```

### Returning Multiple Values

```python
def get_details():
    return "Alex", 25

name, age = get_details()
```

The function returns a tuple containing both values.

### Lists vs Tuples

```python
scores = [10, 20, 30]
scores[0] = 100     # Allowed

point = (10, 20)
# point[0] = 100    # TypeError
```

**When to use tuples:** When a collection represents a fixed group of related values, such as `(name, score)` or `(row, column)`.

---

## Dictionaries

Dictionaries store data as key-value pairs.

### Creating Dictionaries

```python
person = {
    "name": "Alex",
    "age": 25,
    "city": "London"
}

empty = {}

scores = dict(Alex=10, Sam=20)
# {"Alex": 10, "Sam": 20}
```

Keys must be unique and hashable. Values can be of any type.

### Accessing Values

```python
person = {"name": "Alex", "age": 25}

person["name"]          # "Alex"
person.get("name")      # "Alex"
person.get("city")      # None
person.get("city", "")  # ""
```

**Difference:**

```python
person["city"]      # KeyError

person.get("city")  # None
```

Use `.get()` when a key might not exist.

### Adding and Updating Values

```python
person = {"name": "Alex"}

person["age"] = 25
# {"name": "Alex", "age": 25}

person["name"] = "Sam"
# {"name": "Sam", "age": 25}
```

### Removing Values

```python
person = {
    "name": "Alex",
    "age": 25,
    "city": "London"
}

person.pop("age")       # Returns 25
# {"name": "Alex", "city": "London"}

del person["city"]
# {"name": "Alex"}

person.clear()
# {}
```

### Common Dictionary Methods

```python
scores = {
    "Alex": 10,
    "Sam": 20,
    "Jo": 15
}

scores.keys()
# dict_keys(["Alex", "Sam", "Jo"])

scores.values()
# dict_values([10, 20, 15])

scores.items()
# dict_items([("Alex", 10), ("Sam", 20), ("Jo", 15)])
```

Checking whether a key exists:

```python
"Alex" in scores         # True
"Ben" not in scores      # True
```

Checking for a value:

```python
20 in scores.values()    # True
```

### Iterating Through Dictionaries

```python
scores = {"Alex": 10, "Sam": 20}

for name in scores:
    print(name)
```

Accessing keys and values together:

```python
for name, score in scores.items():
    print(name, score)

# Alex 10
# Sam 20
```

### Counting Occurrences

A common technical assessment problem is counting how many times an item appears.

```python
names = ["Alex", "Sam", "Alex", "Jo", "Alex"]

counts = {}

for name in names:
    if name in counts:
        counts[name] += 1
    else:
        counts[name] = 1

# {"Alex": 3, "Sam": 1, "Jo": 1}
```

Shorter version using `.get()`:

```python
counts = {}

for name in names:
    counts[name] = counts.get(name, 0) + 1
```

### Grouping Values

```python
records = [
    ("Alex", 10),
    ("Sam", 20),
    ("Alex", 15)
]

scores = {}

for name, score in records:
    scores.setdefault(name, []).append(score)

# {
#     "Alex": [10, 15],
#     "Sam": [20]
# }
```

### Dictionary Comprehensions

```python
numbers = [1, 2, 3]

squares = {n: n * n for n in numbers}

# {1: 1, 2: 4, 3: 9}
```

### Nested Dictionaries

```python
students = {
    "Alex": {"age": 20, "score": 85},
    "Sam": {"age": 21, "score": 90}
}

students["Alex"]["score"]  # 85
students["Sam"]["age"]     # 21
```

### Combining Dictionaries

```python
a = {"x": 1, "y": 2}
b = {"y": 5, "z": 3}

merged = a | b
# {"x": 1, "y": 5, "z": 3}
```

Values from `b` replace matching values from `a`.

---

## Sets

Sets store unique values and do not guarantee an element order.

### Creating Sets

```python
numbers = {1, 2, 3}
empty = set()

unique = set([1, 2, 2, 3])
# {1, 2, 3}
```

### Adding and Removing

```python
numbers = {1, 2, 3}

numbers.add(4)
# {1, 2, 3, 4}

numbers.remove(2)
# {1, 3, 4}

numbers.discard(10)  # No error if missing
```

`remove()` raises `KeyError` when the element does not exist, while `discard()` does not.

### Set Operations

```python
a = {1, 2, 3}
b = {3, 4, 5}

a | b     # {1, 2, 3, 4, 5} (union)
a & b     # {3}             (intersection)
a - b     # {1, 2}          (difference)
a ^ b     # {1, 2, 4, 5}    (symmetric difference)
```

### Membership Checks

```python
numbers = {1, 2, 3}

2 in numbers     # True
5 in numbers     # False
```

Set membership is typically faster than searching through a list when working with large collections.

---

## Common Collection Operations

### Length

```python
len([1, 2, 3])            # 3
len((1, 2, 3))            # 3
len({"a": 1, "b": 2})     # 2
len({1, 2, 3})            # 3
```

### Membership

```python
2 in [1, 2, 3]           # True
2 in (1, 2, 3)           # True
"a" in {"a": 10}         # True
2 in {1, 2, 3}           # True
```

For dictionaries, `in` checks keys rather than values.

### Combining Collections

```python
[1, 2] + [3, 4]
# [1, 2, 3, 4]

(1, 2) + (3, 4)
# (1, 2, 3, 4)

{1, 2} | {2, 3}
# {1, 2, 3}
```

### Converting Between Collections

```python
list((1, 2, 3))      # [1, 2, 3]
tuple([1, 2, 3])     # (1, 2, 3)
set([1, 2, 2, 3])    # {1, 2, 3}
list("abc")          # ['a', 'b', 'c']
```

### Using `zip()`

`zip()` combines elements from multiple iterables by position.

```python
names = ["Alex", "Sam", "Jo"]
scores = [10, 20, 30]

list(zip(names, scores))

# [
#     ("Alex", 10),
#     ("Sam", 20),
#     ("Jo", 30)
# ]
```

### Unpacking with `*`

```python
numbers = [1, 2, 3, 4]

first, *middle, last = numbers

first     # 1
middle    # [2, 3]
last      # 4
```

---

## Common Gotchas

### 1. Lists Are Mutable

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
# [1, 2, 3, 4]
```

Both variables reference the same list.

Create a shallow copy if an independent outer list is needed:

```python
a = [1, 2, 3]
b = a.copy()
```

For nested lists, use `copy.deepcopy()` if the nested objects must also be independent.

### 2. List Methods Often Return `None`

```python
numbers = [3, 1, 2]

result = numbers.sort()

print(result)   # None
print(numbers)  # [1, 2, 3]
```

Methods such as `append()`, `extend()` and `sort()` modify the list in place.

### 3. Dictionary Keys Must Be Unique

```python
data = {
    "Alex": 10,
    "Alex": 20
}

# {"Alex": 20}
```

The later value replaces the earlier one.

### 4. Sets Do Not Support Indexing

```python
numbers = {10, 20, 30}

# numbers[0]  # TypeError
```

### 5. Empty Collections

```python
bool([])       # False
bool(())       # False
bool({})       # False
bool(set())    # False
```

### 6. Avoid Mutable Default Arguments

```python
# Avoid:
def add_item(value, items=[]):
    items.append(value)
    return items
```

The same list can be reused across function calls.

Use:

```python
def add_item(value, items=None):
    if items is None:
        items = []

    items.append(value)
    return items
```

---

## Common Recipes

### Remove Duplicates While Preserving Order

```python
numbers = [1, 2, 2, 3, 1]

unique = list(dict.fromkeys(numbers))
# [1, 2, 3]
```

### Flatten a Nested List

```python
nested = [[1, 2], [3, 4], [5]]

flat = [value for row in nested for value in row]
# [1, 2, 3, 4, 5]
```

### Find Common Elements

```python
a = [1, 2, 3]
b = [2, 3, 4]

common = set(a) & set(b)
# {2, 3}
```

### Find the Largest Value in a Dictionary

```python
scores = {"Alex": 10, "Sam": 30, "Jo": 20}

winner = max(scores, key=scores.get)
# "Sam"
```

### Convert a List of Tuples Into a Dictionary

```python
records = [("Alex", 10), ("Sam", 20)]

scores = dict(records)
# {"Alex": 10, "Sam": 20}
```

### Check if a Collection Is Empty

```python
numbers = []

if not numbers:
    print("Empty collection")
```

### Find the Number of Unique Elements

```python
numbers = [1, 2, 2, 3, 3, 3]

len(set(numbers))
# 3
```

### Build a List of Index-Value Pairs

```python
names = ["Alex", "Sam", "Jo"]

positions = list(enumerate(names))
# [(0, "Alex"), (1, "Sam"), (2, "Jo")]
```

---

## Quick Reference

| Task | Method / Function |
|---|---|
| Add one item to a list | `append()` |
| Add multiple items | `extend()` |
| Remove a list item by value | `remove()` |
| Remove by index | `pop()` |
| Find an element's index | `index()` |
| Count occurrences | `count()` |
| Reverse a list in place | `reverse()` |
| Create a shallow list copy | `copy()` |
| Access dictionary safely | `get()` |
| Loop through dictionary pairs | `items()` |
| Add a value to a set | `add()` |
| Remove duplicates | `set()` |
| Get index and value | `enumerate()` |
| Combine iterables | `zip()` |
| Find collection length | `len()` |

**Key idea:** Choose the right collection for the problem. Lists are useful for ordered sequences, tuples for fixed groups of values, dictionaries for key-value relationships and sets for unique values.
