# Binary Tree Basics

## What is a Binary Tree?

A Binary Tree is a tree data structure where each node can have at most:

- one left child
- one right child

Example:

```txt
        1
       / \
      2   3
     / \
    4   5
```

---

# When Are Binary Trees Used?

Binary Trees are useful when data naturally forms a hierarchy.

Common use cases:
- file systems
- organization hierarchies
- databases and indexing
- expression trees
- search systems
- heaps and priority queues

They are also one of the most important topics in coding interviews.

---

# Why Use Binary Trees?

Binary Trees help:
- organize hierarchical data
- perform efficient searching and traversal
- solve recursive problems naturally
- reduce time complexity compared to brute force approaches

Many advanced data structures are built using trees:
- BST
- Heap
- Trie
- Segment Tree
- AVL Tree

---

# Common Traversals

## Inorder Traversal
```txt
Left → Root → Right
```

## Preorder Traversal
```txt
Root → Left → Right
```

## Postorder Traversal
```txt
Left → Right → Root
```

## Level Order Traversal
```txt
Breadth First Search (BFS)
```

---

# Time Complexity

Most tree traversals visit every node once.

## Traversal Complexity

| Operation | Time Complexity |
|---|---|
| DFS Traversals | O(n) |
| BFS Traversal | O(n) |

Where:
- `n = number of nodes`

---

# Problems Solved Today

## 1. Inorder Traversal
https://leetcode.com/problems/binary-tree-inorder-traversal/

## 2. Preorder Traversal
https://leetcode.com/problems/binary-tree-preorder-traversal/description/

## 3. Postorder Traversal
https://leetcode.com/problems/binary-tree-postorder-traversal/description/

## 4. Binary Tree Right Side View
https://leetcode.com/problems/binary-tree-right-side-view/

---

# Key Learning

Tree problems become much easier once recursion and traversal patterns become intuitive.

Most Binary Tree problems are built using:
- DFS
- BFS
- recursion
- level-based traversal
- subtree thinking
