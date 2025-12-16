## Closest Binary Search Tree Value

Given the `root` of a binary search tree and a `target` value, return the value in the BST that is closest to the `target`. If there are multiple answers, print the smallest.

**Example 1**:

![closest](../../images/closest1-1-tree.jpg)

```
Input: root = [4,2,5,1,3], target = 3.714286
Output: 4
```

**Example 2**:

```
Input: root = [1], target = 4.428571
Output: 1
```
 

**Constraints**:

- The number of nodes in the tree is in the range `[1, 10^4]`.
- `0 <= Node.val <= 109`
- `-109 <= target <= 109`

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def closestValue(self, root: TreeNode, target: float) -> int:
        def inorder(r: TreeNode):
            return inorder(r.left) + [r.val] + inorder(r.right) if r else []
        
        return min(inorder(root), key = lambda x: abs(target - x))
```