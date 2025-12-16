## Implicit graphs

When we first started looking at graphs, we talked about some common input formats for graphs (adjacency list, adjacency matrix, array of edges, matrix). The problems we have looked at so far have conformed to these input formats, which made it easier for us to identify that the problem should be modeled as a graph. Some problems explicitly told us we were dealing with a graph, while some had a story like "cities connected by roads". Regardless, the input format was usually a giveaway.

Sometimes, a graph is more subtle. The input may look nothing like one of the formats we have talked about. Remember that a graph is any abstract collection of elements (nodes) connected by some abstract relationship (edges). If a problem involves transitioning between states, then try to think about if the states can be nodes and the transition criteria can be edges. Additionally, if the problem wants the shortest path or fewest operations etc., it is a great candidate for BFS. Let's look at some examples.

**Example 1**:
[752. Open the Lock](https://leetcode.com/problems/open-the-lock/description/)

> You have a lock with 4 circular wheels. Each wheel has the digits `0` to `9`. The wheels rotate and wrap around - so `0` can turn to `9` and `9` can turn to `0`. Initially, the lock reads `"0000"`. One move consists of turning a wheel one slot. You are given an array of blocked codes `deadends` - if the lock reads any of these codes, then it can no longer turn. Return the minimum number of moves to make the lock read `target`.

In this problem, we can consider each lock state as a node. The edges are all nodes that differ by only one position by a value of `1`. For example, `"5231"` and `"5331"` are neighbors. From here, we can just perform a simple BFS from `"0000"`, with the one condition that we cannot visit any nodes in deadends. For $O(1)$ checking, let's turn deadends into a set before starting our BFS.

To find the neighbors of a node, we can loop over each of the 4 slots, and each slot, increment and decrement the slot by `1`. To handle the wrap-around case, we can use the modulo operator - `decrement(x) = (x - 1) % 10` and `increment(x) = (x + 1) % 10`. This works because `decrement(0) = 9` and `increment(9) = 0`.

> Just to be a bit cleaner, we can put all the blocked codes from `deadends` in `seen` before starting BFS instead of adding an additional `if` check for if a neighbor is in `deadends`.

```python
class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        def neighbors(node):
            ans = []
            for i in range(4):
                num = int(node[i])
                for change in [-1, 1]:
                    x = (num + change) % 10
                    ans.append(node[:i] + str(x) + node[i + 1:])
            
            return ans

        if "0000" in deadends:
            return -1
        
        queue = deque([("0000", 0)])
        seen = set(deadends)
        seen.add("0000")
        
        while queue:
            node, steps = queue.popleft()
            if node == target:
                return steps
        
            for neighbor in neighbors(node):
                if neighbor not in seen:
                    seen.add(neighbor)
                    queue.append((neighbor, steps + 1))
        
        return -1
```

Technically, the time complexity of this algorithm is $O(d)$, where `d = deadends.length` for converting `deadends` into a set. This is because everything else in the problem is constant (4 wheels, 10 digits). However, if the lock had a variable number of wheels, let's say n, then this changes our time complexity to $O(10^n⋅n^2+d)$. There are $10^n$
different states because each wheel has 10 options. At each state, we perform $O(n^2)$ work because we loop over the `n` wheel while performing string concatenation, which is $O(n)$ for immutable strings. Note that if you have mutable strings (like in C++), then the time complexity reduces to $O(10^n⋅n+d)$.

**Example 2**:
[399. Evaluate Division](https://leetcode.com/problems/evaluate-division/)

> You are given an array `equations` and a number array `values` of the same length. `equations[i] = [x, y]` represents `x / y = values[i]`. You are also given an array `queries` where `queries[i] = [a, b]` which represents the quotient `a / b`. Return an array `answer` where` answer[i]` is the answer to the $i^th$ query, or `-1` if it cannot be determined.

> For example, let's say we have `equations = [["a", "b"], ["b", "c"]]` and `values = [2, 3]`. This input represents 
$\frac{a}{b}=2$ and $\frac{b}{c}=3$. If we had a query `["a", "c"]`, the answer to that query would be $6$, because we can deduce that $\frac{a}{c}=6$

We have some equations $\frac{x}{y}=val$. It's hard to imagine, but these equations are enough to describe a graph!

In all the graph problems we have looked at so far, the graphs have been **unweighted**. A **weight** is a value associated with an edge. For most interviews, weighted graphs are out of scope and require advanced algorithms which is why we have not talked about them yet. In this problem, we can treat each variable x and y as a node. The edges are provided in `equations`, and the weights are provided in `values`.

Let's say we have 3 variables `a, b, c`. We are given that `a / b = 5` and `b / c = 2`. What is `a / c`? We could substitute some values, let's say `a = 10, b = 2, c = 1`. Then the equations work, and we can see that `a / c = 10`. How can we accomplish this through a graph traversal instead of analysis?

$\frac{a}{b}=5$ tells us that `a` is `5` times bigger than `b`. If `a` and `b` are nodes in a graph, then using the edge `a -> b` gives us a multiplier of `5`. $\frac{b}{c}=2$ tells us that `b` is `2` times bigger than `c`. If we use the edge `b -> c` it gives us a multiplier of `2`. Thus, traversing from `a` to `c` would give us a multiplier of `5 * 2 = 10`.

We can create a `graph` using a hash map where each node maps to another hash map containing the relationships given in the input. So with the example above, `a` would map to a hash map which maps `b: 5`. Then, we can do a traversal (BFS or DFS, doesn't matter) for each query - start at the numerator and search for the denominator while associating the current ratio/multiplier (initially `1`) with each node. On each neighbor traversal, we multiply the current ratio with whatever the ratio is between the neighbors.

One more thing: if we have 
$\frac{x}{y}=val$, it also implies $\frac{y}{x}=\frac{1}{val}$, so we should include this when building our graph (the edges are undirected).

```python
from collections import defaultdict

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        def answer_query(start, end):
            # no info on this node
            if start not in graph:
                return -1
            
            seen = {start}
            stack = [(start, 1)]
            
            while stack:
                node, ratio = stack.pop()
                if node == end:
                    return ratio
                
                for neighbor in graph[node]:
                    if neighbor not in seen:
                        seen.add(neighbor)
                        stack.append((neighbor, ratio * graph[node][neighbor]))

            return -1
        
        graph = defaultdict(dict)
        for i in range(len(equations)):
            numerator, denominator = equations[i]
            val = values[i]
            graph[numerator][denominator] = val
            graph[denominator][numerator] = 1 / val
        
        ans = []
        for numerator, denominator in queries:
            ans.append(answer_query(numerator, denominator))
        
        return ans
```

If we have `n` as the number of variables given from `equations` (which is linear with `equations.length` in the worst case) and `q` as the length of queries, then we have a time complexity of $O(q⋅(n+e))$. Each call to `answerQuery` is a traversal on the graph we built, which as we know costs the number of nodes plus the number of edges `n + e`. We perform `q` traversals. If we aren't counting the space used for the output as extra space, then the space complexity is $O(n+e)$ for building `graph`, `seen`, and the recursion call stack.