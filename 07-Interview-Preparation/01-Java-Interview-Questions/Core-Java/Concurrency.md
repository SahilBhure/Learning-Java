# Concurrency (Interview Notes)

Expanded notes

Topics covered: threads vs executor, synchronization primitives, volatile, locks, concurrent collections, thread pools, deadlocks, livelocks.

Example: simple producer-consumer using ArrayBlockingQueue
```java
BlockingQueue<Integer> q = new ArrayBlockingQueue<>(100);
ExecutorService ex = Executors.newFixedThreadPool(2);
ex.submit(() -> { for (int i=0;i<100;i++) q.put(i); });
ex.submit(() -> { while(true) System.out.println(q.take()); });
```

Interview tips
- Explain happens-before relationship, memory visibility issues and show brief examples for volatile and synchronized.
