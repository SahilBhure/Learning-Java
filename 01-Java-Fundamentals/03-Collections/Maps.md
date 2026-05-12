# Maps

Overview

Map is a key-value mapping. Common implementations: HashMap, LinkedHashMap, TreeMap, and ConcurrentHashMap for concurrency.

Complexity & behavior
- HashMap: O(1) average for get/put, null keys allowed (one). Uses chaining/treeify in modern Java for collision handling.
- LinkedHashMap: predictable iteration order (insertion or access-order).
- TreeMap: sorted by keys, O(log n).
- ConcurrentHashMap: thread-safe with better concurrency characteristics than synchronized Map.

Example

```java
Map<String,Integer> counts = new HashMap<>();
counts.put("a", counts.getOrDefault("a", 0) + 1);
```

Best practices
- Implement equals() and hashCode() correctly for custom key types.
- Be careful with mutable keys.

TODO: add examples showing concurrency considerations and iteration idioms.
