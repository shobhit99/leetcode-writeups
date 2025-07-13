# Invert binary tree

## Explanation
1. Traverse the node
2. swap the left and right
3. traverse in preorder traversal again

## Code
```python
class Solution:
    def traverse(self, node):
        if not node:
            return

        node.left, node.right = node.right, node.left
        self.traverse(node.left)
        self.traverse(node.right)
        
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        
        self.traverse(root)

        return root
```