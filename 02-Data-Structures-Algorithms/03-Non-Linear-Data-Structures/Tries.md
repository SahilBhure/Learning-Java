# Tries

Overview

Trie (prefix tree) is efficient for prefix operations and autocomplete.

Basic operations
- insert, search, startsWith — each operation runs in O(L) where L is key length.

Example node
```java
class TrieNode { TrieNode[] children = new TrieNode[26]; boolean isWord; }
```

Use-cases: autocomplete, prefix-counting, spell-check suggestions.
