# Bubble Sort

Overview

Bubble sort repeatedly swaps adjacent elements if they are in the wrong order. Simple but inefficient: O(n^2) time.

Optimized bubble sort
- Track if any swaps occur in a pass; if none, array is sorted and you can stop early.

Example
```java
void bubbleSort(int[] a) {
  int n = a.length; boolean swapped;
  for (int i = 0; i < n - 1; i++) {
    swapped = false;
    for (int j = 0; j < n - 1 - i; j++) {
      if (a[j] > a[j+1]) { int t = a[j]; a[j]=a[j+1]; a[j+1]=t; swapped=true; }
    }
    if (!swapped) break;
  }
}
```
