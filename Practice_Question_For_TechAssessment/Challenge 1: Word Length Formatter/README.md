# Challenge 1: Word Length Formatter

Create a program that analyses a sentence and returns the length of each word. Build your solution step by step, starting with basic string manipulation before introducing more complicated requirements.

REMINDER: The tests provided are a minimal base. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is *likely* too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Background

Text processing is a common task in software development. Many applications need to analyse written text, whether that involves checking user input, searching through documents or calculating statistics about words.

Imagine you are working for a company that develops a tool to analyse the complexity of written sentences.

The company wants to understand how long individual words are, as word length can help indicate how complex a piece of writing might be.

For example, consider the sentence:

`"python is fun"`

It contains three words:

- `python` contains 6 characters.
- `is` contains 2 characters.
- `fun` contains 3 characters.

The program should therefore return:

```python
[6, 2, 3]
```

Your task is to build a function that can perform this operation on different sentences.

As you progress through the challenge, you will extend your solution to support additional requirements, including handling whitespace, ignoring punctuation and filtering words based on their lengths.

## Step 1: Basic Word Lengths

Your task is to create a function called `word_lengths` that takes a string as input and returns a list containing the length of each word.

Start with the following function:

```python
def word_lengths(sentence: str) -> list[int]:
    pass
```

For this first step, you can assume:

- The sentence contains words separated by exactly one space.
- There are no spaces at the beginning or end.
- Words contain letters only.
- The input string may be empty.

**Requirements:**

- Count the number of characters in each word.
- Store each word's length in a list.
- Preserve the original order of the words.
- Return an empty list if the sentence is empty.

**Examples:**

```python
word_lengths("hello")
# [5]

word_lengths("hello world")
# [5, 5]

word_lengths("python is fun")
# [6, 2, 3]

word_lengths("a bb ccc dddd")
# [1, 2, 3, 4]

word_lengths("")
# []
```

**Things to consider:**

- How can you separate a sentence into individual words?
- How can you find the length of a string?
- How can you store multiple values in a list?
- How would your function handle an empty string?

Make sure your solution works with the examples above before moving on.

## Step 2: Handling Multiple Spaces

Your company has noticed that users sometimes include additional spaces when entering sentences.

Your current solution may not correctly handle these cases.

Extend your function so that it can process sentences containing multiple spaces, including spaces at the beginning and end.

**Requirements:**

- Ignore leading and trailing spaces.
- Ignore additional spaces between words.
- Do not treat spaces as individual words.
- Do not include zero-length words in the output.
- Return an empty list if the sentence contains only spaces.

**Examples:**

```python
word_lengths("hello   world")
# [5, 5]

word_lengths("  python is fun  ")
# [6, 2, 3]

word_lengths("a    bb   ccc")
# [1, 2, 3]

word_lengths("   hello")
# [5]

word_lengths("world   ")
# [5]

word_lengths("     ")
# []
```

**Things to consider:**

- What happens when a sentence contains consecutive spaces?
- How does `split()` behave when no separator is provided?
- What is the difference between `split()` and `split(" ")`?
- How can you ensure that empty words are not included?

Your function should continue to work with all the examples from Step 1.

## Step 3: Ignoring Punctuation

The company now wants to analyse sentences containing punctuation.

Currently, punctuation might be counted as part of a word, which could produce incorrect results.

For example, the word `"hello!"` contains six characters, but the actual word `"hello"` contains only five letters.

Extend your solution so that it ignores the following punctuation characters:

```text
. , ! ?
```

**Requirements:**

- Ignore full stops, commas, exclamation marks and question marks.
- Punctuation should not contribute to a word's length.
- Punctuation may appear at the beginning, middle or end of a word.
- If a word contains only punctuation, ignore that word.
- All other characters should still count normally.
- Continue handling multiple spaces as described in Step 2.

**Examples:**

```python
word_lengths("hello, world!")
# [5, 5]

word_lengths("python is fun!")
# [6, 2, 3]

word_lengths("Wait... what?!")
# [4, 4]

word_lengths("Hello!!! How are you?")
# [5, 3, 3, 3]

word_lengths("hello...   world!!!")
# [5, 5]

word_lengths("...")
# []

word_lengths("hello ... world")
# [5, 5]

word_lengths("")
# []
```

**Things to consider:**

- Which Python string methods allow you to remove characters?
- How would you handle multiple punctuation marks together?
- What happens if a word consists entirely of punctuation?
- Should punctuation be removed before or after measuring a word's length?

Your solution should still satisfy the requirements from Steps 1 and 2.

## Step 4: Filtering Words by Length

The company would now like to filter out words that are shorter than a specified minimum length.

For example, given the sentence:

`"python is fun"`

If the minimum length is `3`, the word `"is"` should be excluded because it contains only two characters.

The expected output would be:

```python
[6, 3]
```

Extend your function by adding an optional parameter called `min_length`.

```python
def word_lengths(sentence: str, min_length: int = 0) -> list[int]:
    pass
```

**Requirements:**

- Only return word lengths that are greater than or equal to `min_length`.
- Continue ignoring additional spaces and punctuation.
- If no words meet the minimum length, return an empty list.
- If `min_length` is not provided, the function should behave as it did in Step 3.
- Assume `min_length` is a non-negative integer.

**Examples:**

```python
word_lengths("python is fun", min_length=3)
# [6, 3]

word_lengths("hello world", min_length=5)
# [5, 5]

word_lengths("a bb ccc dddd", min_length=3)
# [3, 4]

word_lengths("hello, wonderful world!", min_length=6)
# [9]

word_lengths("one two three", min_length=10)
# []

word_lengths("  hello!!!   world  ", min_length=5)
# [5, 5]

word_lengths("python is fun")
# [6, 2, 3]
```

**Things to consider:**

- At what point should you check the length of a word?
- Should punctuation be removed before applying the minimum length?
- How can you use conditional statements to decide which values to include?
- How can you ensure your previous tests still pass?

## Testing

You should write your own tests using `pytest`.

The examples above are not exhaustive. Think carefully about other inputs that might cause your function to behave unexpectedly.

Some areas worth testing include:

- Empty strings.
- Single-word sentences.
- Sentences containing multiple words.
- Leading and trailing whitespace.
- Multiple spaces between words.
- Words containing several punctuation characters.
- Sentences containing only punctuation.
- Different minimum word lengths.
- Cases where no words satisfy the minimum length.

**Example:**

```python
from main import word_lengths


def test_single_word():
    assert word_lengths("hello") == [5]


def test_multiple_words():
    assert word_lengths("python is fun") == [6, 2, 3]


def test_empty_sentence():
    assert word_lengths("") == []


# Write additional tests below.
```

Run your tests using:

```bash
pytest -v
```

Remember that you should not rely only on the example tests. Try to identify edge cases independently.

## Technical Assessment Practice

Before implementing your solution, consider how you would explain your approach to an interviewer.

You should be prepared to discuss:

1. What inputs does your function accept, and what should it return?
2. How will you separate the sentence into individual words?
3. Which Python string methods would be useful?
4. How will you build the resulting list?
5. What edge cases should you account for?
6. How will you test the function?
7. How would you extend your solution when the requirements change?

**Start with Step 1.** Get your initial solution working and write your own tests before attempting the later steps.
