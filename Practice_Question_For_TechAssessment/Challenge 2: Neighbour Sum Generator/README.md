# Challenge 2: Neighbour Sum Generator

Create a program that processes a list of numbers and calculates sums using neighbouring elements. Build your solution step by step.

## Background

A company developing sensor-monitoring software wants to analyse measurements collected over time.

The measurements are stored in a Python list, and the company wants to calculate the sum of neighbouring values.

For example, given:

```python
[10, 20, 30, 40]
```

The program should calculate:

- `10 + 20 = 30`
- `20 + 30 = 50`
- `30 + 40 = 70`

The expected result is:

```python
[30, 50, 70]
```

As the requirements develop, the program will also need to support circular lists and configurable distances between elements.

## Step 1: Basic Neighbour Sums

Create a function that takes a list of integers and returns a new list containing the sum of every pair of adjacent numbers.

```python
def neighbour_sums(numbers: list[int]) -> list[int]:
    pass
```

**Requirements:**

- Add each number to the number immediately after it.
- Return the sums in their original order.
- Do not modify the input list.
- Do not add the final number to the first number.
- Return an empty list if fewer than two numbers are provided.
- Support positive numbers, negative numbers and zero.

**Examples:**

```python
neighbour_sums([1, 2, 3, 4])
# [3, 5, 7]

neighbour_sums([5, 10, 20])
# [15, 30]

neighbour_sums([10, -5, 3])
# [5, -2]

neighbour_sums([5])
# []

neighbour_sums([])
# []
```

## Step 2: Circular Neighbours

The company now wants to process measurements that repeat in a cycle.

Extend your function so that the final element is considered a neighbour of the first element.

This is known as a **circular list**.

For example, given:

```python
[1, 2, 3]
```

The calculations should be:

- `1 + 2 = 3`
- `2 + 3 = 5`
- `3 + 1 = 4`

The expected result is `[3, 5, 4]`.

**Requirements:**

- Continue adding each number to its next neighbour.
- After the final element, return to the first element.
- Return one sum for every element in the input list.
- If the list contains one number, add it to itself.
- Return an empty list if the input is empty.
- Do not modify the original list.

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

**Note:** Step 2 changes the behaviour from Step 1 by introducing circular indexing. Your solution should now produce results according to the new requirements.

## Step 3: Configurable Neighbour Distance

The company now wants to compare measurements that are not necessarily next to each other.

Extend your function by introducing an optional parameter called `distance`.

```python
def neighbour_sums(
    numbers: list[int],
    distance: int = 1
) -> list[int]:
    pass
```

The `distance` parameter determines how many positions ahead the second number should be.

For example, given:

```python
[10, 20, 30, 40]
```

With `distance=2`, the calculations become:

- `10 + 30 = 40`
- `20 + 40 = 60`
- `30 + 10 = 40`
- `40 + 20 = 60`

The expected result is `[40, 60, 40, 60]`.

Notice that the list remains circular, so counting continues from the beginning when necessary.

**Requirements:**

- Add each number to the number `distance` positions ahead.
- Continue supporting circular indexing.
- Return one result for every input element.
- Use a default distance of `1`.
- Allow distances larger than the length of the list.
- Assume `distance` is a positive integer.
- Return an empty list if the input is empty.
- Do not modify the original list.

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

Refer to the main **Coding Problems README** for testing requirements and technical assessment preparation guidance.