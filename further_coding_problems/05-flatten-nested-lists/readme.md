# Flatten Nested Lists

You're cleaning up data for _Russian Doll Records_. Their data arrives as lists inside lists inside lists, and nobody knows how deep it goes.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Flatten

Write `flatten(items)` that takes a list which may contain other lists (nested to **any** depth) and returns a single flat list of all the non-list items, in their original order.

Strings are **not** lists for this problem. Don't split them up.

**Examples:**
```python
flatten([1, [2, [3, 4]], 5])
# Returns: [1, 2, 3, 4, 5]

flatten(["a", ["b", ["c"]]])
# Returns: ["a", "b", "c"]

flatten([])
# Returns: []

flatten([[], [[]]])
# Returns: []
```

## Step 2: How Deep?

Write `depth(items)` that returns how deeply nested the data is.

- Anything that isn't a list has depth `0`.
- A list has a depth of `1` plus the depth of its deepest item.
- An empty list has depth `1`.

**Examples:**
```python
depth(5)                  # 0
depth([])                 # 1
depth([1, 2, 3])          # 1
depth([1, [2, [3]]])      # 3
depth([[], [[]]])         # 3
```

## Step 3: Flatten Only Some Levels

Write `flatten_to_depth(items, levels)` that only flattens `levels` levels of nesting and leaves anything deeper alone.

- `levels=0` returns the list unchanged (as a new list).
- A very large `levels` behaves like `flatten`.

**Examples:**
```python
flatten_to_depth([1, [2, [3, [4]]]], 1)
# Returns: [1, 2, [3, [4]]]

flatten_to_depth([1, [2, [3, [4]]]], 2)
# Returns: [1, 2, 3, [4]]

flatten_to_depth([1, [2, [3, [4]]]], 0)
# Returns: [1, [2, [3, [4]]]]

flatten_to_depth([1, [2, [3, [4]]]], 99)
# Returns: [1, 2, 3, 4]
```

## 💡 Hints

1. This is a job for **recursion**: a function that calls itself.
2. Every recursive function needs a stopping point (a "base case"). Here it's an item that isn't a list.
3. `isinstance(item, list)` tells you whether something is a list.
4. For `flatten`: for each item, if it's a list, flatten it too and add the results. Otherwise just add the item.
5. For `depth`, the answer for a list is `1 + max(...)` of the depths of its items. Be careful with an empty list, since `max([])` raises an error. `max(..., default=0)` helps.
6. For `flatten_to_depth`, pass `levels - 1` into the recursive call, and stop flattening when `levels` reaches 0.
