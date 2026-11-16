# Challenge 3: Vote Counter

Create a program that counts votes submitted for different candidates and determines the results of an election. Build your solution step by step.

## Background

A company that organises competitions wants to develop a system for counting votes.

Each vote is represented by a candidate's name stored in a Python list.

For example:

```python
["Alex", "Sam", "Alex", "Jo", "Sam", "Alex"]
```

The program should count how many votes each candidate received and return:

```python
{
    "Alex": 3,
    "Sam": 2,
    "Jo": 1
}
```

As the requirements develop, the program will also need to handle inconsistent name formatting, determine winners and generate sorted leaderboards.

## Step 1: Basic Vote Counting

Create a function that takes a list of candidate names and returns a dictionary containing the number of votes received by each candidate.

```python
def count_votes(votes: list[str]) -> dict[str, int]:
    pass
```

**Requirements:**

- Count how many times each candidate appears.
- Store candidate names as dictionary keys and their vote counts as values.
- Each candidate should only appear once in the dictionary.
- Treat uppercase and lowercase names as different candidates.
- Return an empty dictionary if no votes are provided.
- Do not modify the original list.

**Examples:**

```python
count_votes(["Alex", "Sam", "Alex", "Jo"])
# {"Alex": 2, "Sam": 1, "Jo": 1}

count_votes(["Ben", "Ben", "Ben"])
# {"Ben": 3}

count_votes(["Alex", "alex", "ALEX"])
# {"Alex": 1, "alex": 1, "ALEX": 1}

count_votes([])
# {}
```

## Step 2: Case-Insensitive Voting

The company has noticed that some voters enter candidate names using different combinations of uppercase and lowercase letters.

Extend your function so that names referring to the same candidate are counted together.

**Requirements:**

- Treat names as case-insensitive.
- Convert names to lowercase before storing them.
- Remove leading and trailing whitespace.
- Ignore empty names or names containing only spaces.
- Continue counting repeated names correctly.
- Do not modify the original list.

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

count_votes(["", "   "])
# {}
```

## Step 3: Determine the Election Winner

The company now wants to determine which candidate received the most votes.

Create a second function called `find_winner`.

```python
def find_winner(votes: list[str]) -> str | None:
    pass
```

If multiple candidates receive the same highest number of votes, the candidate whose name comes first alphabetically should be selected.

**Requirements:**

- Follow the case-insensitive counting rules from Step 2.
- Return the candidate with the highest vote count.
- If there is a tie, return the alphabetically first candidate.
- Return the winner's name in lowercase.
- Return `None` if there are no valid votes.
- You may reuse your `count_votes` function.

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

find_winner([])
# None
```

## Step 4: Generate a Leaderboard

The company now wants to display all candidates ranked by their total number of votes.

Create a third function called `leaderboard`.

```python
def leaderboard(
    votes: list[str],
    top_n: int | None = None
) -> list[tuple[str, int]]:
    pass
```

Each result should contain a tuple consisting of the candidate's name and their total votes.

The optional `top_n` parameter determines how many candidates should be returned.

**Requirements:**

- Follow the case-insensitive counting rules from Step 2.
- Return a list of tuples containing `(candidate, votes)`.
- Sort candidates by vote count in descending order.
- If candidates have equal votes, sort them alphabetically.
- If `top_n` is provided, return only the highest-ranking candidates.
- If `top_n` is `None`, return all candidates.
- If `top_n` is `0`, return an empty list.
- If `top_n` exceeds the number of candidates, return the entire leaderboard.
- Assume `top_n` is a non-negative integer or `None`.
- Return an empty list if there are no valid votes.

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

leaderboard(["Alex", "Sam"], top_n=0)
# []

leaderboard([])
# []
```

Refer to the main **Coding Problems README** for testing requirements and technical assessment preparation guidance.