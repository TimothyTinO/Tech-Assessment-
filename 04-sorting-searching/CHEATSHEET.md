# Python Collections Cheatsheet

This cheatsheet focuses on **tuples and dictionaries**, including how to create, access, modify and iterate through data.

## Tuples

Tuples store multiple values in a fixed order. Unlike lists, tuples cannot be modified after they are created.

### Creating Tuples

```python
person = ("Alex", 25)
scores = (10, 20, 30)
empty = ()

single = (5,)  # Single-element tuple
```

### Indexing and Slicing

```python
values = (10, 20, 30, 40)

values[0]      # 10
values[-1]     # 40
values[1:3]    # (20, 30)
values[::-1]   # (40, 30, 20, 10)
```

### Tuple Unpacking

```python
person = ("Alex", 25)

name, age = person

print(name)  # Alex
print(age)   # 25
```

### Iterating Through Tuples

```python
records = [
    ("Alex", 10),
    ("Sam", 20),
    ("Jo", 30)
]

for name, score in records:
    print(name, score)
```

### Tuple Methods

```python
numbers = (1, 2, 2, 3)

numbers.count(2)    # 2
numbers.index(3)    # 3
len(numbers)        # 4
```

### Tuples Cannot Be Modified

```python
person = ("Alex", 25)

# person[0] = "Sam"  # TypeError
```

Tuples are useful when storing related values such as `(name, score)` or `(x, y)`.

---

## Dictionaries

Dictionaries store information using **key-value pairs**.

### Creating Dictionaries

```python
person = {
    "name": "Alex",
    "age": 25,
    "city": "London"
}

empty = {}
```

### Accessing Values

```python
person = {"name": "Alex", "age": 25}

person["name"]         # "Alex"
person["age"]          # 25
person.get("name")     # "Alex"
person.get("city")     # None
person.get("city", "") # ""
```

`.get()` is useful when a key might not exist.

### Adding and Updating Values

```python
scores = {"Alex": 10}

scores["Sam"] = 20
# {"Alex": 10, "Sam": 20}

scores["Alex"] = 30
# {"Alex": 30, "Sam": 20}
```

### Removing Values

```python
scores = {"Alex": 10, "Sam": 20}

scores.pop("Alex")  # Returns 10
# {"Sam": 20}

del scores["Sam"]
# {}
```

### Common Dictionary Methods

```python
scores = {"Alex": 10, "Sam": 20}

scores.keys()
# dict_keys(['Alex', 'Sam'])

scores.values()
# dict_values([10, 20])

scores.items()
# dict_items([('Alex', 10), ('Sam', 20)])
```

### Checking if a Key Exists

```python
scores = {"Alex": 10, "Sam": 20}

"Alex" in scores       # True
"Jo" in scores         # False
"Jo" not in scores     # True
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

Using `.get()`:

```python
counts = {}

for name in names:
    counts[name] = counts.get(name, 0) + 1

# {"Alex": 3, "Sam": 1, "Jo": 1}
```

### Combining Scores

```python
records = [
    ("Alex", 10),
    ("Sam", 20),
    ("Alex", 15)
]

totals = {}

for name, score in records:
    totals[name] = totals.get(name, 0) + score

# {"Alex": 25, "Sam": 20}
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

---

## Common Gotchas

### Accessing Missing Keys

```python
scores = {"Alex": 10}

# scores["Sam"]    # KeyError

scores.get("Sam")  # None
```

### Duplicate Dictionary Keys

```python
scores = {
    "Alex": 10,
    "Alex": 20
}

# {"Alex": 20}
```

The latest value replaces the earlier one.

### Checking Whether a Dictionary Is Empty

```python
scores = {}

if not scores:
    print("No scores available")
```

### Remember the Difference

```python
person = ("Alex", 25)       # Tuple
person = {"Alex": 25}       # Dictionary
```

A tuple stores values by position. A dictionary stores values by key.

---

## Quick Reference

| Task | Python |
|---|---|
| Access tuple element | `tuple[0]` |
| Unpack tuple | `name, age = person` |
| Count tuple values | `.count()` |
| Find tuple position | `.index()` |
| Access dictionary value | `dict[key]` |
| Access safely | `.get()` |
| Add or update a value | `dict[key] = value` |
| Remove a key | `.pop()` |
| Get all keys | `.keys()` |
| Get all values | `.values()` |
| Get key-value pairs | `.items()` |
| Check if key exists | `key in dict` |
| Count occurrences | `counts.get(key, 0) + 1` |

**Key idea:** Tuples are useful for grouping related values, while dictionaries are useful for looking up information and counting or combining values.
