# Binary Search Problems

Today I practiced Binary Search problems focused on:
- searching in sorted arrays
- finding boundaries
- reducing search space efficiently
- using binary search on answers

Binary Search is one of the most important DSA patterns because it reduces time complexity from:

```txt
O(n) → O(log n)
```

by repeatedly eliminating half of the search space.

---

# 1. Binary Search

https://leetcode.com/problems/binary-search/description/

## Intuition

Since the array is sorted:
- compare target with middle element
- eliminate half of the array every step

If:
- target < mid → search left half
- target > mid → search right half

---

## Time Complexity

```txt
O(log n)
```

---

## Space Complexity

```txt
O(1)
```

---

# 2. Search Insert Position

https://leetcode.com/problems/search-insert-position/

## Intuition

If target exists:
- return its index

If target does not exist:
- return the position where it should be inserted

Binary search helps efficiently find:
> first valid position

---

## Key Learning

Even if target is missing,
binary search can still help find:
- insertion points
- lower bounds
- upper bounds

---

## Time Complexity

```txt
O(log n)
```

---

## Space Complexity

```txt
O(1)
```

---

# 3. First and Last Occurrence of Element in Sorted Array

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

## Intuition

Normal binary search finds:
- any occurrence

But this problem requires:
- leftmost occurrence
- rightmost occurrence

Solution:
- run binary search twice
  - once for first position
  - once for last position

---

## Key Learning

Binary search is not only for exact searching.

It is also heavily used for:
- boundary finding
- lower bound
- upper bound
- first/last occurrence problems

---

## Time Complexity

```txt
O(log n)
```

---

## Space Complexity

```txt
O(1)
```

---

# 4. Square Root Using Binary Search

https://leetcode.com/problems/sqrtx/

## Intuition

Instead of checking every number:
- binary search can search possible answers

Search space becomes:

```txt
1 → x
```

For every middle value:
- check if:

```txt
mid * mid <= x
```

This is called:

> Binary Search on Answer

---

## Key Learning

Binary search can also solve:
- mathematical problems
- optimization problems
- minimum/maximum valid answer problems

without directly searching arrays.

---

## Time Complexity

```txt
O(log n)
```

---

## Space Complexity

```txt
O(1)
```

---

# Main Takeaways

Binary Search works whenever:
- search space is sorted
- answer space is monotonic
- half of possibilities can be eliminated

Important Binary Search patterns learned:
- exact search
- insertion position
- boundary finding
- binary search on answer

Common template:

```txt
mid = low + (high - low) / 2
```

used to avoid integer overflow.
