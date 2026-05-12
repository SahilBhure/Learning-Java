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

Examples and benchmarks

ArrayList append amortized O(1): when capacity is reached, it grows (usually by 1.5x), causing occasional O(n) resizes; amortized cost remains O(1).

```java
List<String> arrayList = new ArrayList<>();
arrayList.add("a");
System.out.println(arrayList.get(0));

List<String> linkedList = new LinkedList<>();
linkedList.addFirst("start");
System.out.println(linkedList.removeFirst());
```

Common interview tasks
- Reverse an ArrayList vs reverse a LinkedList — explain cost of index access and iterator usage.
- Find k-th from end in a LinkedList (two-pointer technique).

Gotchas
- Declaring variables as concrete types (ArrayList) instead of interfaces (List) reduces flexibility.

References
- See Collections.md for interview Q&A and complexity reminders.
