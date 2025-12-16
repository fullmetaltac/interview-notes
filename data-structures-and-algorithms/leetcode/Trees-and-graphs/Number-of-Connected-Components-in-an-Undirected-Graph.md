## Number of Connected Components in an Undirected Graph

You have a graph of `n` nodes. You are given an integer `n` and an array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between `ai` and `bi` in the graph.

Return the number of connected components in the graph.

 

**Example 1**:

![ex1](../../images/conn1-graph.jpg)

```
Input: n = 5, edges = [[0,1],[1,2],[3,4]]
Output: 2
```

**Example 2**:

![ex2](../../images/conn2-graph.jpg)

```
Input: n = 5, edges = [[0,1],[1,2],[2,3],[3,4]]
Output: 1
```
 

**Constraints**:

- `1 <= n <= 2000`
- `1 <= edges.length <= 5000`
- `edges[i].length == 2`
- `0 <= ai <= bi < n`
- `ai != bi`
- There are no repeated edges.

```python
class Solution:
    def dfs(self, adj_list, visited, src):
        visited[src] = True

        for neighbor in adj_list[src]:
            if not visited[neighbor]:
                self.dfs(adj_list, visited, neighbor)

    def countComponents(self, n: int, edges: list[list[int]]) -> int:
        if n == 0:
            return 0

        components = 0
        visited = [False] * n
        adj_list = [[] for _ in range(n)]

        # Build adjacency list
        for u, v in edges:
            adj_list[u].append(v)
            adj_list[v].append(u)

        # Count connected components
        for i in range(n):
            if not visited[i]:
                components += 1
                self.dfs(adj_list, visited, i)

        return components

```