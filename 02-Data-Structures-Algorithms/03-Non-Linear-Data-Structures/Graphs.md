# Graphs

Overview

Graphs model relationships. Representations: adjacency list (sparse), adjacency matrix (dense).

BFS example (shortest unweighted path)
```java
int bfs(List<List<Integer>> adj, int src, int target) {
  int n = adj.size(); boolean[] vis = new boolean[n]; Deque<Integer> q = new ArrayDeque<>();
  q.add(src); vis[src] = true; int depth = 0;
  while (!q.isEmpty()) {
    int sz = q.size();
    for (int i = 0; i < sz; i++) {
      int u = q.poll();
      if (u == target) return depth;
      for (int v : adj.get(u)) if (!vis[v]) { vis[v] = true; q.add(v); }
    }
    depth++;
  }
  return -1; // not reachable
}
```

Common problems: cycle detection, topological sort, shortest paths.
