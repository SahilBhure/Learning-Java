# AVL Trees

Overview

AVL trees are self-balancing BSTs that maintain height-balance invariant. Rotations (LL, RR, LR, RL) keep height O(log n).

Rotation example (right rotation)
```
    y                x
   / \     ->       / \
  x   T3           T1  y
 / \                  / \
T1  T2               T2  T3
```

Implementation notes
- Maintain height on every node; after insert/delete, update heights and perform rotations as needed.
