# Binary Tree Problems — DFS & Tree Construction

---
# 1. Construct Binary Tree from Inorder and Postorder Traversal

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/

---

## Intuition

Important observations:

### Postorder Traversal

```txt
Left → Right → Root
```

So:
- last element is always the root

---

### Inorder Traversal

```txt
Left → Root → Right
```

Using root position:
- left side belongs to left subtree
- right side belongs to right subtree

This helps recursively split the tree.

---

## Approach

Steps:
1. Pick last element from postorder as root
2. Find root index in inorder traversal
3. Split inorder into:
   - left subtree
   - right subtree
4. Recursively build subtrees

HashMap is commonly used to:
- quickly find root index in inorder traversal

---

## Time Complexity

```txt
O(n)
```

Reason:
- every node is processed once
- HashMap provides O(1) index lookup

---

## Space Complexity

```txt
O(n)
```

Used for:
- recursion stack
- HashMap storage

---

# 2. Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

## Intuition

The depth of a tree depends on:
- the maximum depth between left subtree and right subtree

For every node:

```txt
Depth = 1 + max(leftDepth, rightDepth)
```

DFS recursion works naturally because:
- recursion explores subtree depth first
- child depths are calculated before parent

---

## Approach

Use DFS recursion:
- recursively calculate left subtree depth
- recursively calculate right subtree depth
- return the maximum depth

---

## Time Complexity

```txt
O(n)
```

Every node is visited once.

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

# 3. Diameter of Binary Tree

https://leetcode.com/problems/diameter-of-binary-tree/description/

## Intuition

Diameter means:
- longest path between any two nodes

The longest path passing through a node is:

```txt
leftHeight + rightHeight
```

So while calculating height,
we can simultaneously calculate diameter.

---

## Approach

Use DFS recursion:
- calculate left subtree height
- calculate right subtree height
- update diameter using:

```txt
leftHeight + rightHeight
```

Return subtree height upward using:

```txt
1 + max(leftHeight, rightHeight)
```

This combines:
- height calculation
- diameter calculation

in a single DFS traversal.

---

## Time Complexity

```txt
O(n)
```

Every node is processed once.

---

## Space Complexity

```txt
O(h)
```

Recursive call stack depends on tree height.

Worst case:
```txt
O(n)
```

Balanced tree:
```txt
O(log n)
```

---

# Main Learning

Most Binary Tree problems become easier once we identify:
- traversal pattern
- recursive relationship
- subtree dependency

Common DFS tree pattern:

```txt
Solve left subtree
Solve right subtree
Combine results at current node
```

Tree recursion is heavily based on:
- breaking problem into smaller subtrees
- combining subtree results upward.
