# DSA Revision Notes

## What I Revised Today

Today I revised the most important DSA fundamental concepts commonly asked in Software Engineering interviews.

The focus was not just on memorizing solutions, but understanding:
- when to use a data structure
- why to use it
- time complexity tradeoffs
- common interview patterns

---

# Time Complexity Cheat Sheet

| Complexity | Example |
|------------|----------|
| O(1) | Array Access |
| O(log n) | Binary Search |
| O(n) | Single Loop |
| O(n log n) | Merge Sort, Quick Sort (Average) |
| O(n²) | Nested Loops, Bubble Sort |
| O(2ⁿ) | Naive Fibonacci |

### Key Interview Tip

Always explain:
1. Approach
2. Time Complexity
3. Space Complexity

---

# Arrays

### When to Use

- Fast indexing needed
- Data stored sequentially
- Frequent reads

### Complexities

| Operation | Complexity |
|------------|------------|
| Access | O(1) |
| Search | O(n) |
| Insert End | O(1) |
| Insert Middle | O(n) |
| Delete | O(n) |

### Common Patterns

- Traversal
- Two Pointers
- Sliding Window
- Prefix Sum
- HashMap

### Common Questions

- Two Sum
- Move Zeroes
- Best Time to Buy & Sell Stock
- Majority Element
- Missing Number
- Merge Sorted Arrays

---

# ArrayList

Dynamic version of an array.

### When to Use

- Size changes frequently
- Need dynamic storage

### Complexities

| Operation | Complexity |
|------------|------------|
| get() | O(1) |
| set() | O(1) |
| add() | O(1) amortized |
| add(index) | O(n) |
| remove(index) | O(n) |

### Array vs ArrayList

| Array | ArrayList |
|---------|---------|
| Fixed Size | Dynamic Size |
| Faster | More Flexible |

---

# Strings

### Important Operations

- length()
- charAt()
- substring()
- split()
- equals()

### Common Questions

- Reverse String
- Valid Palindrome
- Valid Anagram
- Longest Common Prefix

### String vs StringBuilder

| String | StringBuilder |
|----------|----------|
| Immutable | Mutable |
| Slower modifications | Faster modifications |

---

# HashMap

Stores:

```txt
Key → Value
```

### When to Use

- Fast lookup
- Frequency counting
- Caching
- Mapping relationships

### Complexity

| Operation | Complexity |
|------------|------------|
| put() | O(1) |
| get() | O(1) |
| remove() | O(1) |

### Interview Tip

> HashMap often reduces lookup time from O(n) to O(1).

---

# HashSet

Stores unique values.

### When to Use

- Duplicate removal
- Fast existence checks

### Complexity

| Operation | Complexity |
|------------|------------|
| add() | O(1) |
| contains() | O(1) |
| remove() | O(1) |

---

# Binary Search

### Requirement

Array must be sorted.

### Idea

Check middle element and eliminate half of the search space.

### Complexity

```txt
Time: O(log n)
Space: O(1)
```

### Common Questions

- Binary Search
- Search Insert Position
- First & Last Occurrence
- Square Root
- Rotated Sorted Array
- Peak Element

### Interview Answer

> Binary Search works by repeatedly halving the search space.

---

# Linked List

### When to Use

- Frequent insertions/deletions
- Dynamic memory allocation

### Complexity

| Operation | Complexity |
|------------|------------|
| Insert Head | O(1) |
| Delete Head | O(1) |
| Search | O(n) |

### Common Questions

- Reverse Linked List
- Middle Node
- Detect Cycle
- Merge Two Sorted Lists
- Remove Nth Node

### ArrayList vs LinkedList

| ArrayList | LinkedList |
|------------|------------|
| O(1) Access | O(n) Access |
| Better Reads | Better Inserts/Deletes |

---

# Stack

### Principle

```txt
LIFO
(Last In First Out)
```

### When to Use

- DFS
- Undo Operations
- Browser Back Button
- Parentheses Problems

### Operations

- push()
- pop()
- peek()

### Complexity

```txt
O(1)
```

---

# Queue

### Principle

```txt
FIFO
(First In First Out)
```

### When to Use

- BFS
- Scheduling
- Task Processing

### Operations

- offer()
- poll()
- peek()

### Complexity

```txt
O(1)
```

---

# Recursion

### Requirements

1. Base Case
2. Recursive Call

### Interview Tip

> Recursion does not have a fixed complexity. It depends on the number of recursive calls.

### Examples

| Problem | Complexity |
|------------|------------|
| Factorial | O(n) |
| Binary Search | O(log n) |
| Fibonacci | O(2ⁿ) |
| Tree Traversal | O(n) |

---

# Trees

### Terminology

- Root
- Parent
- Child
- Leaf
- Height
- Depth

---

# Binary Tree

Each node has at most two children.

No ordering rule.

### Search Complexity

```txt
O(n)
```

---

# Binary Search Tree (BST)

Rule:

```txt
Left < Root < Right
```

### Advantages

- Faster Search
- Faster Insert
- Faster Delete

### Balanced BST Complexity

| Operation | Complexity |
|------------|------------|
| Search | O(log n) |
| Insert | O(log n) |
| Delete | O(log n) |

### Interview Answer

> All BSTs are Binary Trees, but not all Binary Trees are BSTs.

---

# Tree Traversals

### Inorder

```txt
Left → Root → Right
```

BST Inorder gives:

```txt
Sorted Order
```

---

### Preorder

```txt
Root → Left → Right
```

---

### Postorder

```txt
Left → Right → Root
```

---

### Level Order

Uses:

```txt
Queue + BFS
```

---

# Sorting

## Bubble Sort

### Idea

Largest element bubbles to the end.

### Complexity

```txt
O(n²)
```

---

## Selection Sort

### Idea

Find minimum and place it correctly.

### Complexity

```txt
O(n²)
```

---

## Insertion Sort

### Idea

Like arranging playing cards.

### Complexity

```txt
Best: O(n)
Worst: O(n²)
```

### Good For

Nearly sorted arrays.

---

## Merge Sort

### Idea

```txt
Split
Split
Split

Merge Back
```

### Complexity

```txt
Time: O(n log n)
Space: O(n)
```

### Advantages

- Stable
- Guaranteed O(n log n)

---

## Quick Sort

### Idea

```txt
Choose Pivot
↓
Partition
↓
Repeat
```

### Complexity

```txt
Best: O(n log n)
Average: O(n log n)
Worst: O(n²)
```

### Advantages

- Usually fastest in practice
- Low memory usage

---

# Merge Sort vs Quick Sort

| Feature | Merge Sort | Quick Sort |
|------------|------------|------------|
| Best | O(n log n) | O(n log n) |
| Average | O(n log n) | O(n log n) |
| Worst | O(n log n) | O(n²) |
| Space | O(n) | O(log n) |
| Stable | Yes | No |

### Interview Answer

> Merge Sort guarantees O(n log n) performance but requires extra memory. Quick Sort is usually faster in practice and uses less memory, but its worst case is O(n²).
