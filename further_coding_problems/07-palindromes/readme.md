# Palindromes

You're building a word-game feature for _Mirror Mirror Games_. Players score points for finding words and phrases that read the same forwards and backwards.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Is It a Palindrome?

Write `is_palindrome(text)` that returns `True` if the text reads the same forwards and backwards.

Ignore upper/lower case, spaces and punctuation. Only letters and digits count.

**Examples:**
```python
is_palindrome("racecar")                          # True
is_palindrome("A man, a plan, a canal: Panama")   # True
is_palindrome("race a car")                       # False
is_palindrome("")                                 # True
```

## Step 2: Find Palindrome Words

Write `palindromic_words(sentence)` that returns a list of the words in the sentence that are palindromes, in the order they appear.

- Words are lowercased in the result.
- Punctuation is not part of a word.
- Single-letter words don't count.

**Examples:**
```python
palindromic_words("Anna saw a kayak at noon")
# Returns: ["anna", "kayak", "noon"]

palindromic_words("Wow! Did Bob see Eve?")
# Returns: ["wow", "did", "bob", "eve"]

palindromic_words("Nothing here")
# Returns: []
```

## Step 3: Longest Palindrome Inside a String

Write `longest_palindromic_substring(s)` that returns the longest palindromic piece inside `s`. A piece is a run of consecutive characters. Here case and punctuation **do** matter.

If there's a tie, return the one that appears first. Return `""` for an empty string.

**Examples:**
```python
longest_palindromic_substring("babad")   # "bab"
longest_palindromic_substring("cbbd")    # "bb"
longest_palindromic_substring("a")       # "a"
longest_palindromic_substring("")        # ""
```

## 💡 Hints

1. Build a "cleaned" version of the text that only has lowercase letters and digits, then compare it with itself reversed. `text[::-1]` reverses a string.
2. `str.isalnum()` tells you if a character is a letter or digit.
3. For Step 2, split the sentence into words, clean each word, then reuse `is_palindrome`.
4. For Step 3, a simple approach works fine: try every start and end position, check each piece with your palindrome test, and keep the longest. Check longer pieces only if you want to be smarter.
