# Queues

Overview

Queues are FIFO. Variants include circular queues, deques, and priority queues.

Implementations
- ArrayDeque for general-purpose queues
- PriorityQueue for ordering by priority
- BlockingQueue implementations for producer-consumer patterns

Example

```java
Queue<Integer> q = new ArrayDeque<>();
q.offer(1);
int v = q.poll();
```

TODO: add circular buffer and lock-free queue notes.
