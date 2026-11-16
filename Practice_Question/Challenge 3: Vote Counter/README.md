# Challenge 3: Vote Counter

Create a program that counts votes submitted by different people and determines the results of an election. Build your solution step by step, starting with basic vote counting before introducing more complicated requirements.

REMINDER: The examples provided are only a starting point. You should be writing your own tests to ensure your code works as expected!

## ⚠️ Note

There is *likely* too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Background

Many applications allow users to vote for different options, whether that involves selecting a winner in a competition, choosing a preferred product or electing a representative.

Imagine you are working for a company that organises competitions where participants vote for their favourite candidates.

Currently, votes are collected and stored in a Python list. Each element contains the name of the candidate who received a vote.

For example:

```python
["Alex", "Sam", "Alex", "Jo", "Sam", "Alex"]
```

The company wants a program that can process these votes and determine how many votes each candidate received.

In this example:

- Alex received 3 votes.
- Sam received 2 votes.
- Jo received 1 vote.

The resulting data should look like this:

```python
{
    "Alex": 3,
    "Sam": 2,
    "Jo": 1
}
```

As the company grows, the system will need to handle inconsistent name formatting, determine winners and generate sorted leaderboards.

Your task is to develop these features progressively.

## Step 1: Basic Vote Counting

Your task is to create a function called `count_votes` that takes a list of candidate names and returns a dictionary containing the number of votes each candidate received.

Start with the following function:

```python
def count_votes(votes: list[str]) -> dict[str, int]:
    pass
```

For this first step, you can assume:

- Every element in the list contains a valid candidate name.
- Candidate names are case-sensitive.
- Each occurrence of a name represents one vote.
- The list may be empty.

**Requirements:**

- Count how many times each candidate appears in the list.
- Store each candidate's name as a dictionary key.
- Store their total votes as the corresponding dictionary value.
- A candidate should only appear once in the resulting dictionary.
- Return an empty dictionary if no votes have been submitted.
- Do not modify the original list.

**Examples:**

```python
count_votes(["Alex", "Sam", "Alex", "Jo"])
# {"Alex": 2, "Sam": 1, "Jo": 1}

count_votes(["Ben", "Ben", "Ben"])
# {"Ben": 3}

count_votes(["Alex", "Sam", "Jo"])
# {"Alex": 1, "Sam": 1, "Jo": 1}

count_votes(["Alex", "alex", "ALEX"])
# {"Alex": 1, "alex": 1, "ALEX": 1}

count_votes([])
# {}
```

**Things to consider:**

- What is the difference between a list and a dictionary?
- How can you check whether a key already exists in a dictionary?
- How can you update a value associated with an existing key?
- What should happen when a candidate appears for the first time?
- What should happen when the same candidate appears again?

Make sure you understand how dictionary keys and values work before moving to the next step.

## Step 2: Case-Insensitive Voting

The company has discovered that some voters enter candidate names using different combinations of uppercase and lowercase letters.

For example:

```python
["Alex", "alex", "ALEX", "Sam"]
```

Currently, your function treats `"Alex"`, `"alex"` and `"ALEX"` as three different candidates.

However, these names should all refer to the same person.

Extend your solution so that votes are counted without considering differences in letter case.

The company has also noticed that some voters accidentally include spaces at the beginning or end of candidate names.

Your function should handle these situations as well.

**Requirements:**

- Treat candidate names as case-insensitive.
- Convert candidate names to lowercase before storing them in the dictionary.
- Ignore leading and trailing whitespace around each name.
- If a name is empty or contains only whitespace, ignore that vote.
- Continue counting repeated names correctly.
- Do not modify the original input list.

For this step, assume that all non-empty names are valid.

**Examples:**

```python
count_votes(["Alex", "alex", "ALEX", "Sam"])
# {"alex": 3, "sam": 1}

count_votes(["Ben", "BEN", "ben"])
# {"ben": 3}

count_votes([" Alex ", "alex", " Sam "])
# {"alex": 2, "sam": 1}

count_votes(["Alex", "", "Sam", "   ", "Alex"])
# {"alex": 2, "sam": 1}

count_votes([" JO ", "jo", "Jo", "alex"])
# {"jo": 3, "alex": 1}

count_votes(["", "   "])
# {}

count_votes([])
# {}
```

**Things to consider:**

- Which Python string method can convert text to lowercase?
- How can you remove whitespace from the beginning and end of a string?
- What is the difference between an empty string and a string containing spaces?
- At what point should a candidate's name be formatted?
- How can you reuse your original vote-counting logic?

Your solution should continue to handle the vote-counting requirements from Step 1, using the new case-insensitive rules.

## Step 3: Determine the Election Winner

The company can now count votes accurately, but it also needs to determine which candidate has won the election.

Create a second function called `find_winner`.

```python
def find_winner(votes: list[str]) -> str | None:
    pass
```

The function should return the name of the candidate who received the highest number of votes.

For example:

```python
["Alex", "Sam", "Alex", "Jo", "Alex", "Sam"]
```

Alex received three votes, Sam received two votes and Jo received one vote.

Therefore, the winner is:

```python
"alex"
```

However, elections can sometimes result in a tie.

For example:

```python
["Sam", "Alex", "Sam", "Alex"]
```

Both candidates have received two votes.

To make the result predictable, the company has decided that when two or more candidates have the same highest vote count, the candidate whose name comes first alphabetically should be selected.

Therefore, the winner would be `"alex"`.

**Requirements:**

- Count the number of votes received by each candidate.
- Follow the name-formatting rules introduced in Step 2.
- Return the name of the candidate with the highest vote count.
- If multiple candidates have the highest count, return the alphabetically first name.
- The returned name must be lowercase.
- Return `None` if there are no valid votes.
- Do not modify the original input list.

You may reuse your `count_votes` function.

**Examples:**

```python
find_winner(["Alex", "Sam", "Alex", "Jo"])
# "alex"

find_winner(["Sam", "Alex", "Sam", "Alex"])
# "alex"

find_winner(["Ben", "Alex", "Charlie"])
# "alex"

find_winner(["JO", "jo", "Alex", "alex", "Sam"])
# "alex"

find_winner(["Charlie"])
# "charlie"

find_winner(["", "   "])
# None

find_winner([])
# None
```

**Things to consider:**

- How can you access the values stored in a dictionary?
- How can you keep track of the highest vote count?
- How will you determine which candidate wins when there is a tie?
- How can you compare strings alphabetically?
- Can you reuse a function you have already written instead of repeating its logic?
- Why is it important to decide what happens when the list is empty?

## Step 4: Generate a Leaderboard

The company now wants to display the full election results rather than just the winner.

Create a third function called `leaderboard`.

```python
def leaderboard(
    votes: list[str],
    top_n: int | None = None
) -> list[tuple[str, int]]:
    pass
```

Instead of returning a dictionary, this function should return a list of tuples.

Each tuple should contain:

1. The candidate's name.
2. The total number of votes they received.

The candidates should be sorted based on how many votes they received.

For example, given:

```python
["Alex", "Sam", "Alex", "Jo", "Sam", "Alex"]
```

The leaderboard should be:

```python
[
    ("alex", 3),
    ("sam", 2),
    ("jo", 1)
]
```

Notice that the candidate with the most votes appears first.

If two candidates have the same number of votes, they should be sorted alphabetically.

The company would also like to display only the highest-ranking candidates when requested.

For example, setting `top_n=2` should return only the first two candidates in the leaderboard.

**Requirements:**

- Use the case-insensitive counting rules from Step 2.
- Return a list of tuples containing each candidate's name and vote count.
- Sort candidates by their vote count in descending order.
- If candidates have equal votes, sort them alphabetically by name.
- The optional parameter `top_n` determines the maximum number of candidates returned.
- If `top_n` is `None`, return all candidates.
- If `top_n` is `0`, return an empty list.
- If `top_n` is larger than the number of candidates, return the entire leaderboard.
- Assume `top_n` is either `None` or a non-negative integer.
- Return an empty list when there are no valid votes.

**Examples:**

```python
leaderboard(["Alex", "Sam", "Alex", "Jo", "Sam", "Alex"])
# [("alex", 3), ("sam", 2), ("jo", 1)]

leaderboard(["Alex", "Sam", "Alex", "Jo", "Sam", "Alex"], top_n=2)
# [("alex", 3), ("sam", 2)]

leaderboard(["Sam", "Alex", "Jo"])
# [("alex", 1), ("jo", 1), ("sam", 1)]

leaderboard(["Ben", "BEN", "Alex", "Jo", "jo"])
# [("ben", 2), ("jo", 2), ("alex", 1)]

leaderboard(["Alex", "Sam", "Alex"], top_n=1)
# [("alex", 2)]

leaderboard(["Alex", "Sam"], top_n=0)
# []

leaderboard(["Alex", "Sam"], top_n=10)
# [("alex", 1), ("sam", 1)]

leaderboard([])
# []
```

**Things to consider:**

- How can you convert dictionary entries into tuples?
- What is the difference between sorting in ascending and descending order?
- How can you sort by more than one condition?
- How can you handle candidates with identical vote counts?
- How can you return only the first `top_n` results?
- How could your existing `count_votes` function help you complete this task?

## Testing

You should create your own tests using `pytest`.

The examples above demonstrate the expected behaviour, but they do not cover every possible situation.

You are responsible for identifying normal cases, edge cases and situations where your implementation might fail.

Before moving to the next step, ensure that you have written enough tests to demonstrate that your solution meets the requirements.

Consider whether your tests cover dictionary operations, string formatting, repeated values, ties, sorting and optional parameters.

Run your tests using:

```bash
pytest -v
```

## Technical Assessment Practice

Before writing your solution, practise explaining your approach as though you were in a technical interview.

Consider the following questions:

1. Why is a dictionary appropriate for counting votes?
2. What is the difference between a dictionary key and its value?
3. How can you count occurrences without repeatedly searching the entire list?
4. Why should names be formatted before counting votes?
5. How will you handle an empty input?
6. How can you determine the highest value in a dictionary?
7. How will you handle multiple candidates receiving the same number of votes?
8. What is the difference between a list and a tuple?
9. How can you sort information using multiple conditions?
10. How will you organise your solution to avoid repeating code?

**Start with Step 1.** Implement basic vote counting, write your own tests and get them passing before extending your solution.

Focus on understanding each requirement rather than attempting to complete the entire challenge immediately.