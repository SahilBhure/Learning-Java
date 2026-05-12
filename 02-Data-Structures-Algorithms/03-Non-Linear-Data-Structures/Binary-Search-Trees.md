# Binary Search Trees (BST)

Overview

BST property: left < node < right. Provides average O(log n) search/insert/delete when balanced.

Delete operation (three cases)
- Node with no children: remove.
- Node with one child: replace node with child.
- Node with two children: replace with inorder successor (smallest in right subtree) and delete successor.

Code sketch for delete, insert, search can be added in examples folder.
