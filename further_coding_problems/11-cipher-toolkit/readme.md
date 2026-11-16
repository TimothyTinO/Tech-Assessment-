# Cipher Toolkit

You're writing the encryption helpers for _Spyglass Games_, an escape-room company that hides clues in secret messages.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Caesar Cipher

Write `caesar(text, shift)` that shifts every letter by `shift` places through the alphabet, wrapping around.

- Keep upper and lower case as they are.
- Leave anything that isn't a letter unchanged.
- Negative shifts and shifts larger than 26 must work.

**Examples:**
```python
caesar("Hello, World!", 3)    # "Khoor, Zruog!"
caesar("abc", -1)             # "zab"
caesar("xyz", 29)             # "abc"
caesar("123 !?", 5)           # "123 !?"
```

## Step 2: Vigenère Cipher

Write `vigenere(text, key, decrypt=False)`. Each letter is shifted by the matching letter of the key (`A` = 0, `B` = 1, ...), and the key repeats.

- The key only advances on **letters** in the text. Spaces and punctuation are skipped without using up a key letter.
- Preserve the case of the text. The key is case-insensitive.
- Raise `ValueError` if the key is empty or contains non-letters.

**Examples:**
```python
vigenere("ATTACKATDAWN", "LEMON")
# Returns: "LXFOPVEFRNHR"

vigenere("Attack at dawn!", "lemon")
# Returns: "Lxfopv ef rnhr!"

vigenere("LXFOPVEFRNHR", "LEMON", decrypt=True)
# Returns: "ATTACKATDAWN"

vigenere("hello", "")
# Raises ValueError
```

## Step 3: Crack It

You've intercepted a Caesar-encrypted message and you know one word that's in it.

Write `find_shift(ciphertext, known_word)` that tries every shift from `1` to `25` and returns the shift that was used to encrypt the message. A shift is correct if decrypting with it gives a message containing `known_word` (ignore case).

Return `None` if no shift works.

**Examples:**
```python
find_shift("Khoor, Zruog!", "world")    # 3
find_shift("Khoor, Zruog!", "HELLO")    # 3
find_shift("Khoor, Zruog!", "banana")   # None
```

## 💡 Hints

1. For Caesar, use `ord()` and `chr()` to convert between letters and numbers, and `% 26` to wrap around.
2. Handle uppercase and lowercase separately: the starting point is `ord("A")` for capitals and `ord("a")` for lowercase.
3. Vigenère is just Caesar with a different shift per letter. You can reuse your `caesar` function by passing each letter and its shift.
4. Keep a separate counter for the key position and only increase it when you process a letter.
5. To decrypt, use the negative of the shift.
6. For Step 3, loop `for shift in range(1, 26)`, decrypt with `caesar(ciphertext, -shift)`, and check if the known word is in the lowercase result.
