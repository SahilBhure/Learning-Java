# Heaps

Overview

Heaps are complete binary trees commonly used to implement priority queues. Binary heap supports O(log n) insert and extract-min/max.

Heap operations
- siftUp (after insert) and siftDown (after remove)

Heapify (O(n))
- Building a heap from an array can be done in O(n) by calling siftDown from half of the array backward.
