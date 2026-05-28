# Binary Tree & BST Problems

---

# 1. Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

## Intuition

Lowest Common Ancestor (LCA) means:
> the lowest node where both target nodes exist in different subtrees

A node can be:
- the ancestor itself
- or where paths from both nodes meet

---

## Approach

Use DFS recursion.

For every node:
- recursively search left subtree
- recursively search right subtree

Cases:
- if both left and right return non-null →
  current node is LCA
- if only one side returns non-null →
  return that node upward
- if current node itself is `p` or `q` →
  return current node

---

## Key Learning

This problem is mainly about:
- recursive subtree exploration
- combining subtree results upward

Very common tree recursion pattern:

```txt
Search left
Search right
Combine results
```

---

## Time Complexity

```txt
O(n)
```

Every node may be visited once.

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

# 2. Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/description/

---

## Intuition

BST inorder traversal gives:
> sorted order

Iterator should:
- return next smallest element efficiently

Instead of storing full inorder traversal:
- use stack to simulate controlled traversal

---

# Important BST Property

For BST:

```txt
Left < Root < Right
```

So:
> inorder traversal produces sorted sequence

---

## Approach

Use stack for iterative inorder traversal.

Steps:
1. push all left nodes into stack
2. top of stack becomes next smallest element
3. after removing node:
   - move to right subtree
   - again push all left nodes

This allows:
- lazy traversal
- efficient next element retrieval

---

## Key Learning

This problem combines:
- BST property
- inorder traversal
- stack-based iteration

Important concept:
> iterative DFS using stack

---

## Time Complexity

### next()

Average:
```txt
O(1)
```

Amortized complexity because every node is pushed/popped once.

---

### hasNext()

```txt
O(1)
```

---

## Space Complexity

```txt
O(h)
```

Stack stores tree height.

Worst case:
```txt
O(n)
```

Balanced BST:
```txt
O(log n)
```
rns learned:
- DFS recursion
- subtree combination
- iterative inorder traversal
- stack-based traversal control
