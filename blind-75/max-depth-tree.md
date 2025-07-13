# Maximum depth of binary tree

## Code
```python
class Solution:
    def traverse(self, node, depth):
        if not node:
            self.max_depth = max(self.max_depth, depth)
            return
        
        self.traverse(node.left, depth+1)
        self.traverse(node.right, depth+1)

    def maxDepth(self, root: Optional[TreeNode]) -> int:
        self.max_depth = 0

        if not root:
            return 0

        self.traverse(root, 0)

        return self.max_depth
```