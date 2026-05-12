# Lists

Overview

Java Lists are ordered collections that allow duplicate elements. The two primary implementations are ArrayList (backed by a resizable array) and LinkedList (doubly-linked list).

Complexity (typical):
- Access by index: ArrayList O(1), LinkedList O(n)
- Insert at end: ArrayList amortized O(1), LinkedList O(1)
- Insert/remove at middle: ArrayList O(n), LinkedList O(n) (due to traversal)

When to use
- ArrayList: most general-purpose, fast random access.
- LinkedList: frequent insertions/removals at both ends or iterators that modify the list.

Example

```java
List<String> arrayList = new ArrayList<>();
arrayList.add("a");
arrayList.get(0);

List<String> linkedList = new LinkedList<>();
linkedList.addFirst("start");
```

Common pitfalls
- Prefer interfaces (List) over concrete classes when declaring variables.
- Avoid using LinkedList for random access.

References / TODO
- Add step-by-step benchmarks and common interview problems.
