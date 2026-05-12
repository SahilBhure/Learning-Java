# Sets

Overview

A Set stores unique elements (no duplicates). Common implementations: HashSet, LinkedHashSet, and TreeSet.

Complexity and characteristics
- HashSet: O(1) average for add/remove/contains. No guarantees on order.
- LinkedHashSet: maintains insertion order; slightly higher overhead.
- TreeSet: sorted order (implements SortedSet), operations O(log n).

Examples

```java
Set<String> s = new HashSet<>();
s.add("apple");
if (s.contains("apple")) { System.out.println("has apple"); }

Set<String> linked = new LinkedHashSet<>();
linked.add("a"); linked.add("b"); // preserves order

NavigableSet<Integer> tree = new TreeSet<>();
tree.add(10); tree.add(5); System.out.println(tree.first());
```

Implementing equals/hashCode
- Always override equals() and hashCode() for custom objects used in hash-based sets. Use Objects.hash(...) and compare relevant fields.

Common interview questions
- Explain difference between HashSet and TreeSet and when to use each.
- Implement a custom hash function and discuss collision impacts.

References
- Effective Java: chapters on equals/hashcode and collections.
