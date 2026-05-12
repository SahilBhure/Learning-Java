# Big-O Notation

Overview

Big-O notation describes asymptotic upper bounds of algorithm runtime or space requirements. Common classes:
- O(1): constant
- O(log n): logarithmic
- O(n): linear
- O(n log n): linearithmic
- O(n^2): quadratic

Worked example: binary search
- On a sorted array of size n, binary search halves search space each step: O(log n)

Practical tips
- For small n, constants matter; big-O hides constant factors.
- Consider average vs worst-case depending on the use-case.
