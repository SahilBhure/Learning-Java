# Queue and Stack

Overview

Queue: FIFO data structure. Java provides Queue interface with implementations like LinkedList, ArrayDeque, PriorityQueue.
Stack: LIFO structure. Java's legacy Stack class exists but Deque (ArrayDeque) is preferred.

Common implementations
- ArrayDeque: recommended for stack and queue operations (no capacity overhead of linked nodes).
- PriorityQueue: ordering by priority comparator.
- Stack (legacy): synchronized, avoid in new code.

Example

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);
int top = stack.pop();

Queue<Integer> q = new ArrayDeque<>();
q.offer(1);
int first = q.poll();
```

TODO: add examples for PriorityQueue and concurrent queues (ConcurrentLinkedQueue, LinkedBlockingQueue).
