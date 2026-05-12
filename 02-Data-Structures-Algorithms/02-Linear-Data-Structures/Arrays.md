# Arrays

Overview

Arrays are contiguous memory structures allowing O(1) access by index. Java arrays have fixed size; ArrayList is the dynamic alternative.

Common operations
- Access by index: O(1)
- Search: O(n) unless sorted (binary search: O(log n))
- Insert/delete at arbitrary position: O(n) due to shifting

Example

```java
int[] a = new int[]{1,2,3};
int x = a[0];
```

Patterns
- Two pointers, sliding window, prefix sums are common array techniques in problems.

TODO: add examples and interview problems.
