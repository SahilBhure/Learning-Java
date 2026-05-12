# Bubble Sort

Overview

Bubble sort repeatedly swaps adjacent elements if they are in the wrong order. Simple but inefficient: O(n^2) time.

Example (conceptual)

```java
for (int i = 0; i < n - 1; i++)
  for (int j = 0; j < n - 1 - i; j++)
    if (a[j] > a[j+1]) swap(a,j,j+1);
```

When to use
- Educational only; for tiny arrays or when stability is needed and n is small.

TODO: add optimizations and visual explanation.
