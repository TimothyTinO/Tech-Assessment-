# Anagram Groups

You're building a word-puzzle helper for _Lexi's Games_. Players submit lists of words and the app needs to figure out which words are anagrams of each other.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Group the Anagrams

Write `group_anagrams(words)` that takes a list of lowercase words and returns a list of groups, where each group contains words that are anagrams of each other.

- Words inside each group are sorted alphabetically.
- Groups are sorted alphabetically by their first word.

**Examples:**
```python
group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"])
# Returns:
# [["ate", "eat", "tea"], ["bat"], ["nat", "tan"]]

group_anagrams([])
# Returns: []
```

## Step 2: Ignore Case and Spaces

Make the grouping case-insensitive and ignore spaces, but **return the words exactly as they were given**. Sorting (inside groups and between groups) should also be case-insensitive.

**Examples:**
```python
group_anagrams(["Listen", "Silent", "enlist", "google", "gogole"])
# Returns:
# [["enlist", "Listen", "Silent"], ["gogole", "google"]]

group_anagrams(["Dormitory", "dirty room"])
# Returns:
# [["dirty room", "Dormitory"]]
```

## Step 3: Minimum Group Size

Add an optional `min_size` argument (default `1`). Only return groups that contain at least `min_size` words.

**Examples:**
```python
group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"], min_size=2)
# Returns:
# [["ate", "eat", "tea"], ["nat", "tan"]]

group_anagrams(["eat", "bat"], min_size=3)
# Returns: []
```

## 💡 Hints

1. Two words are anagrams if their letters, once sorted, are identical. That sorted string makes a great dictionary key.
2. A `dict` that maps `key -> list of words` (or `collections.defaultdict(list)`) does most of the work.
3. For Step 2, build the key from the lowercase word with spaces removed, but store the original word in the group.
4. `sorted(..., key=str.lower)` lets you sort case-insensitively without changing the words.
