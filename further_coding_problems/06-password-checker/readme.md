# Password Checker

You're writing the sign-up validation for _SafeNest_, a home security app. Weak passwords get rejected, and users get told exactly what's wrong.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Is It Valid?

Write `is_valid_password(password)` that returns `True` only if the password:

- is at least 8 characters long
- has at least one uppercase letter
- has at least one lowercase letter
- has at least one digit

**Examples:**
```python
is_valid_password("Passw0rdX")      # True
is_valid_password("password")       # False  (no uppercase, no digit)
is_valid_password("SHORT1a")        # False  (only 7 characters)
is_valid_password("NoDigitsHere")   # False
```

## Step 2: What's Wrong?

Write `check_password(password)` that returns a list of **every** rule that failed, as these exact messages, always in this order:

1. `"too short"`
2. `"no uppercase"`
3. `"no lowercase"`
4. `"no digit"`
5. `"contains space"`

Step 5 is a new rule: a password containing a space is a failure. Return an empty list if everything passes.

**Examples:**
```python
check_password("Passw0rdX")
# Returns: []

check_password("abc")
# Returns: ["too short", "no uppercase", "no digit"]

check_password("pass word")
# Returns: ["no uppercase", "no digit", "contains space"]
```

## Step 3: How Strong?

Write `strength(password)` that returns `"weak"`, `"medium"` or `"strong"`.

Score one point for each of these:

- 8 or more characters
- 12 or more characters
- has an uppercase letter
- has a lowercase letter
- has a digit
- has a symbol (any character that isn't a letter, digit or space)

Scores of 0-2 are `"weak"`, 3-4 are `"medium"`, 5-6 are `"strong"`.

**Exception:** if the password is one of `"password"`, `"123456"`, `"qwerty"` or `"letmein"` (in any upper/lower case), it is always `"weak"`, whatever its score.

**Examples:**
```python
strength("abc")                  # "weak"
strength("Passw0rdX")            # "medium"
strength("Tr1cky&Long!Pass")     # "strong"
strength("Password")             # "weak"  (common password)
strength("QWERTY")               # "weak"
```

## 💡 Hints

1. `any(c.isupper() for c in password)` checks if at least one character is uppercase. `isupper`, `islower` and `isdigit` are built-in string methods.
2. Write the individual checks once, as small helper functions, and reuse them in all three steps.
3. For `check_password`, start with an empty list and `append` a message each time a rule fails.
4. `c.isalnum()` is true for letters and digits. A symbol is a character where that is false and `c != " "`.
5. For the common password exception, compare `password.lower()` against a list of common passwords. Do this check first.
