# Day X - Binary Search Trees (BST)

Today I solved:

1. LeetCode 98 - Validate Binary Search Tree
2. LeetCode 230 - Kth Smallest Element in a BST

---

## 98. Validate Binary Search Tree

### Intuition

A BST is not just about checking whether:

```java
node.left < node < node.right
```

Every node must satisfy the BST property with respect to all its ancestors.

Example:

```text
      5
     / \
    4   6
       / \
      3   7
```

Although 3 is less than 6, it is in the right subtree of 5, so it should be greater than 5. Therefore, this is NOT a valid BST.

The idea is to carry a valid range while traversing:

- Left child must be within (min, node.val)
- Right child must be within (node.val, max)

If any node violates the range, return false.

### Approach

- DFS recursion
- Pass lower and upper bounds
- Check if current node lies within the allowed range
- Recursively validate left and right subtrees

### Time Complexity

```text
O(n)
```

Visit every node once.

### Space Complexity

```text
O(h)
```

Where h is the height of the tree (recursion stack).

- Balanced BST → O(log n)
- Skewed BST → O(n)

### Key Learning

For BST validation, comparing only parent and child is not enough. Every node must satisfy constraints from all its ancestors.

---

## 230. Kth Smallest Element in a BST

### Intuition

Inorder traversal of a BST always gives elements in sorted order.

Example:

```text
      5
     / \
    3   6
   / \
  2   4
 /
1
```

Inorder:

```text
1, 2, 3, 4, 5, 6
```

The kth node visited during inorder traversal is the kth smallest element.

### Approach

- Perform inorder traversal
- Keep a counter
- Increment counter whenever a node is visited
- When counter == k, return that node value

### Time Complexity

```text
O(n)
```

Worst case we may visit all nodes.

### Space Complexity

```text
O(h)
```

Where h is the height of the tree.

- Balanced BST → O(log n)
- Skewed BST → O(n)

### Key Learning

The most important BST property:

```text
Inorder Traversal = Sorted Order
```

This property helps solve many BST problems efficiently.

---

# BST Takeaways

### BST Properties

```text
Left Subtree < Root < Right Subtree
```

### Inorder Traversal

```text
Left → Root → Right
```

Produces sorted order.

### Common BST Patterns

1. Validate BST → Range checking (min/max)
2. Kth Smallest → Inorder traversal
3. Search BST → Use BST property to move left/right
4. Lowest Common Ancestor → Use node values to navigate
5. Delete Node → Handle leaf, one child, two children cases

### Complexity Summary

| Operation | Average | Worst |
|------------|----------|---------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Validate BST | O(n) | O(n) |
| Kth Smallest | O(n) | O(n) |

