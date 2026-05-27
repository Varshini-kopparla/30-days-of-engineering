# Sorting Algorithms Fundamentals

## What I Learned

Sorting is one of the most fundamental concepts in Data Structures & Algorithms because many advanced problems become easier after sorting data.

Algorithms revised:
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort

---

# 1. Bubble Sort

## Intuition

Repeatedly compare adjacent elements and swap them if they are in the wrong order.

Largest elements gradually “bubble” toward the end of the array.

---

## How It Works

Example:

```txt
5 1 4 2
```

Pass 1:
- compare 5 & 1 → swap
- compare 5 & 4 → swap
- compare 5 & 2 → swap

Largest element reaches correct position.

Repeat for remaining elements.

---

## Time Complexity

| Case | Complexity |
|---|---|
| Best | O(n) |
| Average | O(n²) |
| Worst | O(n²) |

---

## Space Complexity

```txt
O(1)
```

---

## Key Learning

- simple but inefficient
- mostly useful for learning basics
- not used in large-scale systems

---

# 2. Selection Sort

## Intuition

Repeatedly find:
> smallest element

and place it at correct position.

---

## How It Works

For every index:
- find minimum element from remaining array
- swap with current index

---

## Time Complexity

| Case | Complexity |
|---|---|
| Best | O(n²) |
| Average | O(n²) |
| Worst | O(n²) |

---

## Space Complexity

```txt
O(1)
```

---

## Key Learning

- fewer swaps compared to Bubble Sort
- still inefficient for large datasets

---

# 3. Insertion Sort

## Intuition

Build sorted array gradually by inserting elements into correct position.

Works similar to:
> arranging playing cards in hand

---

## How It Works

Take one element at a time:
- compare with previous elements
- shift larger elements
- insert into correct position

---

## Time Complexity

| Case | Complexity |
|---|---|
| Best | O(n) |
| Average | O(n²) |
| Worst | O(n²) |

---

## Space Complexity

```txt
O(1)
```

---

## Key Learning

- efficient for small datasets
- performs well on nearly sorted arrays
- commonly used internally in hybrid sorting algorithms

---

# 4. Merge Sort

## Intuition

Uses:
> Divide and Conquer

Steps:
1. divide array into halves
2. recursively sort both halves
3. merge sorted halves

---

## How It Works

Example:

```txt
[5, 2, 4, 1]
```

Split:

```txt
[5,2] [4,1]
```

Sort recursively:

```txt
[2,5] [1,4]
```

Merge:

```txt
[1,2,4,5]
```

---

## Time Complexity

| Case | Complexity |
|---|---|
| Best | O(n log n) |
| Average | O(n log n) |
| Worst | O(n log n) |

---

## Space Complexity

```txt
O(n)
```

---

## Key Learning

- stable sorting algorithm
- very efficient for large datasets
- heavily used in external sorting systems
- predictable performance

---

# 5. Quick Sort

## Intuition

Also uses:
> Divide and Conquer

Choose:
> pivot element

Then:
- place smaller elements on left
- larger elements on right

Recursively repeat.

---

## How It Works

Example:

```txt
[5, 2, 4, 1]
```

Choose pivot:
```txt
5
```

Partition:

```txt
[2,4,1] 5
```

Recursively sort left side.

---

## Time Complexity

| Case | Complexity |
|---|---|
| Best | O(n log n) |
| Average | O(n log n) |
| Worst | O(n²) |

Worst case happens when:
- pivot selection becomes poor

Example:
- already sorted arrays

---

## Space Complexity

```txt
O(log n)
```

Average recursion stack.

Worst case:
```txt
O(n)
```

---

## Key Learning

- extremely fast in practice
- widely used in real systems
- in-place sorting algorithm
- pivot selection is important

---

# Sorting Comparison

| Algorithm | Best | Average | Worst | Space |
|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) |

---

# Main Takeaways

Important sorting concepts learned:
- comparison-based sorting
- divide and conquer
- stable vs unstable sorting
- in-place sorting
- recursion in sorting algorithms

Key understanding:
- Bubble / Selection / Insertion → simpler but slower
- Merge Sort → stable and predictable
- Quick Sort → fastest in practice for many cases
