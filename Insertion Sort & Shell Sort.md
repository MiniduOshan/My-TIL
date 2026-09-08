# 📚 Insertion Sort & Shell Sort

**📅 Date:** September 8, 2026

This repository contains my learning notes and implementations of two comparison-based sorting algorithms:

* 🔹 **Insertion Sort**
* 🔹 **Shell Sort**

---

## 🎯 Learning Objectives

By studying these algorithms, I aim to understand:

* How comparison-based sorting works
* How Insertion Sort builds a sorted sequence
* How Shell Sort improves upon Insertion Sort
* The concept of **gap-based sorting**
* Time and space complexity
* When each algorithm is useful

---

## 🔹 1. Insertion Sort

Insertion Sort builds the sorted portion of an array **one element at a time**.

For each element, the algorithm compares it with the elements before it and shifts larger elements to the right until the correct position is found.

### Example

```text
[5, 3, 4, 1, 2]

[3, 5, 4, 1, 2]
[3, 4, 5, 1, 2]
[1, 3, 4, 5, 2]
[1, 2, 3, 4, 5]
```

### Complexity

| Case    | Time Complexity |
| ------- | --------------- |
| Best    | O(n)            |
| Average | O(n²)           |
| Worst   | O(n²)           |

**Space Complexity:** `O(1)`

---

## 🔹 2. Shell Sort

Shell Sort is an optimization of **Insertion Sort**.

Instead of comparing only adjacent elements, Shell Sort compares elements separated by a certain **gap**.

The gap is gradually reduced until it becomes `1`.

### Example

```text
[8, 5, 3, 7, 6, 2, 4, 1]

Gap = 4
↓
Gap = 2
↓
Gap = 1
↓
Insertion Sort
↓
[1, 2, 3, 4, 5, 6, 7, 8]
```

### Complexity

Shell Sort's performance depends on the **gap sequence** used.

**Space Complexity:** `O(1)`

---

## 🔄 Insertion Sort vs Shell Sort

| Feature      | Insertion Sort                      | Shell Sort                 |
| ------------ | ----------------------------------- | -------------------------- |
| Basic idea   | Insert elements into sorted portion | Sort elements using gaps   |
| Comparison   | Adjacent/nearby elements            | Elements separated by gaps |
| In-place     | ✅                                   | ✅                          |
| Stable       | ✅                                   | ❌                          |
| Extra Space  | O(1)                                | O(1)                       |
| Main concept | Insertion                           | Gap-based insertion        |

---

## 💡 Key Takeaway

> **Insertion Sort** sorts elements by inserting each element into its correct position, while **Shell Sort** improves this idea by allowing elements to move larger distances using gaps.

---

