# Challenge 4: Scoreboard Organiser

Create a program that processes player scores and generates an organised scoreboard. Build your solution step by step, starting with basic string manipulation before introducing sorting, dictionaries and ranking systems.

REMINDER: The examples provided are only a starting point. You should be writing your own tests to ensure your code works as expected!

## ⚠️ Note

There is *likely* too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Background

Many online games and competitions use scoreboards to display how well players are performing.

These scoreboards allow players to compare their scores and see how they rank against others.

Imagine you are working for a company that organises online gaming competitions.

During each competition, the system records player names and their scores. However, the information is currently stored as a single string rather than an organised data structure.

For example:

```python
"Alex:10;Sam:30;Jo:20"
```

Each record contains a player's name followed by their score, separated by a colon (`:`).

Individual records are separated by a semicolon (`;`).

The company wants to convert this information into a scoreboard where players are ordered from the highest score to the lowest.

For example, the string above should produce:

```python
[
    ("Sam", 30),
    ("Jo", 20),
    ("Alex", 10)
]
```

Notice that:

- The player's name is stored as a string.
- Their score is stored as an integer.
- Each player is represented by a tuple.
- The scoreboard is a list of tuples.
- The player with the highest score appears first.

As the competition grows, additional requirements will be introduced, including handling tied scores, combining repeated player records and assigning rankings.

Your task is to implement these features progressively.

---

## Step 1: Basic Scoreboard

Create a function called `scoreboard` that accepts a string containing player records and returns a list of tuples sorted by score.

Start with the following function:

```python
def scoreboard(records: str) -> list[tuple[str, int]]:
    pass
```

For this first step, you can assume:

- Each record follows the format `Name:Score`.
- Records are separated by semicolons (`;`).
- Every name is valid and contains no spaces.
- Each score is a valid integer.
- Each player appears only once.
- There are no unnecessary spaces in the input.
- The input may be empty.

**Requirements:**

- Separate the input string into individual player records.
- Extract each player's name and score.
- Convert the score from a string into an integer.
- Store each player as a tuple containing their name and score.
- Return a list of these tuples.
- Sort players by their scores in descending order.
- If two players have the same score, preserve their original input order.
- Return an empty list if the input string is empty.

**Examples:**

```python
scoreboard("Alex:10;Sam:30;Jo:20")
# [("Sam", 30), ("Jo", 20), ("Alex", 10)]

scoreboard("Ben:50;Alex:100;Charlie:75")
# [("Alex", 100), ("Charlie", 75), ("Ben", 50)]

scoreboard("Sam:10;Alex:10;Jo:5")
# [("Sam", 10), ("Alex", 10), ("Jo", 5)]

scoreboard("Alex:25")
# [("Alex", 25)]

scoreboard("Alex:-5;Sam:10;Jo:0")
# [("Sam", 10), ("Jo", 0), ("Alex", -5)]

scoreboard("")
# []
```

**Things to consider:**

- Which string method allows you to separate records using a semicolon?
- How can you separate a player's name from their score?
- What is the difference between `"10"` and `10` in Python?
- How can you convert a string into an integer?
- How can you create a tuple containing two values?
- How can you sort a list of tuples based on the second element?
- How can you preserve the original order when two scores are equal?

Make sure your solution works with the examples before moving on.

---

## Step 2: Handling Tied Scores

The company has noticed that some competitions have multiple players who achieve the same score.

Currently, players with equal scores appear in the order in which their results were submitted.

However, the company wants tied players to be displayed alphabetically.

For example:

```python
"Sam:20;Alex:20;Jo:30"
```

Both Sam and Alex have scored 20 points.

Since Alex comes before Sam alphabetically, Alex should appear first.

The expected scoreboard is:

```python
[
    ("Jo", 30),
    ("Alex", 20),
    ("Sam", 20)
]
```

The company has also noticed that some records contain unnecessary spaces around player names and scores.

Extend your solution to handle these situations.

**Requirements:**

- Continue sorting players by score in descending order.
- When players have the same score, sort them alphabetically by name in ascending order.
- Ignore leading and trailing spaces around player names.
- Ignore leading and trailing spaces around score values.
- Continue returning scores as integers.
- Player names are case-sensitive, and alphabetical ordering follows Python's normal string comparison.
- Assume that all records contain valid names and integer scores after removing surrounding spaces.

**Examples:**

```python
scoreboard("Sam:20;Alex:20;Jo:30")
# [("Jo", 30), ("Alex", 20), ("Sam", 20)]

scoreboard("Charlie:10;Ben:10;Alex:10")
# [("Alex", 10), ("Ben", 10), ("Charlie", 10)]

scoreboard(" Alex : 30 ; Sam : 20 ; Jo : 10 ")
# [("Alex", 30), ("Sam", 20), ("Jo", 10)]

scoreboard("Ben:50;Alex:50;Charlie:100")
# [("Charlie", 100), ("Alex", 50), ("Ben", 50)]

scoreboard("Sam:-10;Alex:-10;Jo:0")
# [("Jo", 0), ("Alex", -10), ("Sam", -10)]

scoreboard("")
# []
```

**Things to consider:**

- How can you remove unwanted spaces from the beginning and end of a string?
- How can you sort using more than one condition?
- How can you sort scores in descending order while sorting names in ascending order?
- What happens when every player has the same score?
- How can you keep your original solution readable as more requirements are introduced?

Your solution should still satisfy the requirements from Step 1, using the new tie-breaking rules.

---

## Step 3: Combining Duplicate Player Records

The company now wants to support competitions where players can participate in multiple rounds.

Each round produces a new score, meaning the same player may appear more than once in the input.

For example:

```python
"Alex:10;Sam:20;Alex:15;Jo:25"
```

Alex participated in two rounds:

- First round: 10 points.
- Second round: 15 points.

Alex's total score should therefore be 25 points.

The company wants the scoreboard to display each player only once, showing their combined score across all rounds.

The expected result is:

```python
[
    ("Alex", 25),
    ("Jo", 25),
    ("Sam", 20)
]
```

Notice that Alex and Jo have the same total score, so the alphabetical sorting rule from Step 2 applies.

**Requirements:**

- Identify players who appear more than once.
- Combine all scores belonging to the same player.
- Each player should appear only once in the final scoreboard.
- Continue sorting by total score in descending order.
- Continue sorting tied scores alphabetically by name.
- Preserve the name-formatting rules introduced in Step 2.
- Player names remain case-sensitive.
- Negative scores must still be supported.
- Return an empty list if the input is empty.

**Examples:**

```python
scoreboard("Alex:10;Sam:20;Alex:15;Jo:25")
# [("Alex", 25), ("Jo", 25), ("Sam", 20)]

scoreboard("Ben:10;Ben:20;Ben:30")
# [("Ben", 60)]

scoreboard("Sam:20;Alex:30;Sam:15;Jo:40")
# [("Jo", 40), ("Sam", 35), ("Alex", 30)]

scoreboard("Alex:10;Sam:20;Alex:-5")
# [("Sam", 20), ("Alex", 5)]

scoreboard(" Alex : 10 ;Alex:20; Sam :30")
# [("Alex", 30), ("Sam", 30)]

scoreboard("Alex:10;alex:20")
# [("alex", 20), ("Alex", 10)]

scoreboard("")
# []
```

**Things to consider:**

- Which Python data structure would help you keep track of each player's total score?
- How can you check whether a player has already been recorded?
- What should happen when you encounter a player for the first time?
- What should happen when a player appears again?
- How can you convert the combined results into a list of tuples?
- Should you combine scores before or after sorting?
- How can you reuse the functionality from your earlier steps?

Your solution should now support repeated players while preserving the ordering rules established previously.

---

## Step 4: Player Rankings

The company can now calculate and sort players' total scores, but it also wants to display their positions in the competition.

Create a second function called `ranked_scoreboard`.

```python
def ranked_scoreboard(records: str) -> list[tuple[int, str, int]]:
    pass
```

The function should return a list of tuples containing:

1. The player's rank.
2. The player's name.
3. Their total score.

For example:

```python
"Alex:10;Sam:30;Jo:20"
```

The expected result would be:

```python
[
    (1, "Sam", 30),
    (2, "Jo", 20),
    (3, "Alex", 10)
]
```

However, ranking becomes more complicated when players have the same score.

The company has decided to use **competition ranking**.

This means that players with the same score receive the same rank, and the next position accounts for the number of players ahead of it.

For example, imagine four players with the following scores:

| Player | Score |
|---|---:|
| Alex | 50 |
| Sam | 40 |
| Jo | 40 |
| Ben | 30 |

Alex is ranked first.

Sam and Jo both have 40 points, so they share second place.

Ben is ranked fourth, not third, because three players have scores higher than or equal to his score and appear ahead of him.

The ranks would therefore be:

```python
[
    (1, "Alex", 50),
    (2, "Jo", 40),
    (2, "Sam", 40),
    (4, "Ben", 30)
]
```

**Requirements:**

- Reuse the score-processing rules from Step 3.
- Combine duplicate player scores before assigning rankings.
- Sort by total score in descending order.
- Sort players with equal scores alphabetically.
- Assign rank 1 to the player with the highest score.
- Players with equal scores must receive the same rank.
- When players share a rank, skip the appropriate number of subsequent ranks.
- Return a list of tuples containing `(rank, name, total_score)`.
- Return an empty list if no records are provided.

**Examples:**

```python
ranked_scoreboard("Alex:10;Sam:30;Jo:20")
# [(1, "Sam", 30), (2, "Jo", 20), (3, "Alex", 10)]

ranked_scoreboard("Alex:50;Sam:40;Jo:40;Ben:30")
# [(1, "Alex", 50), (2, "Jo", 40), (2, "Sam", 40), (4, "Ben", 30)]

ranked_scoreboard("Sam:20;Alex:20;Jo:20")
# [(1, "Alex", 20), (1, "Jo", 20), (1, "Sam", 20)]

ranked_scoreboard("Alex:10;Sam:20;Alex:15;Jo:25")
# [(1, "Alex", 25), (1, "Jo", 25), (3, "Sam", 20)]

ranked_scoreboard("Ben:30")
# [(1, "Ben", 30)]

ranked_scoreboard("")
# []
```

**Things to consider:**

- Can you reuse your `scoreboard` function rather than processing everything again?
- How can you determine whether two consecutive players have the same score?
- How can you track the current player's position?
- What is the difference between a player's position in a list and their competition rank?
- Why does competition ranking sometimes skip numbers?
- How can you handle a scoreboard where all players have identical scores?

---

## Testing

You should write your own tests using `pytest`.

The examples above are intended to demonstrate the expected behaviour, but they do not cover every possible situation.

You are responsible for deciding which cases need testing.

Think about how you would verify the following areas:

- Parsing strings into individual records.
- Converting scores into integers.
- Handling empty inputs.
- Sorting scores in descending order.
- Sorting names alphabetically when scores are tied.
- Handling additional whitespace.
- Combining repeated player records.
- Processing negative scores.
- Assigning ranks when players have equal scores.
- Calculating the correct rank after a tie.

Try to identify other edge cases independently.

Run your tests using:

```bash
pytest -v
```

Remember that passing a small number of examples does not guarantee your solution works for every valid input.

## Technical Assessment Practice

Before writing your solution, consider how you would explain your approach to an interviewer.

You should be prepared to answer the following questions:

1. What are the input and output types of each function?
2. How will you separate a string containing multiple records?
3. How can you convert string values into integers?
4. Why might tuples be appropriate for representing player records?
5. How can you sort data using more than one condition?
6. Which data structure would help you combine scores for duplicate players?
7. Why is it better to combine repeated records before sorting?
8. How can you reuse existing functions as the requirements grow?
9. How will you calculate ranks when multiple players have the same score?
10. What edge cases could cause your implementation to fail?

**Start with Step 1.** Focus on understanding string manipulation, tuples and basic sorting before introducing dictionaries and rankings.

You should aim to write your own tests and be able to explain your reasoning before moving on to the next step.