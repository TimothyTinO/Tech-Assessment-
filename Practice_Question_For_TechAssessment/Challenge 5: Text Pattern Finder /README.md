# Challenge 5: Text Pattern Finder

Create a program that searches through text and identifies the positions where particular character sequences appear. Build your solution step by step, starting with basic string searching before introducing case-insensitive matching, wildcards and multiple search patterns.

## Background

A company developing text-processing software wants to create a tool that searches through documents and identifies where particular words or character sequences appear.

For example, consider the following text:

```python
"banana"
```

Searching for `"ana"` should return:

```python
[1, 3]
```

This is because the pattern appears twice, starting at indexes `1` and `3`. Notice that the matches overlap.

As the requirements develop, the program will also need to handle different letter cases, wildcard characters and multiple search patterns.

## Step 1: Basic Pattern Searching

Create a function that takes a string and a search pattern, then returns a list containing the starting index of every occurrence.

```python
def find_matches(text: str, pattern: str) -> list[int]:
    pass
```

**Requirements:**

- Search the text from left to right.
- Return the starting index of each match in ascending order.
- Include overlapping matches.
- Treat uppercase and lowercase letters as different characters.
- Treat spaces and punctuation as normal characters.
- Return an empty list if no matches exist.
- Return an empty list if either input is empty.
- Do not modify the original strings.

**Examples:**

```python
find_matches("hello", "ll")
# [2]

find_matches("banana", "ana")
# [1, 3]

find_matches("aaaa", "aa")
# [0, 1, 2]

find_matches("hello hello", "lo")
# [3, 9]

find_matches("python", "java")
# []

find_matches("abc", "abcdef")
# []

find_matches("", "ab")
# []

find_matches("hello", "")
# []
```

## Step 2: Case-Insensitive Searching

The company now wants users to search without worrying about uppercase and lowercase letters.

Extend your function by introducing an optional parameter called `ignore_case`.

```python
def find_matches(
    text: str,
    pattern: str,
    ignore_case: bool = False
) -> list[int]:
    pass
```

**Requirements:**

- When `ignore_case=True`, treat uppercase and lowercase letters as equivalent.
- When `ignore_case=False`, preserve Step 1's case-sensitive behaviour.
- Return indexes relative to the original text.
- Continue supporting overlapping matches.
- Do not modify the original strings.
- Assume standard English letters, digits, spaces and punctuation.

**Examples:**

```python
find_matches("Hello HELLO hello", "hello", ignore_case=True)
# [0, 6, 12]

find_matches("BaNaNa", "ana", ignore_case=True)
# [1, 3]

find_matches("BaNaNa", "ana")
# []

find_matches("abcABC", "AbC", ignore_case=True)
# [0, 3]

find_matches("abcABC", "AbC")
# []

find_matches("Python PYTHON", "python", ignore_case=True)
# [0, 7]
```

## Step 3: Wildcard Pattern Matching

The company now wants to introduce wildcard searching.

A question mark (`?`) should represent **exactly one character**.

For example, searching for `"c?t"` in `"cat cut cot"` should match all three words because the wildcard can represent `a`, `u` or `o`.

**Requirements:**

- Treat `?` in the pattern as a wildcard matching exactly one character.
- Support multiple wildcards within a single pattern.
- Wildcards may match letters, numbers, spaces or punctuation.
- All other characters must match normally.
- The matching sequence must have the same length as the pattern.
- Continue supporting overlapping matches and case-insensitive searching.
- Return an empty list if no matches exist or the pattern is empty.
- Treat every `?` in the pattern as a wildcard, not a literal question mark.

**Examples:**

```python
find_matches("cat cut cot", "c?t")
# [0, 4, 8]

find_matches("abc axc a c", "a?c")
# [0, 4, 8]

find_matches("aaaa", "a?")
# [0, 1, 2]

find_matches("abc", "??")
# [0, 1]

find_matches("abc", "????")
# []

find_matches("Cat cOt", "c?t", ignore_case=True)
# [0, 4]

find_matches("hello", "h?ll?")
# [0]

find_matches("hello", "h?z")
# []
```

## Step 4: Searching for Multiple Patterns

The company now wants users to search for several patterns at the same time.

Create a second function called `find_multiple`.

```python
def find_multiple(
    text: str,
    patterns: list[str],
    ignore_case: bool = False
) -> dict[str, list[int]]:
    pass
```

The function should return a dictionary where each key represents a search pattern and each value contains the indexes where it appears.

**Requirements:**

- Search for every pattern independently.
- Return a dictionary mapping each original pattern to its matching indexes.
- Include patterns with no matches, using an empty list.
- Support overlapping matches, wildcards and case-insensitive searching.
- Preserve each pattern's original spelling as its dictionary key.
- Return an empty dictionary if the pattern list is empty.
- If the text is empty, return an empty list for each pattern.
- Assume all patterns are unique and non-empty.
- Do not modify the original inputs.

You may reuse your `find_matches` function.

**Examples:**

```python
find_multiple("banana", ["ana", "na", "b?n"])
# {
#     "ana": [1, 3],
#     "na": [2, 4],
#     "b?n": [0]
# }

find_multiple("hello world", ["hello", "world", "python"])
# {
#     "hello": [0],
#     "world": [6],
#     "python": []
# }

find_multiple("aaaa", ["aa", "a?", "bb"])
# {
#     "aa": [0, 1, 2],
#     "a?": [0, 1, 2],
#     "bb": []
# }

find_multiple("Cat cut cot", ["c?t", "at"], ignore_case=True)
# {
#     "c?t": [0, 4, 8],
#     "at": [1]
# }

find_multiple("abc", [])
# {}

find_multiple("", ["ab", "a?"])
# {
#     "ab": [],
#     "a?": []
# }
```

Refer to the main **Coding Problems README** for testing requirements and technical assessment preparation guidance.