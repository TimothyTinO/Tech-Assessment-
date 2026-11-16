# Tic-Tac-Toe Referee

You're writing the referee for _Noughts & Crosses Online_. Given a board, it decides who has won.

REMINDER: `test.py` is empty. You should be writing tests to ensure your code works as expected!

## ⚠️ Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Step 1: Find the Winner

A board is a list of 3 strings, each 3 characters long, made up of `"X"`, `"O"` and `"."` (an empty square).

Write `winner(board)` that returns `"X"` or `"O"` if that player has three in a row (horizontally, vertically or diagonally), or `None` if nobody has.

**Examples:**
```python
winner(["XXX",
        "OO.",
        "..."])
# Returns: "X"

winner(["O.X",
        "OX.",
        "O.X"])
# Returns: "O"

winner(["X.O",
        ".XO",
        "..X"])
# Returns: "X"

winner(["XO.",
        "...",
        "..."])
# Returns: None
```

## Step 2: Game Status

Write `game_status(board)` that returns one of these strings:

- `"Invalid"`: the numbers of `X` and `O` are impossible. `X` always goes first, so there must be the same number of each, or exactly one more `X`.
- `"X wins"` or `"O wins"`
- `"Draw"`: the board is full and nobody has won
- `"In progress"`: there are still empty squares and nobody has won

**Examples:**
```python
game_status(["XXX", "OO.", "..."])   # "X wins"
game_status(["XX.", "OOO", "X.."])   # "O wins"
game_status(["XOX", "XOO", "OXX"])   # "Draw"
game_status(["XO.", "...", "..."])   # "In progress"
game_status(["XXX", "XXX", "..."])   # "Invalid"
```

## Step 3: Any Board Size

Make `winner` work for square boards of **any** size (3x3, 4x4, 5x5, ...). To win you need a full row, a full column, or a full diagonal.

**Examples:**
```python
winner(["XO..",
        "XO..",
        "X...",
        "X..."])
# Returns: "X"

winner(["..O",
        ".O.",
        "O.."])
# Returns: "O"

winner(["XXOO",
        "OOXX",
        "XXOO",
        "OXXO"])
# Returns: None
```

## 💡 Hints

1. For Step 1, make a list of all the "lines" to check (3 rows, 3 columns, 2 diagonals), then see if any line is all `X` or all `O`.
2. `board[r][c]` gets the character at row `r`, column `c`.
3. For Step 2, `"".join(board).count("X")` counts all X's on the board.
4. Do the `Invalid` check first, before looking for a winner.
5. For Step 3, use `len(board)` instead of the number 3, and build the lines with loops.
6. A full line is all the same when `set(line)` has exactly one item, and that item isn't `"."`.
