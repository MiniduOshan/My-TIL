# TIL: Divide and Conquer Algorithm

**Date:** 2026-08-10
**Topic:** Algorithms – Divide and Conquer

## What is Divide and Conquer?

**Divide and Conquer** is an algorithmic technique where a large problem is divided into smaller subproblems, each subproblem is solved independently, and the results are combined to produce the final solution.

The general process is:

```text
Divide → Conquer → Combine
```

### 1. Divide

Break the original problem into smaller subproblems.

### 2. Conquer

Solve each smaller subproblem, usually using **recursion**.

### 3. Combine

Combine the results of the smaller problems to obtain the final answer.

---

## Example: Merge Sort

**Merge Sort** is one of the most common examples of Divide and Conquer.

Suppose we have:

```text
[8, 3, 5, 4, 7, 6, 1, 2]
```

### Step 1 – Divide

Split the array into two parts:

```text
[8, 3, 5, 4]    [7, 6, 1, 2]
```

Continue dividing:

```text
[8, 3] [5, 4]    [7, 6] [1, 2]
```

Then:

```text
[8] [3] [5] [4] [7] [6] [1] [2]
```

### Step 2 – Conquer

Sort the small subarrays:

```text
[3, 8] [4, 5]    [6, 7] [1, 2]
```

Then:

```text
[3, 4, 5, 8]    [1, 2, 6, 7]
```

### Step 3 – Combine

Merge the two sorted arrays:

```text
[1, 2, 3, 4, 5, 6, 7, 8]
```

---

## Simple Pseudocode

```text
mergeSort(array):

    if array has one element:
        return array

    divide array into two halves

    left = mergeSort(left half)
    right = mergeSort(right half)

    return merge(left, right)
```

The important part is that `mergeSort()` calls itself on smaller parts of the same problem.

---

## Other Divide and Conquer Algorithms

Some common examples are:

* **Merge Sort**
* **Quick Sort**
* **Binary Search**
* **Strassen's Matrix Multiplication**
* **Closest Pair of Points**
* **Karatsuba Multiplication**

---

## Binary Search Example

Binary Search is another simple example.

Given:

```text
[10, 20, 30, 40, 50, 60, 70]
```

To find `60`:

```text
        40
       /  \
     20    60
          /  \
        50    70
```

Instead of checking every element, the algorithm repeatedly divides the search space in half.

### Time Complexity

```text
O(log n)
```

This makes Binary Search much faster than a simple linear search:

```text
Linear Search → O(n)
Binary Search → O(log n)
```

---

## Advantages

* Breaks complex problems into smaller, manageable problems.
* Often improves algorithm efficiency.
* Naturally works well with recursion.
* Can sometimes be parallelized because subproblems are independent.

## Disadvantages

* Recursion can consume additional memory.
* Some problems have overhead from repeatedly dividing and combining.
* Not every problem can be efficiently solved using Divide and Conquer.

---

## Key Idea

The main concept I learned today is:

```text
                Problem
                   │
                 Divide
                /      \
        Subproblem    Subproblem
             │            │
           Solve        Solve
             \            /
              \          /
                Combine
                   │
                Solution
```

**In short:**

> Divide a large problem into smaller problems, solve them, and combine their results.
