# Same tree

## Explanation
1. iterate both tree nodes at once
2. If both nodes are not equal, it means the trees are not same

## Code
```python
class Solution:
    def traverse(self, node1, node2):
        if (node1 and not node2) or (node2 and not node1):
            self.is_same = False
            return
        if not node1 and not node2:
            return
        if node1.val != node2.val:
            self.is_same = False
            return
        
        self.traverse(node1.left, node2.left)
        self.traverse(node1.right, node2.right)

    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        self.is_same = True
        
        self.traverse(p, q)

        return self.is_same
```