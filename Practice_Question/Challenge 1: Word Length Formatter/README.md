
Word Length Formatter
Create a Python program that solves the problem below. Build your solution step by step, extending your code as the requirements change.

Reminder: Any example tests are only a starting point. Write your own pytest tests to check normal inputs, edge cases, and unexpected combinations.

Assessment note: There is likely more work here than you can complete in the allotted time. You are not expected to finish every extension. Focus on a working solution, tests, and explaining your decisions.

How to approach this challenge
Read Step 1 fully before writing code.
Explain what the function receives and what it must return.
Write two or three tests of your own, then implement Step 1.
Run pytest -v and fix any failures.
Only then move on to the next step. Update your tests as the requirements change.
Be ready to describe your algorithm and any edge cases aloud.
You may use built-in Python functions and methods. Do not change the required function name or return type.

Background
A text-analysis team needs to measure how long the words in a message are. The first version is deliberately simple. As the requirements change, your program must handle messy spacing and punctuation without losing track of the words.

This challenge mainly tests strings, .split(), loops, lists, and careful interpretation of requirements.

Understanding the input
The input is one string, such as "Python is fun". The output is a list of integers, where each integer represents the length of a word, in the same order as the input. Do not return a single total or a dictionary.

Step 1 — Count the letters in each word
Write the following function:

def word_lengths(sentence: str) -> list[int]:
    pass
For Step 1, assume words are separated by exactly one space. Return a list containing the length of each word. An empty sentence returns an empty list.

Examples

word_lengths("hello world")      # [5, 5]
word_lengths("Python is fun")    # [6, 2, 3]
word_lengths("a bb ccc")        # [1, 2, 3]
word_lengths("")                # []
Think about: What does splitting a sentence produce? How do you build a new list from the result? How can you handle an empty input without producing a length for a non-existent word?

Before continuing, test: one word, several words of different lengths, and an empty string.

Step 2 — Support uneven spacing
Real messages may have multiple spaces between words, or spaces at the beginning or end. Update the same function to ignore those extra spaces. Do not count blank segments as words.

Examples

word_lengths("hello   world")       # [5, 5]
word_lengths("  Python is fun  ")   # [6, 2, 3]
word_lengths("   ")                 # []
word_lengths("a    bb")             # [1, 2]
Think about: What is the difference between sentence.split() and sentence.split(" ")? Which behaviour helps you avoid empty words?

Before continuing, test: leading spaces, trailing spaces, repeated spaces, and a sentence containing only spaces.

Step 3 — Ignore selected punctuation
The team now wants the lengths of the words without counting these punctuation characters: . , ! ?. These characters may appear at the start, middle, or end of a word. All other characters continue to count normally. A segment made entirely of ignored punctuation should not contribute a length to the output.

Examples

word_lengths("Hello, world!")       # [5, 5]
word_lengths("Wait... what?!")      # [4, 4]
word_lengths("wow! really?")       # [3, 6]
word_lengths("Hi !!! there")        # [2, 5]
word_lengths("a-b")                 # [3]  # hyphen still counts
Think about: Do you need to remove punctuation from the original sentence, or can you work with each word? What happens if removing punctuation leaves an empty string?

Testing checklist
Step 1: simple words and empty input
Step 2: repeated, leading, and trailing spaces
Step 3: punctuation at different positions
Step 3: punctuation-only segments
Original word order is preserved
Interview-style questions
Why did you choose a list as your result?
What does your loop do on each iteration?
How did your tests change between Step 1 and Step 3?
What would happen if the input included a tab or newline? (You do not need to add extra support unless required.)
Submission guidance
Write your solution in a Python file and your tests in a separate test_*.py file. You can run pytest -v from the relevant project directory. The README intentionally contains no completed solution.

