# Valid binary search tree

## Explanation

> The propery of the bst is that if we run a inorder traversal on that tree, we get all the elements in ascending order

If you don't get the elements in ascending order after inorder traversal, means it's not a valid bst

## code
```python
class Solution:
    def traverse(self, node):
        if not node:
            return

        self.traverse(node.left)
        self.traversal.append(node.val)
        self.traverse(node.right)

    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        self.traversal = []

        self.traverse(root)

        if not self.traversal:
            return True
        
        for i in range(len(self.traversal)):
            if i == 0:
                continue
            if self.traversal[i-1] >= self.traversal[i]:
                return False
        
        return True
```