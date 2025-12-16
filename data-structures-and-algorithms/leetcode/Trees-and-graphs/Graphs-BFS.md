## Graphs - BFS

Like with trees, in many graph problems, it doesn't really matter if you use DFS or BFS, and there are rarely scenarios where DFS performs better than BFS - people just choose DFS because it's faster/cleaner to implement, especially recursively. Every problem we looked at in the previous example could be solved with a BFS.

But, there are some problems where using BFS is clearly better than using DFS. In trees, this was the case when we were concerned with tree levels. In graphs, it is mostly the case when you are asked to find the **shortest path**.

Recall that in binary trees, BFS would visit all nodes at a depth `d` before visiting any node at a depth `d + 1`. BFS visited the nodes **according to their distance from the root**.

99% of the time, a graph will not have a tree structure. But even then, the same logic still applies. Imagine whatever node you start from as a "root". Then, the neighbors of the root represent the next level, and the neighbors of those nodes represent the level after that.

BFS on a graph always visits nodes according to their distance from the **starting point**. This is the key idea behind BFS on graphs - **every time you visit a node**, you must have reached it in the minimum steps possible from wherever you started your BFS.

> The above statement was always the case on binary trees, even if you did a DFS, because there is only one possible path to any node from the root. In a graph, there could be many paths from a given starting point to any other node. Using BFS will ensure that out of all possible paths, you take the shortest one.

We implemented DFS primarily with recursion, which uses a stack under the hood. To implement BFS, we will use a queue (iteratively) instead.

> **Example 1**:
[1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

> Given an `n x n` binary matrix `grid`, return the length of the shortest clear path in the matrix. If there is no clear path, return `-1`. A clear path is a path from the top-left cell `(0, 0)` to the bottom-right cell `(n - 1, n - 1)` such that all visited cells are `0`. You may move 8-directionally (up, down, left, right, or diagonally).

We can treat the matrix as a graph where each square is a node and all squares have up to 8 edges to adjacent squares (up to, because squares on the edges have less due to potential neighbors being out of bounds). There could be many paths on the matrix, but we want the shortest one. Remember: with traversals, we only want to visit each square at most once, not just for efficiency but also to avoid cycles. If we were to do a DFS, we might not find the shortest path. Take the following example:

![Shortest-Path-in-Binary-Matrix](../../images/Shortest-Path-in-Binary-Matrix.png)

The path marked by the arrows is the optimal path (7 squares), and the red path is a path that might happen if you were to use DFS (11 squares). As you can see, the red path is longer and also "uses" up squares on the optimal path, and thus, this algorithm will not produce a correct answer. To find the shortest path, we should use BFS. With BFS, every time we visit a node, it is guaranteed that we reached it in the fewest steps possible. See the following example:

> Green squares represent the current level. Blue squares represent the previous level.

Remember when we looked at BFS on trees, and every iteration of the while loop represented a level/depth? Every time the animation above updates is like another "level" on the graph. Each level has the same distance from the start `(0, 0)` if you were to take the optimal path. With trees, we used a for loop inside of a while loop. This was because we cared about the levels as a whole - we wanted to analyze each level separately (find the maximum element, etc.). Here, we don't really care about the levels as a whole - we just want to reach the end `(n - 1, n - 1)`. As such, we don't need the for loop, just the while loop on a queue. We can store the number of steps we have taken with each node, and once we reach the bottom right we know that we have the answer. Recall that this is because the first time we visit a node with BFS, we know we must have reached it with the minimum possible steps.

> Alternatively, you can keep using the format from the binary tree problems.

> Then, you wouldn't need to store the number of steps taken so far with each node. You could initialize a variable `level` before starting the BFS and increment it every time you move up a level (each while loop iteration = one level). When you encounter the target node `(n - 1, n - 1)`, you can return `level`.

```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        if grid[0][0] == 1:
            return -1
        
        def valid(row, col):
            return 0 <= row < n and 0 <= col < n and grid[row][col] == 0
        
        n = len(grid)
        seen = {(0, 0)}
        queue = deque([(0, 0, 1)]) # row, col, steps
        directions = [(0, 1), (1, 0), (1, 1), (-1, -1), (-1, 1), (1, -1), (0, -1), (-1, 0)]
        
        while queue:
            row, col, steps = queue.popleft()
            if (row, col) == (n - 1, n - 1):
                return steps
            
            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col) and (next_row, next_col) not in seen:
                    seen.add((next_row, next_col))
                    queue.append((next_row, next_col, steps + 1))
        
        return -1
```

If the queue implementation is efficient, then removing from the left is $O(1)$ which makes the work at each node $O(1)$. This means the time complexity is equal to the number of nodes, which is $O(n^2)$. The space complexity is also $O(n^2)$ as `seen` can grow to that size.

> With an efficient queue, BFS has the same time and space complexity as DFS.

The steps taken to implement BFS are very similar to DFS. At each node, do some logic, then iterate over the neighbors (in this case, the 8 directions), check if the neighbor is in `seen`, and if it isn't, add it to `seen` and the queue. The main difference is that we are using a queue instead of a stack.

**Example 2**:
[863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

> Given the `root` of a binary tree, a target node `target` in the tree, and an integer `k`, return an array of the values of all nodes that have a distance `k` from the target node.

In a binary tree, we only have pointers from parents to children. We can easily find the nodes at distance k that are in the target node's subtree, but what about all the other nodes? Let's convert the tree into a graph by assigning every node a `parent` pointer. Then, the tree becomes an undirected graph, and we can use a simple BFS to find the nodes at distance k.

We can perform the parent assignments using either BFS or DFS - it doesn't really matter, so we'll use DFS. Then, we'll perform a BFS starting at `target`, and after we have reached `k` steps, we will return the nodes in the queue.

```python
from collections import deque

class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
        def dfs(node, parent):
            if not node:
                return
            
            node.parent = parent
            dfs(node.left, node)
            dfs(node.right, node)
            
        dfs(root, None)
        queue = deque([target])
        seen = {target}
        distance = 0
        
        while queue and distance < k:
            current_length = len(queue)
            for _ in range(current_length):
                node = queue.popleft()
                for neighbor in [node.left, node.right, node.parent]:
                    if neighbor and neighbor not in seen:
                        seen.add(neighbor)
                        queue.append(neighbor)
            
            distance += 1
        
        return [node.val for node in queue]
```

Both the DFS and BFS perform constant work at each node, and only visit each node at most once. Therefore we have a time and space complexity of $O(n)$ (the space comes from the recursion call stack when we assign the parents, the queue, and `seen`).

**Example 3**:
[542. 01 Matrix](https://leetcode.com/problems/01-matrix/)

> Given an `m x n` binary (every element is `0` or `1`) matrix `mat`, find the distance of the nearest `0` for each cell. The distance between adjacent cells (horizontally or vertically) is `1`.

> For example, given `mat = [[0,0,0],[0,1,0],[1,1,1]]`, return `[[0,0,0],[0,1,0],[1,2,1]]`.

For all `0`, the distance is `0`, so we don't need to change those. For all `1`, we need to find the nearest `0`. One way to solve this is to perform a BFS from each `1` that stops upon finding the first `0` - but this would be very inefficient. Imagine if you had a huge matrix with only `1`. The time complexity would be $O(m^2⋅n^2)$ (each BFS costs $O(m⋅n)$ and we would need to perform $O(m⋅n)$ different BFS if the entire matrix is only `1`, except for a single `0` in a corner). Can we find a linear time approach that avoids visiting the same square multiple times?

Instead of performing the BFS from the ones, what if we started from the zeros? A critical observation is that if we have a square `x` with value `1` and its nearest square with value `0` is `y`, then it doesn't make a difference if we traverse from `x -> y or y -> x`, both take the same number of steps. If we perform a BFS starting from all the zeros, whenever we encounter a `1`, we know that the current number of steps is the answer for that `1`. Using `seen` will prevent the answer from being overridden. Below is a visualization of this process.

```python
from collections import deque

class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n and mat[row][col] == 1
        
        # if you don't want to modify the input, you can create a copy at the start
        m = len(mat)
        n = len(mat[0])
        queue = deque()
        seen = set()
        
        for row in range(m):
            for col in range(n):
                if mat[row][col] == 0:
                    queue.append((row, col, 1))
                    seen.add((row, col))
        
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

        while queue:
            row, col, steps = queue.popleft()
            
            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if (next_row, next_col) not in seen and valid(next_row, next_col):
                    seen.add((next_row, next_col))
                    queue.append((next_row, next_col, steps + 1))
                    mat[next_row][next_col] = steps
        
        return mat
```

This algorithm improves the time complexity to $O(m⋅n)$, because the BFS now only visits each square once, and does a constant amount of work each time. The space complexity is also $O(m⋅n)$ for the queue and seen.

**Example 4**:
[1293. Shortest Path in a Grid with Obstacles Elimination](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

> You are given an `m x n` integer matrix `grid` where each cell is either `0` (empty) or `1` (obstacle). You can move up, down, left, or right from and to an empty cell in one step. Return the minimum number of steps to walk from the upper left corner to the lower right corner given that you can eliminate at most `k` obstacles. If it is not possible, return `-1`.

This problem is almost the same as the first example we looked at in this article. We have a binary matrix, we are allowed to walk along one of the numbers, and we need to find the shortest path from top left to bottom right. The difference with this problem is that we are allowed to eliminate up to `k` obstacles.

Eliminating an obstacle is the same as walking over it. We can add another state variable `remain` that represents how many removals we have remaining. At each square, if a neighbor is an obstacle, we can still walk to it if `remain > 0`.

```python
from collections import deque

class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n
        
        m = len(grid)
        n = len(grid[0])
        queue = deque([(0, 0, k, 0)])
        seen = {(0, 0, k)}
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        
        while queue:
            row, col, remain, steps = queue.popleft()
            if row == m - 1 and col == n - 1:
                return steps
            
            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col):
                    if grid[next_row][next_col] == 0:
                        if (next_row, next_col, remain) not in seen:
                            seen.add((next_row, next_col, remain))
                            queue.append((next_row, next_col, remain, steps + 1))
                    # otherwise, it is an obstacle and we can only pass if we have remaining removals
                    elif remain and (next_row, next_col, remain - 1) not in seen:
                        seen.add((next_row, next_col, remain - 1))
                        queue.append((next_row, next_col, remain - 1, steps + 1))
        
        return -1
```

We said that the time complexity for graph algorithms is $O(nodes+edges)$. The argument was that we never visited a node more than once. Technically, we should be using $s$ instead of $nodes$, where $s$ denotes the number of **states**, and we never visit a state more than once due to `seen`.

It's just that for all the problems we have looked at so far, the `node` entirely described a state. Therefore, we always had $s=nodes$.

In this problem, we have two variables representing a state - `(node, remain)`. There are $m⋅n$ values for `node` and $k$ values for `remain`. This gives us $m⋅n⋅k$ states.

The work done at each state is $O(1)$, which gives us a time complexity of $O(m⋅n⋅k)$. The space complexity is the same, as `seen` grows linearly with the number of states.

**Example 5**:
[1129. Shortest Path with Alternating Colors](https://leetcode.com/problems/shortest-path-with-alternating-colors/)

You are given a directed graph with `n` nodes labeled from `0` to `n - 1`. Edges are red or blue in this graph. You are given `redEdges` and `blueEdges`, where `redEdges[i]` and `blueEdges[i]` both have the format `[x, y]` indicating an edge from `x` to `y` in the respective color. Return an array `ans` of length `n`, where `answer[i]` is the length of the shortest path from `0` to `i` where edge colors alternate, or `-1` if no path exists.

In this problem, we start at node `0` and want to find the shortest path to all other nodes. Normally, a simple BFS with a `steps` variable can accomplish this easily. However, we have the added constraint that the edges we cross must be alternating in color. Let's assign `RED = 0` and `BLUE = 1`. When we do BFS, we can store either `RED` or `BLUE` along with the node to indicate what color the last edge was. We can then perform a BFS starting from both `(0, RED)` and `(0, BLUE)`.

Every time we traverse an edge, we need to first make sure that we are only considering edges of the correct color, and then when making the traversal we need to switch `RED <-> BLUE`.

> One neat trick to flip between `1` and `0` is `f(x) = 1 - x. f(1) = 0` and `f(0) = 1`.

Whenever we introduce new state variables, we need to also include those variables in `seen`. So we treat `(node, color)` as one state and store those states in `seen`.

```python
from collections import defaultdict, deque

class Solution:
    def shortestAlternatingPaths(self, n: int, redEdges: List[List[int]], blueEdges: List[List[int]]) -> List[int]:
        RED = 0
        BLUE = 1
        
        graph = defaultdict(lambda: defaultdict(list))
        for x, y in redEdges:
            graph[RED][x].append(y)
        for x, y in blueEdges:
            graph[BLUE][x].append(y)
        
        ans = [float("inf")] * n
        queue = deque([(0, RED, 0), (0, BLUE, 0)])
        seen = {(0, RED), (0, BLUE)}
        
        while queue:
            node, color, steps = queue.popleft()
            ans[node] = min(ans[node], steps)
            
            for neighbor in graph[color][node]:
                if (neighbor, 1 - color) not in seen:
                    seen.add((neighbor, 1 - color))
                    queue.append((neighbor, 1 - color, steps + 1))
        
        return [x if x != float("inf") else -1 for x in ans]
```

The number of states is the product of the ranges of each state variable. Here, the range of color is always 2, so it doesn't affect the time complexity. This gives us our standard time and space complexity of $O(n+e)$ where $e$ is the total number of edges (both colors).

The space complexity is the same due to graph, seen, and queue.