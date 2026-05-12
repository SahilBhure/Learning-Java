# Binary Search

Overview

Binary search works on sorted arrays with O(log n) time complexity.

Preconditions
- Input must be sorted.

Example (iterative)

```java
int binarySearch(int[] a, int target) {
  int lo = 0, hi = a.length - 1;
  while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (a[mid] == target) return mid;
    if (a[mid] < target) lo = mid + 1; else hi = mid - 1;
  }
  return -1;
}
```

TODO: add variations (first/last occurrence, lower/upper bound).
