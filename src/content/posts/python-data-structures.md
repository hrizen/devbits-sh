---
title: 'Python Data Structures'
published: 2025-08-07
draft: false
description: 'A concise reference to Python’s core data structures and when to use them.'
tags: ['python', 'cheatsheet', 'data structures']
---

Python includes a rich set of built-in data structures. This cheatsheet covers the core types, their use cases, and examples.

## Lists

Ordered, mutable sequences.

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("date")
print(fruits[1])  # banana
```

**When to use:** Ordered collections with frequent insertions, deletions, or updates.

## Tuples

Ordered, immutable sequences.

```python
point = (3, 4)
print(point[0])  # 3
```

**When to use:** Fixed collections, function return values, or dictionary keys.

## Sets

Unordered collections of unique elements.

```python
colors = {"red", "green", "blue"}
colors.add("yellow")
print("red" in colors)
```

**When to use:** Membership tests, eliminating duplicates, set operations (`union`, `intersection`).

## Dictionaries

Key-value mappings.

```python
person = {"name": "Alice", "age": 30}
print(person["name"])
person["city"] = "New York"
```

**When to use:** Fast lookups by unique keys, mapping relationships.

## Strings

Immutable sequences of characters.

```python
greeting = "Hello, World"
print(greeting.lower())
```

**When to use:** Text processing, immutable sequences.

## Stacks (via list)

```python
stack = []
stack.append(1)
stack.append(2)
print(stack.pop())  # 2
```

**When to use:** Last-in, first-out (LIFO) data handling.

## Queues

Use `collections.deque` for efficiency.

```python
from collections import deque
queue = deque([1, 2, 3])
queue.append(4)
print(queue.popleft())  # 1
```

**When to use:** First-in, first-out (FIFO) tasks.

## Heaps (Priority Queues)

```python
import heapq
heap = [3, 1, 4]
heapq.heapify(heap)
heapq.heappush(heap, 2)
print(heapq.heappop(heap))  # 1
```

**When to use:** Retrieve smallest/largest items efficiently.

## Arrays

For numeric data, use `array` or `numpy` for performance.

```python
from array import array
nums = array('i', [1, 2, 3])
```

**When to use:** Memory-efficient storage of large numeric data.

## Choosing the Right Structure

| Structure | Ordered | Mutable | Duplicates |
| --------- | ------- | ------- | ---------- |
| list      | Yes     | Yes     | Yes        |
| tuple     | Yes     | No      | Yes        |
| set       | No      | Yes     | No         |
| dict      | No\*    | Yes     | Keys: No   |

\*Insertion order preserved from Python 3.7+.

## Final Thoughts

Knowing Python’s built-in data structures and their performance characteristics helps you write clean, efficient code.
