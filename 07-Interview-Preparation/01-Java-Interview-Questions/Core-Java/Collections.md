# Collections (Interview Notes)

Extended Q&A

Q: Difference between HashMap and Hashtable?
A: Hashtable is synchronized and legacy. HashMap is unsynchronized and allows null keys.

Q: How does HashMap resize and why load factor matters?
A: When size > loadFactor * capacity, HashMap resizes (allocates bigger table) and rehashes entries. Load factor is a trade-off between memory and collision rate.

Sample question: Design LRU cache — outline using LinkedHashMap with accessOrder=true and overriding removeEldestEntry.

Examples and code snippets included inline.
