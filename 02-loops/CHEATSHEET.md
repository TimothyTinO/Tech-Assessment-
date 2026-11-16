# **Python Loops Cheatsheet**

## **For Loops**
Iterate over any iterable (list, tuple, string, dictionary, set, etc.).

```python
for item in iterable:
    # Execute code for each item

for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 6):       # 2, 3, 4, 5
    print(i)

for i in range(0, 10, 2):   # 0, 2, 4, 6, 8
    print(i)

for i in range(5, 0, -1):   # 5, 4, 3, 2, 1
    print(i)
```

## **While Loops**
Repeat code while a condition is `True`.

```python
while condition:
    # Execute code
    # Update condition to avoid infinite loop

count = 0
while count < 5:
    print(count)
    count += 1
```

# Key points:
- The condition is checked before each iteration.
- A while loop may execute zero times.
- Ensure the condition eventually becomes `False`.
- Useful when the number of iterations is not known in advance.

## **The range() Function**

Generates a sequence of integers, commonly used with `for` loops.

```python
range(stop)              # Starts at 0
range(start, stop)       # Custom start and stop
range(start, stop, step) # Custom increment

list(range(5))           # [0, 1, 2, 3, 4]
list(range(2, 6))        # [2, 3, 4, 5]
list(range(1, 10, 2))    # [1, 3, 5, 7, 9]
list(range(5, 0, -1))    # [5, 4, 3, 2, 1]
list(range(0))           # []
```

# Important:The stop value is excluded. The step cannot be zero.

## **Loop Control Statements**

### break
Immediately exits the innermost loop.

```python
for i in range(10):
    if i == 5:
        break
    print(i)             # 0, 1, 2, 3, 4
```

### continue
Skips the current iteration and moves to the next one.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)             # 0, 1, 3, 4
```

### pass
Does nothing. Used as a placeholder.

```python
for i in range(5):
    pass
```

## **Nested Loops**

A loop inside another loop.

```python
for i in range(3):
    for j in range(2):
        print(i, j)

# Inner loop completes all iterations
# for every iteration of the outer loop
```
### Nested Loop Example

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(i * j)
```

# Remember: The total number of iterations is the product of the iterations of each loop.

## **Looping Through Collections**

### Lists
```python
numbers = [10, 20, 30]

for num in numbers:
    print(num)
```

### Strings
```python
for char in "Python":
    print(char)
```

### Tuples
```python
for item in (1, 2, 3):
    print(item)
```

### Dictionaries
```python
person = {"name": "Alice", "age": 30}

for key in person:
    print(key)

for value in person.values():
    print(value)

for key, value in person.items():
    print(key, value)
```

### Sets
```python
for item in {1, 2, 3}:
    print(item)
# Sets are unordered collections
```

## **Useful Loop Functions**

### enumerate()

Returns both the index and value when iterating.

```python
names = ["Alice", "Bob", "Charlie"]

for index, name in enumerate(names):
    print(index, name)

for index, name in enumerate(names, start=1):
    print(index, name)
```

### zip()

Iterates over multiple iterables simultaneously.

```python
names = ["Alice", "Bob"]
scores = [85, 90]

for name, score in zip(names, scores):
    print(name, score)

# Stops when the shortest iterable is exhausted
```

### reversed()

Iterates through an iterable in reverse order.

```python
for i in reversed([1, 2, 3]):
    print(i)             # 3, 2, 1
```

### sorted()

Returns a sorted list from an iterable.

```python
for num in sorted([3, 1, 2]):
    print(num)           # 1, 2, 3
```

## **Loop Else Clause**

Python supports an optional `else` clause with loops.

The `else` block executes when the loop finishes normally, but not when it exits using `break`.

```python
for i in range(5):
    print(i)
else:
    print("Loop completed")

# With break
for i in range(5):
    if i == 3:
        break
else:
    print("This will not execute")
```

The same behaviour applies to `while` loops.

## **List Comprehensions**

A concise way to create lists using iteration.

```python
# Basic syntax
[expression for item in iterable]

# With condition
[expression for item in iterable if condition]

# Examples
squares = [x**2 for x in range(5)]

evens = [x for x in range(10) if x % 2 == 0]

words = [word.upper() for word in ["hello", "world"]]

# Nested comprehension
pairs = [(x, y) for x in range(2) for y in range(2)]
```

## **Common Loop Patterns**

```python
# Counter
count = 0
for item in iterable:
    count += 1

# Accumulator (running total)
total = 0
for num in numbers:
    total += num

# Conditional filtering
result = []
for num in numbers:
    if num > 0:
        result.append(num)

# Finding an item
for item in iterable:
    if condition:
        # Item found
        break

# Tracking minimum / maximum
smallest = numbers[0]
for num in numbers:
    if num < smallest:
        smallest = num

# Check if any item matches
found = False
for item in iterable:
    if condition:
        found = True
        break
```

## **Useful Built-ins**

```python
len([1, 2, 3])          # 3 (number of items)
sum([1, 2, 3])          # 6 (total)
min([1, 2, 3])          # 1 (smallest)
max([1, 2, 3])          # 3 (largest)
any([False, True])      # True (at least one True)
all([True, True])       # True (all True)
list(range(5))          # [0, 1, 2, 3, 4]
next(iter([1, 2, 3]))   # 1 (next item)
```