# Run-Length Encoding

You're writing a tiny compression tool for _Pixel Pete's Sprite Shop_. Sprites contain long runs of the same character, so run-length encoding is perfect.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Encode and Decode

Write two functions:

- `encode(s)` replaces each run of identical characters with the count followed by the character.
- `decode(s)` reverses it.

**Examples:**
```python
encode("AAAABBBCCD")    # "4A3B2C1D"
decode("4A3B2C1D")      # "AAAABBBCCD"
encode("")              # ""
decode("")              # ""
```

## Step 2: Long Runs and Bad Input

1. Counts can have more than one digit.
2. `encode` should return `None` if the input contains any digit (it would make decoding ambiguous).
3. `decode` should return `None` if the input is malformed: a count with no character after it, a character with no count, or a count of `0`.

**Examples:**
```python
encode("A" * 12 + "B")   # "12A1B"
decode("12A1B")          # "AAAAAAAAAAAAB"
encode("AB3")            # None

decode("4")              # None  (count with no character)
decode("A4")             # None  (character with no count)
decode("0A")             # None  (zero count)
```

## Step 3: Compact Mode

Add `compact=False` to `encode`. When `compact=True`, runs of length 1 omit the count.

`decode` should understand **both** styles automatically (a letter with no count means a run of 1).

**Examples:**
```python
encode("AAAABBBCCD", compact=True)   # "4A3B2CD"
decode("4A3B2CD")                    # "AAAABBBCCD"
decode("ABC")                        # "ABC"
decode("4A3B2C1D")                   # "AAAABBBCCD"
```

> Careful: once compact mode is allowed, Step 2's rule "a character with no count is malformed" no longer applies, so update your tests too!

## 💡 Hints

1. Walk through the string keeping track of the current character and a running count. When the character changes, write out the previous run.
2. Don't forget to flush the final run after the loop ends.
3. For `decode`, collect digits into a string until you hit a non-digit, then `int()` that string.
4. `itertools.groupby` is a handy shortcut for encoding, but try it by hand first.
