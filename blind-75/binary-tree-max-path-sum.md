# Binary tree max path sum

## Explanation
- You return the max of self / self + left / self + right
- For each node traversal You set the global max as max (self / self + left / self + right / self + left + right)

## Code
```python
class Solution:
    def traverse(self, node):
        if not node:
            return 0
        
        left_max = self.traverse(node.left)
        right_max = self.traverse(node.right)

        self.max_sum = max(self.max_sum, node.val + left_max + right_max, node.val, node.val + left_max, node.val + right_max)
        
        return max(node.val+left_max if left_max > 0 else node.val, node.val+right_max if right_max > 0 else node.val)

    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.max_sum = -999999999

        op = self.traverse(root)
        self.max_sum = max(self.max_sum, op)

        return self.max_sum
```