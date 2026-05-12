# Linked Lists

Overview

Linked lists store nodes with next (and optional prev) pointers. They are good for insert/remove at known node positions.

Common algorithms
- Reverse a linked list (iterative and recursive)
- Detect cycle (Floyd's tortoise-hare)
- Merge two sorted lists

Reversing example (iterative)
```java
Node prev = null; Node cur = head;
while (cur != null) { Node next = cur.next; cur.next = prev; prev = cur; cur = next; }
return prev; // new head
```
