# Hash Tables

Overview

Hash tables map keys to values using a hash function. Java's HashMap uses chaining and treeification for skewed buckets.

Key internals
- Initial capacity, load factor (default 0.75), resizing, and treeify threshold.

Performance tips
- Choose good hashCode implementations; avoid using mutable fields in keys.
- Understand that worst-case operations can become O(n) for poor hash distribution but treeify mitigates this.
