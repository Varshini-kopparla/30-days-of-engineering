# Binary Tree DFS Problems

A major learning today was understanding how recursion can:
- carry information downward
- return information upward
- solve complex tree problems elegantly.

---

# 1. Binary Tree Maximum Path Sum

https://leetcode.com/problems/binary-tree-maximum-path-sum/

## Intuition

The maximum path can pass through:
- left subtree
- current node
- right subtree

For every node:

```txt
Path Sum = leftGain + node + rightGain
```

But when returning upward,
a node can only choose:
- left path OR right path

because paths cannot split upward.

Negative paths are ignored because they reduce total sum.

---

## Approach

Use DFS recursion:
- calculate maximum gain from left subtree
- calculate maximum gain from right subtree
- ignore negative contributions
- update global maximum path sum
- return best single path upward

This problem combines:
- recursion
- subtree calculations
- global answer tracking

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

# 2. Path Sum

https://leetcode.com/problems/path-sum/
---

## Intuition

We need to check whether:
- any root-to-leaf path
adds up to target sum.

At every node:
- subtract current node value from target
- continue recursion downward

If we reach a leaf node and remaining target becomes zero:
- valid path exists

---

## Approach

Use DFS recursion:
- reduce target sum while traversing
- recursively explore left and right subtrees
- check condition at leaf nodes

This is a classic:
> root-to-leaf traversal problem

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

Recursive stack depends on tree height.

Worst case:
```txt
O(n)
```

Balanced tree:
```txt
O(log n)
```

---

# 3. Sum Root to Leaf Numbers

https://leetcode.com/problems/sum-root-to-leaf-numbers/

---

## Intuition

Each root-to-leaf path forms a number.

Example:

```txt
1 → 2 → 3
```

forms:

```txt
123
```

At every step:
- previous number shifts left by one digit
- current digit gets added

Formula:

```txt
newValue = currentValue * 10 + node.val
```

---

## Approach

Use DFS recursion:
- carry current number while traversing
- build number digit by digit
- when leaf node is reached:
  - add completed number to answer

This problem is mainly about:
- path building
- recursive state propagation

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

Recursive stack depends on tree height.

Worst case:
```txt
O(n)
```

Balanced tree:
```txt
O(log n)
```

