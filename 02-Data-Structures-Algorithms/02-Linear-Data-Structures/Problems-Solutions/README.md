# Problems & Solutions

Overview

Curated problems for linear data structures with solutions and complexity analysis. Structure:
- easy.md: common starter problems (reverse list, valid parentheses)
- medium.md: level-up problems (kth-from-end, merge intervals)
- hard.md: advanced problems

Sample problem (kth from end)
- Two-pointer method: advance fast pointer k steps, then move both until fast reaches end; slow will be kth from end.

Solution sketch
```java
Node kthFromEnd(Node head, int k) {
  Node fast = head, slow = head;
  for (int i = 0; i < k; i++) fast = fast.next;
  while (fast != null) { fast = fast.next; slow = slow.next; }
  return slow;
}
```
