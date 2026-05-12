# Arrays

Overview

Arrays are contiguous memory structures allowing O(1) access by index. Java arrays have fixed size; ArrayList is the dynamic alternative.

Common techniques
- Sliding window: maintain a window of indices to compute sums or counts in O(n).
- Two pointers: used for sorted arrays or partitioning problems.

Example problems
- Remove duplicates from sorted array in-place (two pointers), move zeros, etc.

Implementation notes
- Use System.arraycopy for fast block moves.
