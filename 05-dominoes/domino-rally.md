# Domino Rally

Create a program that simulates a row of dominoes being knocked over, returning every frame of the fall. Build your solution step by step.

REMINDER: The tests provided are a minimal base. You should be writing tests to ensure your code works as expected!

## Note

There is _likely_ too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

The function signatures shown are suggestions. The examples are the contract.

## Background

In a domino rally, one push sets off a chain: each domino that falls knocks over the next. A row is a string made of these characters:

- `|` is a standing domino
- `.` is an empty spot
- `>` is a domino that has fallen to the right
- `<` is a domino that has fallen to the left

Time moves in frames. A domino that falls in one frame knocks over its neighbour in the next frame. Every frame you return is a string the same length as the row.

## Step 1: Simple Topple

Create a function that pushes the leftmost domino to the right and returns a list with one string per frame.

- Frame 1 shows the row just after the push
- In each later frame, the domino that fell last knocks over the domino immediately to its right
- The chain stops at an empty spot or at the end of the row. The last frame is the one in which the last domino falls
- The input contains only `|` and `.` and may be empty. With no dominoes, return an empty list

**Examples:**
```python
topple("|||")
# [">||", ">>|", ">>>"]

topple("||.||")
# [">|.||", ">>.||"]

topple("..|")
# ["..>"]

topple("")
# []
```

## Step 2: Push Anywhere, and Taller Dominoes

Extend your solution so any domino can be pushed in either direction, and so that tall dominoes can fall across a gap.

- `start` is the index of the domino to push and `direction` is `"L"` or `"R"`
- If there is no standing domino at `start`, return an empty list
- A falling domino looks up to `reach` cells ahead in the direction it fell, and knocks over the first domino it finds there
- `reach` defaults to 1, which is the Step 1 behaviour: only the adjacent cell
- Falling across a gap takes no extra time

**Examples:**
```python
topple("||||", 2, "L")
# ["||<|", "|<<|", "<<<|"]

topple("||.||", 0, "R")
# [">|.||", ">>.||"]

topple("||.||", 0, "R", reach=2)
# [">|.||", ">>.||", ">>.>|", ">>.>>"]

topple("|.|..|", 0, "R", reach=2)       # the gap of two is too wide
# [">.|..|", ">.>..|"]

topple("|.|..|", 5, "L", reach=3)
# ["|.|..<", "|.<..<", "<.<..<"]
```

## Step 3: Several Pushes at Once

Now several dominoes are pushed in frame 1, each given as `(index, direction)`. The chains run at the same time, and they can meet.

- A fallen domino stays as it fell. A chain that reaches a fallen domino stops there
- A standing domino hit from both sides in the same frame stays standing, and both chains end
- The same rule applies to one domino pushed both ways at once

**Examples:**
```python
topple("|||||", [(0, "R"), (4, "L")])     # the middle domino is hit from both sides
# [">|||<", ">>|<<"]

topple("||||", [(0, "R"), (3, "L")])
# [">||<", ">><<"]

topple("||||||", [(2, "L"), (3, "R")])
# ["||<>||", "|<<>>|", "<<<>>>"]

topple("|||||||", [(0, "R"), (3, "R")])   # the first chain stops when it catches the second
# [">||>|||", ">>|>>||", ">>>>>>|", ">>>>>>>"]

topple("|.|.|", [(0, "R"), (4, "L")], reach=2)
# [">.|.<"]
```

## Step 4: Timed Pushes

Finally, pushes can happen in any frame. Each push is now `(frame, index, direction)`, with frames counted from 1.

- A push lands in its frame together with any hits from running chains. A domino pushed one way and hit the other way in the same frame stays standing
- A push on an empty spot or a fallen domino does nothing
- A frame in which nothing falls is still returned if a domino falls in a later frame. The list ends with the last frame in which a domino falls

**Examples:**
```python
topple("||||||", [(1, 0, "R"), (3, 5, "L")])
# [">|||||", ">>||||", ">>>||<", ">>>><<"]

topple("|||||", [(1, 0, "R"), (3, 2, "L")])   # the late push meets the chain on domino 2
# [">||||", ">>|||"]

topple("|.|", [(1, 0, "R"), (3, 2, "L")])     # frame 2 is unchanged but still returned
# [">.|", ">.|", ">.<"]
```

## If You Finish Early

Given a row and a `reach`, what is the smallest number of frame-1 pushes that leaves no domino standing?
