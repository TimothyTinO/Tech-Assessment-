# Challenge 2: Neighbour Sum Generator

Create a program that processes a list of numbers and calculates sums using neighbouring elements. Build your solution step by step, starting with basic list indexing before introducing more complicated requirements.

REMINDER: The examples provided are a minimal guide. You should be writing your own tests to ensure your code works as expected!

## ⚠️ Note

There is *likely* too much work here to be done in the time you've been given. You are **not** expected to complete the whole challenge.

## Background

Working with lists is a common task in software development. Many applications need to process sequences of information, such as temperatures, financial transactions, scores or measurements collected over time.

Imagine you are working for a company that develops software to analyse measurements collected by sensors.

Each sensor records a number, and the measurements are stored in a Python list in the order they were collected.

For example, consider the following measurements:

```python
[10, 20, 30, 40]
```

The company wants to analyse how neighbouring measurements behave when combined.

Initially, the system should add each number to the number immediately after it.

For the example above:

- The first calculation is `10 + 20 = 30`.
- The second calculation is `20 + 30 = 50`.
- The third calculation is `30 + 40 = 70`.

The resulting list would be:

```python
[30, 50, 70]
```

As the requirements become more complicated, you will extend your solution to support circular lists and configurable distances between numbers.

## Step 1: Basic Neighbour Sums

Your task is to create a function called `neighbour_sums` that takes a list of integers and returns a new list containing the sum of every pair of adjacent numbers.

Start with the following function:

```python
def neighbour_sums(numbers: list[int]) -> list[int]:
    pass
```

Two numbers are considered adjacent when they appear directly next to each other in the list.

For example, given:

```python
[1, 2, 3, 4]
```

The neighbouring pairs are:

- `1` and `2`
- `2` and `3`
- `3` and `4`

Notice that each number may be used in more than one calculation.

**Requirements:**

- Add each number to the number immediately after it.
- Store the resulting sums in a new list.
- Preserve the order in which the calculations occur.
- Do not modify the original input list.
- Do not add the final number to the first number in this step.
- If the list contains fewer than two numbers, return an empty list.
- The list may contain positive numbers, negative numbers or zero.

**Examples:**

```python
neighbour_sums([1, 2, 3, 4])
# [3, 5, 7]

neighbour_sums([5, 10, 20])
# [15, 30]

neighbour_sums([10, -5, 3])
# [5, -2]

neighbour_sums([0, 0, 0])
# [0, 0]

neighbour_sums([5])
# []

neighbour_sums([])
# []
```

**Things to consider:**

- How do you access an element at a particular index in a list?
- How can you access the next element?
- How will you iterate through the list without going beyond its final index?
- How many sums should be produced for a list containing four numbers?
- What happens when the list contains only one element?

Your function should work with all the examples above before moving to the next step.

## Step 2: Circular Neighbours

The company now wants to process measurements that repeat in a cycle.

For example, some sensors continuously collect readings, and the final measurement in one cycle is followed by the first measurement in the next cycle.

Your current function stops when it reaches the final number because there is no next element.

Extend your solution so that the list behaves as though its ends are connected.

This is known as a **circular list**.

Consider the following list:

```python
[1, 2, 3]
```

The calculations should now be:

- `1 + 2 = 3`
- `2 + 3 = 5`
- `3 + 1 = 4`

Notice that after reaching the final element, the function returns to the beginning of the list.

The result is:

```python
[3, 5, 4]
```

**Requirements:**

- Continue adding each number to its next neighbour.
- When you reach the final element, its next neighbour should be the first element.
- Return one sum for every element in the input list.
- Do not change the order of the original numbers.
- If the list contains one number, add that number to itself.
- If the list is empty, return an empty list.

**Examples:**

```python
neighbour_sums([1, 2, 3])
# [3, 5, 4]

neighbour_sums([10, 20, 30, 40])
# [30, 50, 70, 50]

neighbour_sums([5, 10])
# [15, 15]

neighbour_sums([7])
# [14]

neighbour_sums([])
# []
```

**Things to consider:**

- How can you tell when you have reached the final element?
- How can you return to the first element after reaching the end?
- What changes between Step 1 and Step 2?
- Why does the output now contain the same number of elements as the input?
- What happens when the list contains only two elements?

Your solution should now follow the circular behaviour described in this step. The expected results from Step 1 have changed because of the new requirement.

## Step 3: Configurable Neighbour Distance

The company now wants to compare measurements that are not necessarily next to each other.

Instead of always adding a number to its immediate neighbour, the user should be able to choose how far ahead the second number is.

Extend your function by adding an optional parameter called `distance`.

```python
def neighbour_sums(
    numbers: list[int],
    distance: int = 1
) -> list[int]:
    pass
```

The `distance` parameter determines how many positions ahead the function should look when selecting the second number.

For example, consider:

```python
[10, 20, 30, 40]
```

With `distance=1`, the function behaves exactly as it did in Step 2.

With `distance=2`, the function skips the immediate neighbour and adds the number two positions ahead instead.

The calculations become:

- `10 + 30 = 40`
- `20 + 40 = 60`
- `30 + 10 = 40`
- `40 + 20 = 60`

The result is:

```python
[40, 60, 40, 60]
```

Notice that circular behaviour still applies. When a position goes beyond the end of the list, counting continues from the beginning.

**Requirements:**

- Add each number to the number `distance` positions ahead.
- Continue treating the list as circular.
- Generate one result for every element in the input list.
- If `distance` is not supplied, use the default value of `1`.
- Assume `distance` is always a positive integer.
- Allow distances larger than the length of the list.
- Return an empty list if the input list is empty.
- Do not modify the original input list.

**Examples:**

```python
neighbour_sums([1, 2, 3, 4], distance=2)
# [4, 6, 4, 6]

neighbour_sums([10, 20, 30, 40], distance=1)
# [30, 50, 70, 50]

neighbour_sums([2, 4, 6], distance=3)
# [4, 8, 12]

neighbour_sums([1, 2, 3], distance=4)
# [3, 5, 4]

neighbour_sums([5], distance=2)
# [10]

neighbour_sums([], distance=3)
# []

neighbour_sums([1, 2, 3])
# [3, 5, 4]
```

**Things to consider:**

- How can you calculate which index is `distance` positions ahead?
- What happens when the calculated position is outside the list?
- How can you handle a distance greater than the number of elements?
- What happens when the distance equals the list's length?
- How can you ensure the default parameter preserves the behaviour from Step 2?

## Testing

You should create your own tests using `pytest`.

The examples above are intended to help you understand the requirements, but they are not a complete set of tests.

You are responsible for deciding which cases need testing and writing the tests yourself.

Consider the following when planning your tests:

- How will you verify that neighbouring numbers are added correctly?
- What happens with an empty list or a single-element list?
- Does the function work with negative numbers and zero?
- How will you test the transition from the final element back to the first?
- What happens when the neighbour distance is larger than the number of elements?
- Does the original input list remain unchanged?
- Does the default distance produce the correct circular behaviour?

You should aim to write tests that cover normal behaviour, boundary conditions and edge cases.

Run your tests using:

```bash
pytest -v
```

Remember that a solution passing the provided examples does not necessarily mean it works for every valid input.

## Technical Assessment Practice

Alongside writing your solution, practise explaining your reasoning as though you were completing a technical interview.

Before writing code, consider the following questions:

1. What are the input and output data types?
2. How will you access neighbouring elements in a list?
3. How can you prevent indexing errors?
4. Why does Step 1 produce fewer results than Step 2?
5. How will you implement the circular behaviour?
6. How will your solution change when the distance parameter is introduced?
7. Which edge cases could cause your approach to fail?
8. How would you explain your solution to someone unfamiliar with the problem?

**Start with Step 1.** Focus on understanding how list indexing works and writing your own tests before moving on to circular indexing and configurable distances.
