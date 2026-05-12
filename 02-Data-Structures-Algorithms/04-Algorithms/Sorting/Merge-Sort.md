# Merge Sort

Overview

MergeSort divides the array and merges sorted halves. Stable and O(n log n) worst-case.

Recursive merge sort sketch
```java
void mergeSort(int[] a, int l, int r) {
  if (l >= r) return;
  int m = (l + r) >>> 1;
  mergeSort(a, l, m); mergeSort(a, m+1, r);
  merge(a, l, m, r);
}
```

Space and performance
- Typical merges require O(n) extra space; stable and predictable performance.
