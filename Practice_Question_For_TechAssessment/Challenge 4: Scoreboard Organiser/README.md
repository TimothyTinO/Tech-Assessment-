# Challenge 4: Scoreboard Organiser

Create a program that processes player scores and generates an organised scoreboard. Build your solution step by step, starting with basic string manipulation before introducing sorting, dictionaries and ranking systems.

## Background

A company that organises online gaming competitions wants to develop a system for managing player scores.

Currently, player results are stored as a single string:

```python
"Alex:10;Sam:30;Jo:20"
```

Each record contains a player's name and score separated by a colon (`:`). Individual records are separated by a semicolon (`;`).

The program should organise these records into a list of tuples, sorted from the highest score to the lowest.

For example:

```python
[
    ("Sam", 30),
    ("Jo", 20),
    ("Alex", 10)
]
```

As the requirements develop, the system will also need to handle tied scores, combine duplicate player records and assign rankings.

## Step 1: Basic Scoreboard

Create a function that takes a string containing player records and returns a list of tuples sorted by score.

```python
def scoreboard(records: str) -> list[tuple[str, int]]:
    pass
```

For this step, assume that each record follows the format `Name:Score`, all scores are valid integers, and each player appears only once.

**Requirements:**

- Separate the input into individual player records using semicolons.
- Extract each player's name and score.
- Convert scores into integers.
- Store each player as a tuple containing `(name, score)`.
- Sort players by score in descending order.
- If scores are equal, preserve the original input order.
- Return an empty list if the input is empty.
- Support positive scores, negative scores and zero.

**Examples:**

```python
scoreboard("Alex:10;Sam:30;Jo:20")
# [("Sam", 30), ("Jo", 20), ("Alex", 10)]

scoreboard("Ben:50;Alex:100;Charlie:75")
# [("Alex", 100), ("Charlie", 75), ("Ben", 50)]

scoreboard("Sam:10;Alex:10;Jo:5")
# [("Sam", 10), ("Alex", 10), ("Jo", 5)]

scoreboard("Alex:-5;Sam:10;Jo:0")
# [("Sam", 10), ("Jo", 0), ("Alex", -5)]

scoreboard("")
# []
```

## Step 2: Handling Tied Scores

The company has noticed that multiple players sometimes achieve the same score.

Extend your solution so that players with equal scores are sorted alphabetically by name.

The function should also handle unnecessary spaces around player names and scores.

**Requirements:**

- Continue sorting scores in descending order.
- If players have equal scores, sort their names alphabetically in ascending order.
- Remove leading and trailing spaces from player names and scores.
- Continue returning scores as integers.
- Treat names as case-sensitive and use Python's normal string comparison.
- Assume the records contain valid names and integer scores after removing spaces.

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

## Step 3: Combining Duplicate Player Records

The company now wants to support competitions where players participate in multiple rounds.

This means the same player may appear more than once in the input.

For example:

```python
"Alex:10;Sam:20;Alex:15;Jo:25"
```

Alex has scored 10 points in one round and 15 in another, giving a total of 25 points.

The scoreboard should display each player only once, using their combined score.

**Requirements:**

- Identify players who appear multiple times.
- Add together all scores belonging to the same player.
- Display each player only once.
- Sort by total score in descending order.
- Sort players with tied scores alphabetically.
- Continue removing unnecessary spaces.
- Treat names as case-sensitive.
- Continue supporting negative scores.
- Return an empty list if no records are provided.

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

## Step 4: Player Rankings

The company now wants to display players' positions in the competition.

Create a second function called `ranked_scoreboard`.

```python
def ranked_scoreboard(records: str) -> list[tuple[int, str, int]]:
    pass
```

Each tuple should contain:

- The player's rank.
- The player's name.
- Their total score.

The company has decided to use **competition ranking**, meaning players with equal scores share the same rank.

For example, consider:

```python
"Alex:50;Sam:40;Jo:40;Ben:30"
```

Alex ranks first, while Jo and Sam share second place. Ben ranks fourth rather than third, because three players appear ahead of him.

The expected result is:

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
- Combine duplicate player scores before assigning ranks.
- Sort by total score in descending order.
- Sort tied players alphabetically.
- Assign rank `1` to the highest-scoring player.
- Players with equal scores must receive the same rank.
- Skip the appropriate number of ranks after a tie.
- Return tuples containing `(rank, name, total_score)`.
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

Refer to the main **Coding Problems README** for testing requirements and technical assessment preparation guidance.