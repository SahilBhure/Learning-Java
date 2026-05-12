# Binary Search

Overview

Binary search works on sorted arrays with O(log n) time complexity.

Variants
- Find first/last occurrence, lower bound and upper bound.

First occurrence example (find leftmost index)
```java
int first(int[] a, int target) {
  int lo = 0, hi = a.length - 1, ans = -1;
  while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (a[mid] >= target) { if (a[mid] == target) ans = mid; hi = mid - 1; }
    else lo = mid + 1;
  }
  return ans;
}
```
