# Linear Search

Overview

Linear search checks each element one-by-one and runs in O(n) time.

When to use
- When data is unsorted and small, or when few searches are required.

Example

```java
int indexOf(int[] a, int target) {
  for (int i = 0; i < a.length; i++) if (a[i] == target) return i;
  return -1;
}
```

TODO: add sentinel optimization and variants.
