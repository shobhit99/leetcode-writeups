# Kth smallest element in bst

## Explanation
1. Create an inorder traversal of the bst
> The propery of the bst is that if you do inorder traversal, you will get the elements in sorted order
2. return the idx - 1 from ther created list

## Code
```python
class Solution:
    def traverse(self, node):
        if not node:
            return
        
        self.traverse(node.left)
        self.trail.append(node.val)
        self.traverse(node.right)

    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        self.trail = []

        self.traverse(root)

        return self.trail[k-1]
```