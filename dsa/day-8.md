# Binary Tree Zigzag Level Order Traversal

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/

## Intuition

This problem is similar to:
> Binary Tree Level Order Traversal

The only difference is:

- Level 1 → Left to Right
- Level 2 → Right to Left
- Level 3 → Left to Right
- Level 4 → Right to Left

This alternating pattern creates a:
> Zigzag Traversal

---

## Approach

Use BFS (Queue) to process nodes level by level.

For each level:
1. Process all nodes currently in queue.
2. Store values in a temporary list.
3. If current level should be reversed:
   - reverse the list
4. Add level result to final answer.
5. Toggle traversal direction for next level.

---

## Example

```txt
        3
       / \
      9   20
         /  \
        15   7
```

Output:

```txt
[
 [3],
 [20, 9],
 [15, 7]
]
```

Level order:

```txt
Level 0 → Left to Right
Level 1 → Right to Left
Level 2 → Left to Right
```

---

## Why BFS?

BFS naturally processes:
> one level at a time

which makes it easy to alternate directions after every level.

---

## Time Complexity

```txt
O(n)
```

Every node is visited once.

---

## Space Complexity

```txt
O(n)
```

Queue may store an entire level of the tree.

---

# Main Takeaway

Whenever a tree problem mentions:
- level order
- level by level
- nearest nodes
- shortest path

Think:

```txt
BFS + Queue
```

If traversal direction changes per level:

```txt
BFS + Level Processing + Direction Flag
```

