# Balanced Brackets

You've been tasked with writing the bracket checker for a new code editor, _Bracewell Studio_.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Is It Balanced?

Write `is_balanced(s)` that returns `True` if every bracket in the string is correctly opened and closed, otherwise `False`.

Brackets are `()`, `[]` and `{}`. All other characters should be ignored.

**Examples:**
```python
is_balanced("{[()]}")      # True
is_balanced("a(b)c[d]")    # True
is_balanced("([)]")        # False
is_balanced("((")          # False
is_balanced("")            # True
```

## Step 2: Find the Error

Write `find_error(s)` that returns the **index** of the first problem, or `-1` if the string is balanced.

- A closing bracket with nothing to match (or the wrong match) is a problem at **its own index**.
- If the string ends with unclosed opening brackets, return the index of the **earliest** one that was never closed.

**Examples:**
```python
find_error("()")       # -1
find_error("([)]")     # 2   (the ")" doesn't match the "[")
find_error("())")      # 2
find_error("(()")      # 0   (the first "(" is never closed)
find_error("{[}")      # 2
```

## Step 3: Strings and Custom Pairs

1. Brackets inside double-quoted strings should be ignored.
2. `is_balanced` should accept an optional `pairs` dictionary mapping openers to closers. The default is `{"(": ")", "[": "]", "{": "}"}`.

**Examples:**
```python
is_balanced('print("(")')   # True  (the "(" is inside a string)
is_balanced('("(")')        # True

is_balanced("<a[b]>", pairs={"(": ")", "[": "]", "<": ">"})   # True
is_balanced("<a[b>]", pairs={"(": ")", "[": "]", "<": ">"})   # False
```

## 💡 Hints

1. A stack (a plain Python list with `append` and `pop`) is the natural tool here.
2. Push every opener. When you see a closer, the top of the stack must be its matching opener.
3. Don't forget to check the stack is empty at the end (that catches `"(("`).
4. For `find_error`, store the **index** on the stack as well as the character, e.g. `(char, index)`.
5. For quoted strings, keep an `in_string` flag that flips each time you see a `"`.
