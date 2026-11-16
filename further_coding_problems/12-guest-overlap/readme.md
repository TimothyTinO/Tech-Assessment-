# Guest Overlap

You're helping _Party Planners Inc._ compare guest lists from different events, to see who's coming to what.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Compare Two Lists

Write `compare_lists(a, b)` that takes two lists of names and returns a dictionary with three keys:

- `"both"`: names in both lists
- `"only_a"`: names only in the first list
- `"only_b"`: names only in the second list

Each value is an alphabetically sorted list with no duplicates.

**Examples:**
```python
compare_lists(["ann", "bob", "cy"], ["bob", "dee", "cy"])
# Returns:
# {"both": ["bob", "cy"], "only_a": ["ann"], "only_b": ["dee"]}

compare_lists(["a", "a"], ["a"])
# Returns:
# {"both": ["a"], "only_a": [], "only_b": []}

compare_lists([], [])
# Returns:
# {"both": [], "only_a": [], "only_b": []}
```

## Step 2: Messy Names

Real guest lists are messy. Make `compare_lists` ignore upper/lower case and any spaces at the start or end of a name. Names in the result should be lowercase.

**Examples:**
```python
compare_lists([" Ann", "BOB"], ["bob ", "Dee"])
# Returns:
# {"both": ["bob"], "only_a": ["ann"], "only_b": ["dee"]}

compare_lists(["ANN", "ann", " Ann "], ["Ann"])
# Returns:
# {"both": ["ann"], "only_a": [], "only_b": []}
```

## Step 3: Many Events

Write `compare_many(lists)` that takes a list of guest lists (any number of them) and returns a dictionary with:

- `"everyone"`: names that appear in **every** list
- `"anyone"`: names that appear in **at least one** list
- `"exactly_one"`: names that appear in **exactly one** list

Clean the names like in Step 2. A name repeated inside one list only counts once for that list. All values are sorted lists.

**Examples:**
```python
compare_many([["ann", "bob"], ["bob", "cy"], ["bob", "ann", "dee"]])
# Returns:
# {"everyone": ["bob"],
#  "anyone": ["ann", "bob", "cy", "dee"],
#  "exactly_one": ["cy", "dee"]}

compare_many([["Ann"], ["ann", "ann"]])
# Returns:
# {"everyone": ["ann"], "anyone": ["ann"], "exactly_one": []}

compare_many([])
# Returns:
# {"everyone": [], "anyone": [], "exactly_one": []}
```

## 💡 Hints

1. Python has a built-in `set` type that removes duplicates automatically: `set(["a", "a", "b"])` is `{"a", "b"}`.
2. Sets have operators for exactly this problem: `a & b` (in both), `a - b` (only in a), `a | b` (in either).
3. Convert a set back to a sorted list with `sorted(my_set)`.
4. To clean a name: `name.strip().lower()`. You can do this for a whole list in one line with a list comprehension.
5. For Step 3, turn each list into a set first. `set.intersection(*sets)` and `set.union(*sets)` work on many sets at once.
6. For `exactly_one`, count how many sets each name appears in. A dictionary works well, or compare "union" against names that appear more than once.
