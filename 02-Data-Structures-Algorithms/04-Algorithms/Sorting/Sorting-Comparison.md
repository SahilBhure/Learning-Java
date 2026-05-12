# Sorting Comparison

Overview

Compare common sorting algorithms by complexity and characteristics.

Summary
- Bubble Sort: O(n^2), stable, educational
- QuickSort: average O(n log n), unstable, fast in practice
- MergeSort: O(n log n), stable, needs O(n) auxiliary space
- HeapSort: O(n log n), in-place, not stable

Which to use
- For stable sorts on large data: MergeSort (or TimSort used by Java's Arrays.sort on objects)
- For primitive arrays in Java: dual-pivot quicksort (built-in) is fast.
