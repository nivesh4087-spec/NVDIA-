# Sorting & Searching Algorithm Complexity Analysis

This document provides a comprehensive analysis of time and space complexities for classical sorting and searching algorithms, prepared for **Assignment 1 (Task 4)**.

---

## 📊 Summary Reference Table

| Algorithm | Best Case Time | Worst Case Time | Average Case Time | Space Complexity | Stable? | In-Place? |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Bubble Sort** | $\mathcal{O}(n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | Yes | Yes |
| **Insertion Sort** | $\mathcal{O}(n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | Yes | Yes |
| **Selection Sort** | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | No | Yes |
| **Merge Sort** | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n)$ | Yes | No |
| **Quick Sort** | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(\log n)$ | No | Yes |
| **Linear Search** | $\mathcal{O}(1)$ | $\mathcal{O}(n)$ | $\mathcal{O}(n)$ | $\mathcal{O}(1)$ | N/A | Yes |
| **Binary Search** | $\mathcal{O}(1)$ | $\mathcal{O}(\log n)$ | $\mathcal{O}(\log n)$ | $\mathcal{O}(1)$ | N/A | Yes |

---

## 1. Bubble Sort

### Overview
Bubble Sort iteratively steps through the input list, compares adjacent elements, and swaps them if they are in the wrong order. This pass is repeated until the list is sorted.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(n)$**
  * **One-line why:** With an optimized swapped flag, an already sorted array requires only one pass of $n-1$ comparisons and 0 swaps to confirm it is sorted.
  * *Detailed Reason:* The algorithm traverses the array once. If no elements are swapped during the initial pass, the flag indicates the array is sorted, enabling early termination after $\mathcal{O}(n)$ operations.

* **Worst Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** A reverse-sorted array forces every adjacent pair comparison to result in a swap, requiring $\frac{n(n-1)}{2}$ total operations.
  * *Detailed Reason:* In a reverse-sorted array, each of the $n$ elements must bubble all the way across the array. The outer loop runs $n-1$ times, and the inner loop performs $(n - i)$ comparisons/swaps per pass, summing to $\sum_{i=1}^{n-1} i = \frac{n(n-1)}{2} = \mathcal{O}(n^2)$.

* **Average Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** For randomly ordered elements, roughly half of all adjacent comparisons require swaps, resulting in quadratic time complexity.
  * *Detailed Reason:* On average, the number of inversions in a random sequence is $\frac{n(n-1)}{4}$. Since each swap reduces inversions by 1, the algorithm requires $\mathcal{O}(n^2)$ comparisons and swaps.

* **Space Complexity: $\mathcal{O}(1)$ auxiliary space**
  * Bubble sort sorts the array in-place using only a constant amount of extra memory for loop counters and swap variables.

---

## 2. Insertion Sort

---

## 3. Selection Sort

### Overview
Selection Sort divides the array into a sorted and an unsorted region. It repeatedly selects the smallest (or largest) element from the unsorted region and swaps it into the sorted region.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** Selection sort always scans the entire unsorted subarray to find the minimum element regardless of initial ordering.
  * *Detailed Reason:* The algorithm lacks early termination mechanisms. It performs $(n-1) + (n-2) + \dots + 1 = \frac{n(n-1)}{2}$ comparisons even if the array is already sorted.

* **Worst Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** Complete scanning of unsorted subarrays leads to $\frac{n(n-1)}{2}$ comparisons regardless of input distribution.
  * *Detailed Reason:* Performs $n-1$ outer passes and $\frac{n(n-1)}{2}$ inner loop comparisons. Performs at most $n-1$ swaps.

* **Average Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** Input data permutation does not alter the number of minimum-finding comparisons required.
  * *Detailed Reason:* Comparative count remains strictly deterministic at $\frac{n(n-1)}{2} = \mathcal{O}(n^2)$.

* **Space Complexity: $\mathcal{O}(1)$ auxiliary space**
  * In-place algorithm requiring constant auxiliary variables.

---

## 4. Merge Sort

### Overview
Merge Sort is a Divide-and-Conquer algorithm that divides the input array into two halves, recursively sorts them, and merges the two sorted halves.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(n \log n)$**
  * **One-line why:** Array division into halves creates a tree of depth $\log n$, and merging at each level takes $\mathcal{O}(n)$ time regardless of initial order.
  * *Detailed Reason:* Recurrence relation is $T(n) = 2T(n/2) + \mathcal{O}(n)$. By Master Theorem, $T(n) = \mathcal{O}(n \log n)$.

* **Worst Case Time Complexity: $\mathcal{O}(n \log n)$**
  * **One-line why:** Splitting down to single elements and merging back requires $\log n$ levels with $n$ merge work per level.
  * *Detailed Reason:* The divide step always takes $\mathcal{O}(1)$ time, creating $\log_2 n$ levels. Merging $n$ total elements across all subarrays at level $k$ takes $\mathcal{O}(n)$ time, leading to $n \times \log_2 n = \mathcal{O}(n \log n)$.

* **Average Case Time Complexity: $\mathcal{O}(n \log n)$**
  * **One-line why:** Performance is independent of initial element ordering.

---

## 5. Quick Sort

### Overview
Quick Sort selects a 'pivot' element and partitions the array into two sub-arrays according to whether elements are less than or greater than the pivot, then recursively sorts the sub-arrays.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(n \log n)$**
  * **One-line why:** Pivot choices split the array into two equal halves at every recursion level, forming a tree of height $\log n$.
  * *Detailed Reason:* Recurrence $T(n) = 2T(n/2) + \mathcal{O}(n)$ resolves to $\mathcal{O}(n \log n)$ via Master Theorem.

* **Worst Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** Pivot selection consistently picks the smallest or largest element, creating highly unbalanced partitions of size $0$ and $n-1$.
  * *Detailed Reason:* For an already sorted array with naive pivot choice (e.g. first or last element), the tree depth grows to $n$. The recurrence becomes $T(n) = T(n-1) + \mathcal{O}(n)$, evaluating to $\sum_{i=1}^{n} i = \mathcal{O}(n^2)$.

* **Average Case Time Complexity: $\mathcal{O}(n \log n)$**
  * **One-line why:** Balanced and moderately unbalanced splits average out over all random permutations, yielding expected tree depth of $\mathcal{O}(\log n)$.
  * *Detailed Reason:* Mathematically, even a 90:10 partition split still yields a logarithmic tree depth ($\log_{10/9} n$), keeping overall average execution time at $\mathcal{O}(n \log n)$.

* **Space Complexity: $\mathcal{O}(\log n)$ auxiliary stack space**
  * In-place partitioning requires $\mathcal{O}(1)$ memory, but recursive call stack requires $\mathcal{O}(\log n)$ space in best/average cases and $\mathcal{O}(n)$ in worst case.

---

## 6. Linear Search

### Overview
Linear Search checks every element of a list sequentially until a match is found or the end of the list is reached.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(1)$**
  * **One-line why:** Target item is located at the first index (index 0) of the array, requiring only 1 comparison.
  * *Detailed Reason:* The search loop executes its first check, finds `array[0] == target`, and returns immediately.

* **Worst Case Time Complexity: $\mathcal{O}(n)$**
  * **One-line why:** Target item is either at the final position (index $n-1$) or completely absent from the array.
  * *Detailed Reason:* The search must iterate through all $n$ elements, performing $n$ comparisons before terminating.

* **Average Case Time Complexity: $\mathcal{O}(n)$**
  * **One-line why:** On average for a target present in a random position, the algorithm checks half the elements ($\frac{n+1}{2}$ comparisons).
  * *Detailed Reason:* Assuming uniform probability $\frac{1}{n}$ for target location, expected comparisons = $\frac{1}{n}\sum_{i=1}^{n} i = \frac{n+1}{2} = \mathcal{O}(n)$.

* **Space Complexity: $\mathcal{O}(1)$ auxiliary space**
  * Requires no additional storage beyond search pointers/variables.

---

## 7. Binary Search

### Overview
Binary Search works on pre-sorted arrays by repeatedly dividing the search interval in half.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(1)$**
  * **One-line why:** Target element is located exactly at the middle index on the very first comparison.
  * *Detailed Reason:* The initial middle index calculated `mid = low + (high - low) / 2` immediately matches the target value.

* **Worst Case Time Complexity: $\mathcal{O}(\log n)$**
  * **One-line why:** Target is located at maximum search depth or not present, requiring search space to be halved until size reaches 1.
  * *Detailed Reason:* Starting from size $n$, array size shrinks as $n, n/2, n/4, \dots, 1$. The number of steps required is $\lfloor \log_2 n \rfloor + 1 = \mathcal{O}(\log n)$.

* **Average Case Time Complexity: $\mathcal{O}(\log n)$**
  * **One-line why:** Searching elements at various depths in the binary decision tree averages out to $\mathcal{O}(\log n)$ comparisons.
  * *Detailed Reason:* The average path length in a complete binary search tree of $n$ nodes is $\mathcal{O}(\log n)$.

* **Space Complexity: $\mathcal{O}(1)$ iterative / $\mathcal{O}(\log n)$ recursive**
  * Iterative implementation operates in $\mathcal{O}(1)$ extra memory. Recursive implementation uses $\mathcal{O}(\log n)$ stack frames.

---

## 📌 Summary Recommendations

1. **Small Datasets ($n < 50$):** Insertion sort is often fastest due to low overhead and cache friendliness.
2. **General Purpose Sorting:** Quick Sort (or Timsort/Introsort hybrids) for average speed; Merge Sort when stability is strictly required.
3. **Searching Sorted Data:** Binary Search ($\mathcal{O}(\log n)$) should always be preferred over Linear Search ($\mathcal{O}(n)$).

  * *Detailed Reason:* The recursive branching pattern and element comparison/copying during merge operations remain structurally uniform across all inputs.

* **Space Complexity: $\mathcal{O}(n)$ auxiliary space**
  * Auxiliary array storage of size $n$ is required to hold merged elements during execution.


### Overview
Insertion Sort builds the final sorted array one item at a time by taking elements from the unsorted portion and inserting them into their correct position in the sorted sub-array.

### Time & Space Complexities

* **Best Case Time Complexity: $\mathcal{O}(n)$**
  * **One-line why:** If the array is already sorted, each element is compared once with its predecessor and requires zero shifts.
  * *Detailed Reason:* For every index $i$ from 1 to $n-1$, the element at index $i$ is immediately greater than or equal to the element at $i-1$, causing the inner loop to terminate after 1 comparison. Total comparisons: $n-1$.

* **Worst Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** In a reverse-sorted array, element $i$ must be compared and shifted past all $i$ elements in the sorted sub-array.
  * *Detailed Reason:* Inserting the $i$-th element requires $i$ comparisons and shifts. Summing over all elements yields $\sum_{i=1}^{n-1} i = \frac{n(n-1)}{2} = \mathcal{O}(n^2)$.

* **Average Case Time Complexity: $\mathcal{O}(n^2)$**
  * **One-line why:** On average, element $i$ needs to be shifted past half of the $i$ sorted elements ($\frac{i}{2}$ comparisons), giving quadratic performance.
  * *Detailed Reason:* Total expected operations equal $\sum_{i=1}^{n-1} \frac{i}{2} = \frac{n(n-1)}{4} = \mathcal{O}(n^2)$.

* **Space Complexity: $\mathcal{O}(1)$ auxiliary space**
  * Operates completely in-place using constant extra storage.
