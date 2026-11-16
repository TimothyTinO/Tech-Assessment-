Challenge 1: Word Length Formatter
Focus: String manipulation, split(), loops, and output formatting
Task
Create a function that describes how many characters are in each word of a sentence.
def word_lengths(sentence: str) -> str:
    """Return each word with its character count."""
    pass
Step 1: Basic Word Lengths
Return a string in the format word:length, with entries separated by ;. Assume words are separated by a single space.
word_lengths("red blue green")
# "red:3;blue:4;green:5"

word_lengths("hello")
# "hello:5"

word_lengths("")
# ""
Step 2: Handle Extra Whitespace
Ignore leading, trailing, and repeated spaces. The output should not contain empty entries.
word_lengths("  red   blue  ")
# "red:3;blue:4"
Step 3: Ignore Punctuation When Counting
For the count only, ignore these punctuation characters: .,!?. Preserve the original word, including its punctuation, in the output.
word_lengths("Hello, world!")
# "Hello,:5;world!:5"

word_lengths("wow!!!")
# "wow!!!:3"
Write your own tests for: an empty sentence, one word, repeated spaces, and punctuation.