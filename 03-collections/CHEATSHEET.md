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

Sets store unique values and do not guarantee
