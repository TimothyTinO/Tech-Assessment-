# Challenge 5: Text Pattern Finder

Create a program that searches through text and identifies the positions where a particular sequence of characters appears. Build your solution step by step, starting with basic string searching before introducing case-insensitive matching, wildcards and multiple search patterns.

REMINDER: The examples provided are only a starting point. You should be writing your own tests to ensure your code works as expected!

## ⚠️ Note

There is *likely* too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Background

Searching for patterns within text is a common task in software development.

Search engines, text editors, document-processing applications and data-analysis tools all need to identify particular words or sequences of characters.

Imagine you are working for a company developing a simple text-searching application.

The application allows users to search through sentences and identify where specific patterns appear.

For example, consider the following string:

```python
"banana"
```

A user wants to search for the pattern:

```python
"ana"
```

The pattern appears twice in the original string.

The first occurrence starts at index `1`, while the second occurrence starts at index `3`.

The application should therefore return:

```python
[1, 3]
```

Notice that the two matches overlap.

As the requirements become more complicated, your program will need to handle uppercase and lowercase letters, special wildcard characters and multiple search patterns.

Your task is to develop these features progressively.

---

## Step 1: Basic Pattern Searching

Create a function called `find_matches` that takes two strings:

1. `text`: The original string that will be searched.
2. `pattern`: The sequence of characters you want to find.

The function should return a list containing the starting index of every occurrence of the pattern.

Start with the following function:

```python
def find_matches(text: str, pattern: str) -> list[int]:
    pass
```

For this first step, you can assume:

- Both inputs are strings.
- Matching is case-sensitive.
- The pattern may contain more than one character.
- Both strings may be empty.
- Characters such as spaces and punctuation are treated normally.

**Requirements:**

- Search the text from left to right.
- Identify every occurrence of the given pattern.
- Return the starting index of each match.
- Store the indexes in a list in ascending order.
- Include overlapping matches.
- Return an empty list if the pattern does not appear.
- Return an empty list if either `text` or `pattern` is empty.
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

### Understanding Overlapping Matches

Consider:

```python
"aaaa"
```

Searching for `"aa"` produces three matches:

- The first match starts at index `0`.
- The second match starts at index `1`.
- The third match starts at index `2`.

Even though the matches share characters, they must all be included.

Your function should not skip indexes simply because a previous match has already been found.

**Things to consider:**

- How can you access an individual character using its index?
- How can you examine multiple consecutive characters?
- How can you determine where a match starts?
- How can you avoid searching beyond the end of the string?
- How will your function handle patterns longer than the text?
- How can you ensure overlapping patterns are not missed?

Make sure your solution works with the examples above before moving on.

---

## Step 2: Case-Insensitive Searching

The company has noticed that users sometimes search for words using different combinations of uppercase and lowercase letters.

For example, consider:

```python
"Hello HELLO hello"
```

A user searching for `"hello"` may expect to find all three occurrences, regardless of how the letters are capitalised.

However, the current function performs case-sensitive comparisons.

Extend your function by introducing an optional parameter called `ignore_case`.

```python
def find_matches(
    text: str,
    pattern: str,
    ignore_case: bool = False
) -> list[int]:
    pass
```

When `ignore_case` is `True`, uppercase and lowercase letters should be treated as equivalent.

When `ignore_case` is `False`, the function should behave exactly as it did in Step 1.

For this challenge, assume the strings contain standard English letters, spaces, digits and punctuation.

**Requirements:**

- Support case-insensitive searching when `ignore_case=True`.
- Continue supporting case-sensitive searching by default.
- Return positions relative to the original text.
- Preserve overlapping matches.
- Do not modify the input strings.
- Continue handling empty inputs and missing patterns.

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

find_matches("", "hello", ignore_case=True)
# []
```

**Things to consider:**

- Which Python string methods can help with case-insensitive comparisons?
- Should you convert the original text or create a new version?
- How can you preserve the correct indexes?
- How will the function behave when the optional parameter is not provided?
- Can you reuse your solution from Step 1?

Your function should continue to satisfy the original searching requirements.

---

## Step 3: Wildcard Pattern Matching

The company now wants to introduce a more flexible searching feature.

Users should be able to search for patterns even when they do not know every character.

To achieve this, the application will introduce a special wildcard character:

```text
?
```

A wildcard represents **exactly one character**.

It can match any single character, including letters, numbers, spaces or punctuation.

For example, consider the following text:

```python
"cat cut cot"
```

A user searches for:

```python
"c?t"
```

The pattern should match:

- `"cat"`
- `"cut"`
- `"cot"`

This is because the `?` can represent `a`, `u` or `o`.

The resulting indexes should be:

```python
[0, 4, 8]
```

Extend your existing `find_matches` function to support this behaviour.

**Requirements:**

- A question mark (`?`) in the pattern matches exactly one character.
- All other pattern characters must match normally.
- Multiple wildcards may appear in a single pattern.
- Wildcards can match spaces and punctuation.
- A wildcard cannot match zero characters or multiple characters.
- The pattern and matched text must have the same length.
- Continue supporting overlapping matches.
- Continue supporting the `ignore_case` parameter.
- Return an empty list if no matches exist.
- Continue returning an empty list when the pattern is empty.

For this step, treat every `?` in the pattern as a wildcard. You do not need to implement a way to search for a literal question mark.

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

find_matches("", "?")
# []
```

### Understanding Multiple Wildcards

Consider the following pattern:

```python
"a??d"
```

This pattern contains four positions:

- The first character must be `a`.
- The second character can be anything.
- The third character can be anything.
- The fourth character must be `d`.

Therefore, the pattern could match `"abcd"`, `"a12d"` or `"a  d"`.

It would not match `"abd"`, because that string contains only three characters.

**Things to consider:**

- How can you compare two strings character by character?
- How can you determine whether a character is a wildcard?
- How would you track whether an entire pattern matches?
- What should happen if one character does not match?
- Why might nested loops be useful for this problem?
- How can you ensure the outer search continues even when a particular comparison fails?

Your solution should now support ordinary character matching and wildcard matching.

---

## Step 4: Searching for Multiple Patterns

The company now wants users to search for several patterns at the same time.

Instead of searching for just one pattern, the application should accept a list of patterns and return the positions where each pattern appears.

Create a second function called `find_multiple`.

```python
def find_multiple(
    text: str,
    patterns: list[str],
    ignore_case: bool = False
) -> dict[str, list[int]]:
    pass
```

The function should return a dictionary where:

- Each key is one of the original search patterns.
- Each value is a list containing all starting indexes where that pattern appears.

For example:

```python
text = "banana"
patterns = ["ana", "na", "b?n"]
```

The expected result is:

```python
{
    "ana": [1, 3],
    "na": [2, 4],
    "b?n": [0]
}
```

Notice that:

- `"ana"` appears at indexes `1` and `3`.
- `"na"` appears at indexes `2` and `4`.
- `"b?n"` matches `"ban"` beginning at index `0`.

The company wants the function to support all the searching functionality introduced in the previous steps.

**Requirements:**

- Accept a list containing multiple search patterns.
- Search for every pattern independently.
- Return a dictionary containing the results for each pattern.
- Preserve each pattern's original spelling when using it as a dictionary key.
- Include patterns that produce no matches, using an empty list as their value.
- Support overlapping matches.
- Support the wildcard character introduced in Step 3.
- Support case-insensitive searching when `ignore_case=True`.
- Return an empty dictionary if the pattern list is empty.
- If the text is empty, return each pattern with an empty list.
- Do not modify the original text or pattern list.

You may assume all patterns in the list are unique and non-empty.

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

find_multiple(
    "Cat cut cot",
    ["c?t", "at"],
    ignore_case=True
)
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

**Things to consider:**

- How can you iterate through a list of patterns?
- Which data structure is appropriate for associating patterns with their matching positions?
- How can you reuse your previous function rather than repeating the searching logic?
- Why should patterns with no matches still appear in the dictionary?
- How can you preserve the original pattern names when searching without considering letter case?
- How can you keep the code readable as the number of requirements increases?

---

## Testing

You should write your own automated tests using `pytest`.

The provided examples demonstrate the expected behaviour, but they are not exhaustive.

You are responsible for identifying and testing cases that might cause your implementation to fail.

When planning your tests, consider the following areas:

- Finding single-character and multi-character patterns.
- Searching when a pattern occurs more than once.
- Handling overlapping matches.
- Searching for patterns that do not exist.
- Handling empty inputs.
- Patterns longer than the original text.
- Case-sensitive and case-insensitive searching.
- Wildcards appearing at different positions.
- Multiple wildcards within the same pattern.
- Searching for multiple patterns.
- Handling patterns that produce no matches.
- Ensuring input strings and lists remain unchanged.

You should also consider whether each new step affects functionality introduced in the earlier steps.

Run your tests using:

```bash
pytest -v
```

Remember that passing the examples provided does not guarantee that your solution is correct for every valid input.

## Technical Assessment Practice

Before writing code, practise explaining how you would approach the problem.

You should be prepared to answer the following questions:

1. What are the inputs and outputs of each function?
2. How can you use indexes to search through a string?
3. What is the difference between indexing and slicing?
4. How can you determine how many possible starting positions exist for a pattern?
5. Why do overlapping matches require special consideration?
6. How can you compare strings without considering letter case?
7. How would you implement wildcard matching?
8. When might nested loops be appropriate?
9. How can dictionaries help organise multiple search results?
10. How can you reuse existing functions as requirements become more complicated?
11. What edge cases might cause indexing errors?
12. How would you explain your approach to someone unfamiliar with Python?

**Start with Step 1.** Focus on implementing basic pattern searching and writing your own tests before introducing case-insensitive searching, wildcards and multiple patterns.

You should be able to explain your reasoning and identify potential edge cases before moving on to the next step.