# Word Frequency

You're building a text analysis tool for _Bookworm Analytics_, which helps authors see which words they overuse.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Top Words

Write `top_words(text, n)` that returns the `n` most common words as a list of `(word, count)` tuples.

- Words are case-insensitive (store them lowercase).
- Punctuation should not be part of a word.
- Sort by count (highest first), then alphabetically for ties.

**Examples:**
```python
top_words("the cat and the hat and the bat", 2)
# Returns: [("the", 3), ("and", 2)]

top_words("Hello, hello! HELLO?", 1)
# Returns: [("hello", 3)]

top_words("", 3)
# Returns: []
```

## Step 2: Stop Words

Add an optional `stop_words` argument, a set of words to ignore completely.

Apostrophes **inside** a word (like `don't`) should be kept as part of that word.

**Examples:**
```python
top_words("the cat and the hat and the bat", 2, stop_words={"the", "and"})
# Returns: [("bat", 1), ("cat", 1)]

top_words("Don't stop. Don't, don't!", 1)
# Returns: [("don't", 3)]
```

## Step 3: Phrases (N-grams)

Write `top_ngrams(text, n, size=2)` that does the same thing for sequences of `size` consecutive words. Each phrase is the words joined by a single space.

Words are cleaned the same way as in Step 1 (lowercase, no punctuation). Do **not** apply stop words here.

**Examples:**
```python
top_ngrams("the cat and the hat and the cat", 2)
# Returns: [("and the", 2), ("the cat", 2)]

top_ngrams("a b c a b c", 1, size=3)
# Returns: [("a b c", 2)]

top_ngrams("just two", 1, size=3)
# Returns: []   (not enough words)
```

## 💡 Hints

1. Split the text with `.split()`, then clean each word: `.lower()` and `.strip(".,!?;:\"")` remove case and punctuation (but keep apostrophes inside words).
2. A plain dictionary works for counting: `counts[word] = counts.get(word, 0) + 1`.
3. To sort by count descending and then alphabetically, use `sorted(counts.items(), key=lambda kv: (-kv[1], kv[0]))`.
4. For n-grams, build them with a sliding window: `words[i:i+size]` for each valid `i`.
