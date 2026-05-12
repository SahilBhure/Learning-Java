# Queue and Stack

Overview

Queue: FIFO data structure. Java provides Queue interface with implementations like LinkedList, ArrayDeque, PriorityQueue.
Stack: LIFO structure. Java's legacy Stack class exists but Deque (ArrayDeque) is preferred.

Common implementations
- ArrayDeque: recommended for stack and deque operations (efficient and not thread-safe).
- PriorityQueue: provides ordering by natural order or Comparator.
- BlockingQueue (LinkedBlockingQueue, ArrayBlockingQueue) for producer-consumer patterns.

Examples

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);
int top = stack.pop();

Queue<Integer> q = new ArrayDeque<>();
q.offer(1);
int first = q.poll();

PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5); pq.add(1); System.out.println(pq.poll()); // 1
```

When to use
- Use ArrayDeque for typical stack/queue needs—fast and memory-efficient.
- Use BlockingQueue implementations for thread-safe producer-consumer.

Interview problems
- Design a queue using two stacks (explain amortized costs).
- Implement LRU cache using LinkedHashMap or combination of HashMap + Doubly Linked List.
