# Quick Sort

Overview

QuickSort is a divide-and-conquer algorithm. Average-case O(n log n), worst-case O(n^2) without good pivot selection.

Lomuto partition scheme (example)
```java
int partition(int[] a, int low, int high) {
  int pivot = a[high]; int i = low;
  for (int j = low; j < high; j++) if (a[j] < pivot) { swap(a, i++, j); }
  swap(a, i, high); return i;
}

void quickSort(int[] a, int low, int high) {
  if (low < high) {
    int p = partition(a, low, high);
    quickSort(a, low, p-1);
    quickSort(a, p+1, high);
  }
}
```

Practical tips
- Randomize pivot or use median-of-three to avoid worst-case on sorted inputs.
