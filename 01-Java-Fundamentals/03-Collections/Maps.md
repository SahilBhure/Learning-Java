# Maps

Overview

Map is a key-value mapping. Common implementations: HashMap, LinkedHashMap, TreeMap, and ConcurrentHashMap for concurrency.

Complexity & behavior
- HashMap: O(1) average for get/put, null keys allowed (one). Uses chaining and treeification in modern Java for collision handling.
- LinkedHashMap: predictable iteration order (insertion or access-order).
- TreeMap: sorted by keys, O(log n).
- ConcurrentHashMap: thread-safe with segment/table-level concurrency.

Examples and idioms

```java
Map<String,Integer> counts = new HashMap<>();
counts.put("a", counts.getOrDefault("a", 0) + 1);

// Iteration
for (Map.Entry<String,Integer> e : counts.entrySet()) {
  System.out.println(e.getKey() + " -> " + e.getValue());
}
```

HashMap internals (overview)
- HashMap computes a hash from the key's hashCode and spreads bits to index into buckets.
- Buckets start as linked lists; when a bucket grows beyond a threshold, Java converts the bucket to a balanced tree (treeify) for O(log n) access.
- Rehashing occurs when size exceeds loadFactor * capacity.

Best practices
- Use immutable or effectively immutable keys.
- Avoid using mutable fields of keys that affect equals/hashCode.
- For concurrency, prefer ConcurrentHashMap or use Collections.synchronizedMap with care.

Interview Q&A
- Describe how HashMap handles collisions and what happens during resizing.
- Explain difference between HashMap and Hashtable.
