# Trees

Overview

Trees are hierarchical data structures. Binary tree nodes have at most two children. Tree traversals: preorder, inorder, postorder, level-order.

Traversal examples
- Recursive inorder:
```java
void inorder(Node n) { if (n == null) return; inorder(n.left); visit(n); inorder(n.right); }
```
- Iterative level-order: use a queue

Common interview problems
- Lowest common ancestor (LCA), diameter of binary tree, serialize/deserialize binary tree.
