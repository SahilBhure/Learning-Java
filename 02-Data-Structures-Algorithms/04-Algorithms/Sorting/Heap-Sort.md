# Heap Sort

Overview

Heap sort builds a heap and repeatedly extracts the max (or min) to produce a sorted array. O(n log n) time, not stable.

Algorithm sketch
- Build max-heap in O(n) using siftDown starting from middle of array.
- Repeatedly swap root with last element and siftDown on reduced heap.
