# Queues

Overview

Queues are FIFO. Variants include circular queues, deques, and priority queues.

Circular buffer sketch
- Maintain head, tail indices and size; wrap indices modulo capacity.

Producer-consumer pattern
- Use BlockingQueue implementations (LinkedBlockingQueue, ArrayBlockingQueue) to coordinate producers and consumers safely.
