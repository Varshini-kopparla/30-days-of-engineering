# Binary Tree Notes

---

# 1. Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

## Approach

Use DFS recursion.

For every node:
- recursively calculate left subtree depth
- recursively calculate right subtree depth
- return:

```txt
1 + max(leftDepth, rightDepth)
```

This works because tree height depends on the deeper subtree.

---

## Why DFS?

DFS naturally explores the tree depth-first,
making it perfect for:
- height problems
- subtree calculations
- recursive tree problems

---

## Time Complexity

```txt
O(n)
```

Reason:
- every node is visited once.

---

## Space Complexity

```txt
O(h)
```

Where:
- `h = height of tree`

Worst case:
```txt
O(n)
```

Balanced tree:
```txt
O(log n)
```

---

# Key Pattern

For tree height problems:

```txt
1 + max(left, right)
```

is a very common pattern.

---

# 2. Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/description/

---

## Approach

Use BFS (Breadth First Search) with a Queue.

Steps:
- add root to queue
- process nodes level by level
- for every node:
  - remove from queue
  - add children into queue
- repeat until queue becomes empty

This guarantees:
- left-to-right traversal
- level-by-level processing

---

## Why BFS?

BFS is naturally designed for:
- level order traversal
- nearest node problems
- shortest path problems

Queue helps process nodes in:
```txt
FIFO order
```

which matches level traversal perfectly.

---

## Time Complexity

```txt
O(n)
```

Reason:
- every node is processed once.

---

## Space Complexity

```txt
O(n)
```

Reason:
- queue may contain an entire tree level.

Worst case:
- last level may contain nearly half the nodes.

---

# Key Pattern

Whenever a problem says:
- level order
- nearest
- shortest path
- minimum steps

Think:

```txt
BFS + Queue
```
