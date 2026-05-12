# Sets

Overview

A Set stores unique elements (no duplicates). Common implementations: HashSet, LinkedHashSet, and TreeSet.

Complexity and characteristics
- HashSet: O(1) average for add/remove/contains. No guarantees on order.
- LinkedHashSet: maintains insertion order; slightly higher overhead.
- TreeSet: sorted order (implements SortedSet), operations O(log n).

When to use
- HashSet: fast membership checks.
- LinkedHashSet: preserve insertion order.
- TreeSet: need ordered traversal.

Example

```java
Set<String> s = new HashSet<>();
s.add("apple");
if (s.contains("apple")) { ... }
```

Notes
- Hash collisions affect performance but Java's HashMap/HashSet handle rehashing.
- Use Objects.hash and good equals/hashCode implementations for custom objects.

TODO: add examples for equals/hashCode and LinkedHashSet vs TreeSet.
