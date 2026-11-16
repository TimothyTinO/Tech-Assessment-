# Python Strings Cheatsheet

## Creating Strings

```python
s1 = 'single quotes'
s2 = "double quotes"
s3 = '''triple quotes
span multiple
lines'''
s4 = """also triple
double quotes"""
s5 = str(123)              # '123'
s6 = "abc" * 3             # 'abcabcabc'
s7 = "a" "b" "c"           # 'abc' (implicit concatenation)
```

## Escape Characters

| Escape | Meaning |
|--------|---------|
| `\n` | Newline |
| `\t` | Tab |
| `\\` | Backslash |
| `\'` | Single quote |
| `\"` | Double quote |
| `\r` | Carriage return |
| `\b` | Backspace |
| `\0` | Null character |
| `\xhh` | Hex character (e.g. `\x41` = 'A') |
| `\ooo` | Octal character |
| `\N{name}` | Unicode name (e.g. `\N{BULLET}`) |

```python
print(r"C:\new\test")      # raw string: C:\new\test
```

## Indexing & Slicing

```python
s = "Python"
#    012345
#   -6-5-4-3-2-1

s[0]        # 'P'
s[-1]       # 'n'
s[1:4]      # 'yth'
s[:3]       # 'Pyt'
s[3:]       # 'hon'
s[:]        # 'Python'
s[::2]      # 'Pto'
s[::-1]     # 'nohtyP' (reverse)
s[1:-1]     # 'ytho'
```

## Common Methods

### Case
```python
s = "Hello World"
s.upper()           # 'HELLO WORLD'
s.lower()           # 'hello world'
s.title()           # 'Hello World'
s.capitalize()      # 'Hello world'
s.swapcase()        # 'hELLO wORLD'
s.casefold()        # 'hello world' (aggressive lowercase)
```

### Search & Check
```python
s = "Hello World"
s.find("o")         # 4  (first index or -1)
s.rfind("o")        # 7  (last index or -1)
s.index("o")        # 4  (raises ValueError if missing)
s.rindex("o")       # 7
s.count("l")        # 3
s.startswith("He")  # True
s.endswith("ld")    # True
"ell" in s          # True
```

### Strip / Trim
```python
s = "  hello  "
s.strip()           # 'hello'
s.lstrip()          # 'hello  '
s.rstrip()          # '  hello'
"xxhixx".strip("x") # 'hi'
```

### Replace
```python
"hello".replace("l", "L")        # 'heLLo'
"hello".replace("l", "L", 1)     # 'heLlo'
```

### Split & Join
```python
"a,b,c".split(",")         # ['a', 'b', 'c']
"a b  c".split()           # ['a', 'b', 'c']  (any whitespace)
"a,b,c".split(",", 1)      # ['a', 'b,c']
"a\nb\r\nc".splitlines()   # ['a', 'b', 'c']

",".join(["a", "b", "c"])  # 'a,b,c'
"".join(["a", "b"])        # 'ab'
```

### Alignment / Padding
```python
"hi".center(10)        # '    hi    '
"hi".center(10, "-")   # '----hi----'
"hi".ljust(10)         # 'hi        '
"hi".rjust(10, ".")    # '........hi'
"42".zfill(5)          # '00042'
```

### Character Checks
```python
"abc".isalpha()      # True  (letters only)
"123".isdigit()      # True  (digits only)
"123".isnumeric()    # True
"abc123".isalnum()   # True  (letters or digits)
"   ".isspace()      # True
"Hello".isupper()    # False
"HELLO".isupper()    # True
"hello".islower()    # True
"Hello World".istitle()   # True
"abc".isascii()      # True
"abc123".isidentifier()   # True (valid identifier)
```

### Encoding
```python
"hello".encode()              # b'hello'
"h\u00e9llo".encode("utf-8")  # b'h\xc3\xa9llo'
b"hello".decode("utf-8")      # 'hello'
```

## String Formatting

### f-strings (preferred, Python 3.6+)
```python
name, age = "Alice", 30
f"{name} is {age}"                 # 'Alice is 30'
f"{age:.2f}"                       # '30.00'
f"{3.14159:.3f}"                   # '3.142'
f"{1234567:,}"                     # '1,234,567'
f"{0.25:.1%}"                      # '25.0%'
f"{42:08b}"                        # '00101010' (binary)
f"{255:#x}"                        # '0xff'
f"{name!r}"                        # "'Alice'" (repr)
f"{name:>10}"                      # '     Alice'
f"{name:*^10}"                     # '**Alice***'
f"{age=}"                          # 'age=30' (debug, 3.8+)
```

### `format()` method
```python
"{} is {}".format("Alice", 30)
"{1} is {0}".format(30, "Alice")
"{name} is {age}".format(name="Alice", age=30)
"{:.2f}".format(3.14159)           # '3.14'
```

### `%` formatting (legacy)
```python
"%s is %d" % ("Alice", 30)
"%.2f" % 3.14159                   # '3.14'
"%05d" % 42                        # '00042'
```

## Common Operations

### Concatenation & Repetition
```python
"a" + "b"          # 'ab'
"ab" * 3           # 'ababab'
```

### Membership
```python
"ell" in "hello"       # True
"xyz" not in "hello"   # True
```

### Comparison
```python
"abc" == "abc"     # True
"abc" < "abd"      # True  (lexicographic)
"Z" < "a"          # True  (ASCII order)
```

### Iteration
```python
for ch in "abc":
    print(ch)

chars = list("abc")        # ['a', 'b', 'c']
```

### Length
```python
len("hello")    # 5
```

## Useful Built-ins

```python
ascii("héllo")              # "'h\\xe9llo'"
repr("hello\n")             # "'hello\\n'"
ord("A")                    # 65
chr(65)                     # 'A'
max("hello")                # 'o' (by char code)
min("hello")                # 'e'
sorted("cba")               # ['a', 'b', 'c']
```

## Type Conversion

```python
str(42)          # '42'
str(3.14)        # '3.14'
str(True)        # 'True'
str([1, 2])      # '[1, 2]'
int("42")        # 42
float("3.14")    # 3.14
list("abc")      # ['a', 'b', 'c']
tuple("abc")     # ('a', 'b', 'c')
```

## Common Gotchas

```python
# Strings are immutable
s = "hello"
# s[0] = "H"           # TypeError

# Need to rebuild instead
s = "H" + s[1:]        # 'Hello'

# Multiplication with 0 gives empty string
"abc" * 0              # ''

# int() strips surrounding whitespace
int("  42  ")          # 42
int("42a")             # ValueError
```

## Ternary / Conditional

```python
"big" if len(s) > 5 else "small"
```

## Common Recipes

```python
# Reverse a string
s[::-1]

# Check palindrome
s == s[::-1]

# Count occurrences
"hello".count("l")             # 2

# Remove all whitespace
"".join(s.split())

# Title-case words
"hello world".title()          # 'Hello World'

# Capitalize first letter
s[0].upper() + s[1:] if s else s

# Split into words
"a b c".split()

# Join list to string
" ".join(["a", "b", "c"])

# Format with thousands separator
f"{1234567:,}"                 # '1,234,567'

# Check if string is empty
not s                          # True if s == ""
```